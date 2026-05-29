---
type: concept
sources:
- 2026-05-25-cluade-pipeline-plan
- chatgpt-llm-based-project-workflow
last_updated: 2026-05-29
---

# MVP Scope

## Consensus

- **Start minimal; don't overbuild.** Pipeline quality and distillation quality matter more than fancy UI.
- **Automate incrementally** from manual Cursor skills — do not jump to full FastAPI/LangChain stack on day one.
- **Markdown + git** as the persistent medium; Obsidian as optional viewer.

## Divergence

| Source | MVP recommendation |
|--------|-------------------|
| ChatGPT | CLI-only; 3 output files; no UI, no knowledge graph |
| Gemini | Obsidian vault + OpenKB/Nashsu + MCP integration |
| Claude | Markdown + git + Obsidian as wiki IDE; manual Phase 3 compile |
| Claude pipeline plan | Open WebUI + scheduler daemon early; FastAPI + React operator after MVP |

## Decision

**MVP remains markdown + git.** The project-wiki submodule pattern (manual ingest/lint/export skills) is the baseline. Obsidian is an optional viewer, not a requirement. 

**v2 operator** (FastAPI + React or Open WebUI Pipelines) is an optional acceleration layer, not a replacement for AGENTS.md schema authority. Add automation (OpenKB, embedding dedup, session harvesters) incrementally only after the manual workflow is proven.

ChatGPT's "no UI" means no custom app on day one — Obsidian as viewer satisfies the need. Claude's pipeline plan diverged from this (Open WebUI early), but the as-built progression (wiki_core → CLI/API → UI → MCP sidecar) validates the incremental approach.

Related: [[pipeline-operator]], [[research-to-implementation-pipeline]], [[implementation-readiness]]
