---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Purpose Steering

## Consensus

Every ingestion cycle must read intent guidance alongside structural schema ([[gemini-llm-wiki-multi-agent]]):

| File | Answers | Contains |
|------|---------|----------|
| `schema.md` / `AGENTS.md` | *How* to build the wiki | File formats, folder conventions, naming rules |
| `purpose.md` | *Why* the wiki exists | Project thesis, engineering goals, constraints, research boundaries |

Without [[purpose-steering]], the [[compounding-knowledge-layer]] drifts into irrelevant topics. Claude's Phase 3 `spec.md` serves similar steering at export time. ChatGPT's [[decision-records]] and constraints docs partially cover intent.

Related: [[mvp-scope]] defines what to build first; [[implementation-readiness]] defines success.

## Divergence

| Source | View |
|--------|------|
| Gemini | Explicit root `purpose.md` read at every ingest cycle |
| Claude | `spec.md` at export time; `AGENTS.md` for schema |
| ChatGPT | Constraints and decision records; no `purpose.md` |

## Decision

**Lean: add `purpose.md` to parent project root.** Wiki `AGENTS.md` handles schema; parent `docs/PROJECT_BRIEF.md` evolves from export-brief into purpose steering.
