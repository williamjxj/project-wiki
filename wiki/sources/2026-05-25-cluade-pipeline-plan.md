---
type: source-summary
raw: raw/llm/2026-05-25-cluade-pipeline-plan.md
source: claude
date: 2026-05-25
---

# Claude: Project-Wiki Pipeline Implementation Plan

## Key Claims

1. **Build pipeline core first** — a shared Python module that all interfaces (CLI, Web UI, MCP) call into, avoiding duplication.
2. **Open WebUI over AnythingLLM** — AnythingLLM is for RAG/Q&A. Open WebUI's Pipelines plugin system maps cleanly to ETL stages and requires zero new infrastructure.
3. **Dirty-only reprocessing** — SQLite tracks what's changed since last run; only reprocess dirty files to avoid burning LLM tokens on unchanged content.
4. **MCP server provides genuine value** — closes the loop: Claude generates wiki → MCP exposes it back → Claude can reference live wiki state without manual copy-paste.
5. **Build order matters**: core → CLI scripts → MCP server → Open WebUI plugin.

## Unique Insights

- **Pipeline stages as a Python module**: `config.yaml` (paths, model, schedule), `ingest.py`, `refine.py`, `synthesize.py`, `export.py`, `runner.py` (orchestrator).
- **CLI interface** with argparse/typer: full run, step-specific, file-watch mode, dry-run.
- **Scheduler** using APScheduler (cross-platform) + watchdog (filesystem trigger), run as systemd/launchd.
- **MCP server** with fastmcp: tools for `run_pipeline`, `get_article`, `list_articles`, `get_run_status`, `search_wiki`.
- **Recommended tech stack**: Python 3.12, anthropic SDK, pydantic, rich, pathlib, sqlite3.
- **Open WebUI Pipelines plugin** exposes pipeline controls as chat commands: `/run`, `/status`, `/run step=refine`, `/preview slug=<article>`.

## Contradictions

- None with first three sources. This is an implementation plan, not a research analysis. It assumes the wiki pattern established by sources 1–3.
- Recommends FastMCP for MCP server — consistent with Gemini's Obsidian MCP recommendation but simpler to implement.
