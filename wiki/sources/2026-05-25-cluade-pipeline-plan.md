---
type: source-summary
raw: raw/llm/2026-05-25-cluade-pipeline-plan.md
source: claude
date: 2026-05-25
---

# Claude Pipeline Feature Plan

## Key Claims

- Build a shared **Python pipeline core** first; Web UI, automation, and MCP attach to it.
- **Open WebUI Pipelines** recommended over AnythingLLM for ETL-style pipeline control (chat commands: `/run`, `/status`, `/preview`).
- **Autonomous scripts**: Typer CLI + APScheduler daemon + watchdog for dirty-file reprocessing; SQLite run-state.
- **MCP server** (FastMCP sketch): `run_pipeline`, `get_article`, `list_articles`, `get_run_status`, `search_wiki`.
- Proposed build order: core → CLI → MCP → Open WebUI plugin.

## Unique Insights

- Treats Open WebUI as a zero-new-infra UI harness via Pipelines plugin — not a custom React app.
- SQLite dirty-tracking to avoid reprocessing unchanged wiki articles.
- MCP framed as closing the Claude loop (wiki state back into Claude Code sessions).

## Contradictions

- Proposes Open WebUI / FastAPI stack; **this repo implemented a dedicated FastAPI + React operator** instead ([[mvp-scope]] divergence — see [[pipeline-operator]]).
- Raw plan places MCP before UI; experimental-app shipped **wiki_core → CLI/API → UI → MCP sidecar** ([[research-to-implementation-pipeline]]).
