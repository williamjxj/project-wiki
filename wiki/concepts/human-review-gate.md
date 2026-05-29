---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Human Review Gate

## Consensus

Mandatory checkpoint between wiki distillation (Phase 2) and dev context packaging (Phase 3).

- Never feed unreviewed wiki synthesis to a code agent ([[claude-multi-llm-research-synthesis-workflow]]).
- Human browses compiled wiki, resolves [[contradictions-tracking|unresolved contradictions]], approves export.
- Ingest workflow requires human confirmation before marking sources ingested (AGENTS.md).
- Gemini adds Obsidian review phase; ChatGPT de-emphasizes but doesn't eliminate human oversight.

Phase 3 compile (wiki → dev context) is currently **manual** — export-brief skill is the gate.

## Divergence

| Source | Human involvement |
|--------|------------------|
| Claude | **Non-negotiable** gate; weekly lint; manual Phase 3 compile |
| Gemini | Obsidian synthesis & verification phase; lint health checks |
| ChatGPT | Optimize for automated distillation; less explicit gate |

## Decision

**Keep human review gate for export-brief and ingest confirmation.** Automate ingest mechanics ([[two-stage-ingestion]]) but not approval. Resolve [[contradictions-tracking]] before export.
