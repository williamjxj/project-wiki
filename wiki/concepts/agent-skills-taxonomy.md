---
type: concept
sources:
  - gemini-llm-memory-research
  - claude-second-brain-prd
  - claude-second-brain-implementation
  - gemini-second-brain-design
  - chatgpt-mem-weaver-v2-roadmap
  - claude-frontend-admin-integration
last_updated: 2026-05-24
---

# Agent Skills Taxonomy

## Consensus

- Memory chunks organized like **Agent Skills**: categorized by topic/keywords, triggered at query time when user question matches.
- **Storage options:** tiered Markdown folders, `SKILL.md` packaging, or `_index.md` keyword routing table.
- **Retrieval flow:** scan index for keyword overlap → load matching wiki page(s) → inject into public LLM prompt (cap ~3000 chars).
- **Synthesis prompt:** ask Ollama to "compile into a skill" — extract facts, constraints, decisions; format as Markdown with category tags.
- **Value gate:** skip synthesis when Q+A contains no reusable technical insight (`SKIP` vs `PROCESS`).

## Divergence

| Topic | [[gemini-llm-memory-research]] | [[claude-second-brain-implementation]] |
|-------|----------------------------------|----------------------------------------|
| Index mechanism | Fast keyword scan of `/wiki/index.md` (no LLM) | `_index.md` + SKILL_TAXONOMY in code |
| Taxonomy source | Predefined list vs Ollama auto-keywords | Agent-Skills keyword triggers + Ollama fallback |
| Skill format | `SKILL.md` standard for portability | Fixed page schema (Facts, Gotchas, Related) |

## Decision

**Done:** `SKILL_TAXONOMY` wired in `classifier.py` (P0 from [[chatgpt-mem-weaver-v2-roadmap]]).

**Gap:** chat retriever reads `_index.md` pipe-table format; ingest appends to `wiki/index.md` catalog style. **Fix:** unify on one index format — either teach ingest to write `_index.md` rows or point retriever at `wiki/index.md` + hybrid search fallback (already implemented).

Related: [[dual-llm-memory-pipeline]], [[mem-weaver-architecture]], [[implementation-milestones]]
