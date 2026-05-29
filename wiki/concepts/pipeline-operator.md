---
type: concept
sources: [2026-05-25-cluade-pipeline-plan]
last_updated: 2026-05-29
---

# Pipeline Operator

## Consensus

The pipeline operator is a Python core module that orchestrates the wiki pipeline with multiple interface frontends (CLI, API, MCP, Web UI) all calling into a shared library. This architectural principle is confirmed by the actual implementation.

## Planned vs Actual

The source 4 plan describes a flat structure with separate ingest/refine/synthesize/export modules. The actual implementation evolved into a richer architecture:

| Aspect | Planned (source 4) | Actual (pipeline/) |
|--------|-------------------|-------------------|
| **Core module** | `pipeline/runner.py` orchestrating flat `ingest.py`, `refine.py`, `synthesize.py`, `export.py` | `pipeline/wiki_core/` shared library: `fs.py`, `graph.py`, `lint.py`, `models.py`, `paths.py`, `status.py`, `sync.py` |
| **State tracking** | SQLite in runner.py | SQLite (via job modules in `pipeline/api/jobs.py`) |
| **LLM integration** | Implicit in ingest/refine steps | `pipeline/llm/` — separate module with ingest + export workflow packages |
| **CLI** | argparse/typer with `--watch`, `--dry-run` | Typer CLI in `pipeline/cli/` |
| **MCP** | fastmcp: 5 tools (run_pipeline, get_article, list_articles, get_run_status, search_wiki) | fastmcp: 5 tools (list_pending, read_page, run_lint, get_status, run_sync) — different tool set |
| **Web UI** | Open WebUI Pipelines plugin | Custom React dashboard (`pipeline/ui/`) + FastAPI (`pipeline/api/`) |
| **Auto-pipeline** | Not described | `pipeline/workflows/auto.py` — pre-approved auto mode with 2 LLM passes, no human gates |
| **API layer** | Not described | `pipeline/api/` — FastAPI with job orchestration |
| **Test suite** | Not described | `pipeline/tests/` |

## Key Differences

1. **wiki_core as shared library** replaced the flat module structure — cleaner separation, CLI/API/MCP all call into the same core
2. **FastAPI + custom React UI** replaced the planned Open WebUI Pipelines plugin — more control, same architectural principle
3. **Auto-pipeline workflow** emerged as a new concept not in the original plan — pre-approval mode for experienced operators
4. **MCP tool set** shifted from pipeline execution tools to wiki inspection tools — more practical for Claude Code integration
5. **Build order** was core → CLI → MCP → Web UI — actual order included API before UI, MCP was added later

## Decision

The architectural principle is validated: shared core with multiple interface frontends. The actual implementation is richer than planned, with an additional API layer, custom UI, and auto-pipeline workflow. The original plan served as direction, not specification. Future development should align with the actual `pipeline/wiki_core/` structure rather than the source 4 flat layout.
