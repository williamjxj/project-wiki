---
type: concept
sources: [claude-multi-llm-research-synthesis-workflow, gemini-llm-wiki-multi-agent]
last_updated: 2026-05-29
---

# Purpose Steering

## Consensus

Both sources converge on the need for intent guidance beyond structural schema. Claude implies it through "CLAUDE.md as schema." Gemini formalizes it as a dedicated `purpose.md` file.

**Gemini's framework:**
- `CLAUDE.md` / `schema.md` defines *how* to build the wiki (file formats, folder conventions, structural rules)
- `purpose.md` defines *why* the wiki exists (project thesis, engineering goals, core constraints, research boundary)
- The compiling model reads `purpose.md` at the start of every ingestion cycle to prevent knowledge graph drift into irrelevant topics

## Divergence

| Aspect | Claude | Gemini |
|--------|-------|--------|
| Mechanism | Schema file (CLAUDE.md/AGENTS.md) | Dual file: schema.md + purpose.md |
| Intent layer | Implicit in dev context package | Explicit purpose.md read at every ingest |
| Drift prevention | Not addressed | Primary purpose of purpose.md |

## Decision

Purpose steering is confirmed as a design principle. Implement with a dedicated `purpose.md` file that the LLM reads before every ingest cycle to maintain focus and prevent scope drift.
