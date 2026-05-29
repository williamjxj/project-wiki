---
type: llm-chat
source: claude
topic: project-wiki pipeline feature implementation plan
date: 2026-05-25
status: ingested
question: How should we implement Web UI, autonomous scripts, and MCP for the project-wiki
  pipeline?
---

## Draft: project-wiki Pipeline — Feature Implementation Plan

---

### Overview

The project has three independent but composable layers to add: a **Web UI** harness, an **automation layer**, and an **MCP server**. They share a common Python pipeline core, so the right move is to build that core first and let the other three attach to it.

---

### 1. Pipeline Core (prerequisite for everything else)

Before adding any interface, refactor the current manual `/wiki-ingest` skill steps into a proper Python pipeline module. This becomes the single source of truth all three features call into.

**Structure:**

```
project-wiki/
├── wiki/                    # source llm-wiki articles (.md)
├── pipeline/
│   ├── __init__.py
│   ├── config.yaml          # paths, model, schedule, flags
│   ├── ingest.py            # step 1 — collect & parse wiki sources
│   ├── refine.py            # step 2 — distill/clean via LLM
│   ├── synthesize.py        # step 3 — cross-article synthesis
│   ├── export.py            # step 4 — emit final docs
│   └── runner.py            # orchestrator: chains all steps, handles state
├── scripts/
│   ├── run_pipeline.py      # CLI entry point
│   └── scheduler.py        # autonomous daemon
├── mcp_server/
│   └── server.py            # MCP server (feature 3)
├── open_webui/
│   └── pipeline_fn.py       # Open WebUI pipeline function (feature 1)
└── CLAUDE.md
```

**Tech stack:** Python 3.12, `anthropic` SDK, `pydantic` for config/validation, `rich` for CLI output, `pathlib` throughout, `sqlite3` for lightweight run-state tracking (what's been processed, last modified timestamps, errors).

---

### 2. Feature 1 — Web UI

**Recommendation: Open WebUI over AnythingLLM.**

AnythingLLM is better suited for RAG/document Q&A. Open WebUI has an explicit **Pipelines** plugin system — you write a Python class with `pipe()` and it becomes a selectable model in the chat UI. This maps cleanly to your ETL steps and requires zero new infrastructure since you already have it running.

**Implementation:** Create `open_webui/pipeline_fn.py` as an Open WebUI Pipeline plugin. It exposes pipeline controls as chat commands:

- `/run` — triggers the full pipeline
- `/status` — shows last run state, counts, errors
- `/run step=refine` — runs a single stage
- `/preview slug=<article>` — shows the refined output for one article before committing

The plugin calls into `pipeline/runner.py` directly. Open WebUI handles the UI, auth, and history for free.

**Harness requirements:** Open WebUI must have Pipelines enabled (Settings → Admin → Pipelines). The plugin file is dropped into the Pipelines directory and registered via the admin panel. No code changes to Open WebUI itself.

---

### 3. Feature 2 — Autonomous Scripts

Two modes: **on-demand CLI** and **scheduled daemon**.

**CLI (`scripts/run_pipeline.py`):**

```bash
python run_pipeline.py              # full run
python run_pipeline.py --step refine
python run_pipeline.py --watch      # file-watch mode: re-runs on wiki/ changes
python run_pipeline.py --dry-run    # show what would change, no writes
```

Built with `argparse` (or `typer` for nicer ergonomics), calls `runner.py`.

**Scheduler (`scripts/scheduler.py`):**

Use `APScheduler` (not cron — keeps it cross-platform and configurable from `config.yaml`). Runs as a background daemon:

```yaml
# config.yaml
schedule:
  enabled: true
  cron: "0 3 * * *"     # daily at 3am
  watch_dir: ./wiki      # also trigger on file changes
```

`watchdog` handles the filesystem watch trigger. SQLite tracks which articles have changed since the last run so only dirty files are reprocessed — avoids burning LLM tokens on unchanged content.

**Harness requirements:** Python environment with `apscheduler`, `watchdog`, `anthropic`. Run as a `systemd` service or `launchd` plist for persistence. A `Makefile` with `make start`, `make stop`, `make status` targets keeps it manageable.

---

### 4. Feature 3 — MCP Server

**Verdict: genuine value, not just sugar** — specifically because you are already in the Claude ecosystem. An MCP server means Claude Code (and any other MCP client) can directly invoke pipeline operations, query article status, and retrieve synthesized docs as tool results during a coding or writing session. That closes the loop: Claude generates wiki → MCP exposes it back to Claude → Claude can reference live wiki state without manual copy-paste.

**Tools to expose:**

| Tool | Description |
|---|---|
| `run_pipeline` | Trigger full or partial pipeline run |
| `get_article` | Retrieve a specific wiki article by slug |
| `list_articles` | List all articles with status (raw / refined / synthesized) |
| `get_run_status` | Last run timestamp, counts, any errors |
| `search_wiki` | Simple keyword/tag search across articles |

**Tech stack:** `fastmcp` (the FastAPI-style MCP library — far less boilerplate than the raw SDK). Server runs locally on a fixed port, registered in `~/.claude/mcp_servers.json` for Claude Code.

```python
# mcp_server/server.py (sketch)
from fastmcp import FastMCP
from pipeline.runner import run, get_status
from pipeline.ingest import list_articles, get_article

mcp = FastMCP("project-wiki")

@mcp.tool()
def run_pipeline(step: str = "all") -> str:
    return run(step=step)

@mcp.tool()
def get_article(slug: str) -> str:
    return get_article(slug)
```

**Harness requirements:** `fastmcp` installed, server started with `python mcp_server/server.py`, one JSON entry in the MCP config. No external hosting needed — local only.

---

### Summary

| Feature | Framework | Key Libs | Effort |
|---|---|---|---|
| Pipeline core | Python 3.12 | `anthropic`, `pydantic`, `sqlite3` | Medium — do this first |
| Web UI | Open WebUI Pipelines | existing install | Low — one plugin file |
| Autonomous scripts | APScheduler + watchdog | `apscheduler`, `watchdog`, `typer` | Low–medium |
| MCP server | FastMCP | `fastmcp` | Low — ~50 lines of server code |

Build order: **core → CLI scripts → MCP server → Open WebUI plugin**. The MCP server and Open WebUI plugin are both thin wrappers over the same core, so doing them last means minimal rework.