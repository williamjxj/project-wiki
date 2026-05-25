---
type: concept
sources:
- 2026-05-25-cluade-pipeline-plan
- chatgpt-llm-based-project-workflow
last_updated: 2026-05-25
---

# MVP Scope

## Consensus

Start minimal; don't overbuild. Pipeline quality and distillation quality matter more than fancy UI.

## Divergence

| Source | MVP recommendation |
|--------|-------------------|
| ChatGPT | CLI-only; 3 output files; no UI, no knowledge graph |
| Gemini | Obsidian vault + OpenKB/Nashsu + MCP integration |
| Claude | Markdown + git + Obsidian as wiki IDE; manual Phase 3 compile |

## Decision

**Lean: match current project-wiki submodule pattern** — markdown wiki in git, Obsidian as optional viewer, manual ingest/lint/export skills. Add automation (OpenKB, embedding dedup, session harvesters) incrementally. ChatGPT's "no UI" means no custom app UI — Obsidian as viewer is fine.

# MVP Scope

## Consensus

Automate incrementally from manual Cursor skills — do not jump to full FastAPI/LangChain stack on day one.

## Divergence

Claude's follow-on plan proposes Open WebUI + scheduler daemon early; experimental-app v2 added a **local operator app** after manual workflow was proven.

## Decision

MVP remains markdown + git; v2 operator is an optional acceleration layer, not a replacement for `AGENTS.md` schema authority.
