---
type: source-summary
raw: raw/llm/2026-05-11-claude-second-brain-implementation.md
source: claude
date: 2026-05-11
---

# Second Brain Implementation Plan

## Key Claims

- Modular FastAPI delegator + Ollama compiler + Markdown wiki + Next.js chat with WikiSidebar.
- Phase A sync / Phase B async pattern with value gate and incremental merge.
- Agent-Skills taxonomy for topic routing; injection cap ~3000 chars.
- Wiki page schema: Facts, Gotchas, Related; optional .bak versioning.
- Phase 4: semantic search via nomic-embed-text, sqlite-vec, hybrid RRF.
- RAM-tier table mapping Mac specs to Ollama model size.
- Later phases: graph overlay (Graphiti/Zep-style).

## Unique Insights

- Priming injection as synthetic user/assistant exchange.
- Same-topic turns merge into one denser article over time.

## Contradictions

Claims Phase 4 semantic search done; [[claude-mem-weaver-competitive-analysis]] disputes — see [[mem-weaver-as-built-status]].

**Resolved (2026-05-24):** Phase 4 semantic search and async ingest confirmed built. Value gate and _index.md alignment still open. See [[mem-weaver-as-built-status]], [[dual-llm-memory-pipeline]].

## Related sources

[[claude-second-brain-prd]], [[gemini-second-brain-design]], [[claude-architecture-inspiration]]

Related concepts: [[dual-llm-memory-pipeline]] [[mem-weaver-architecture]] [[agent-skills-taxonomy]]
