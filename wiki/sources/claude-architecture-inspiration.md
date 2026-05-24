---
type: source-summary
raw: raw/llm/2026-05-11-claude-architecture-inspiration.md
source: claude
date: 2026-05-11
---

# Architecture Decision & Inspiration

## Key Claims

- Two plans: second brain (chat + Phase A/B) vs middleware delegator (/ingest, /query); middleware largely built.
- Karpathy: compile once, query compiled wiki; scales ~100–200 pages before stronger search.
- Spisak counter: domain vaults, skills as commands, qmd hybrid search, tiered models.
- mem-weaver = Karpathy compilation + DB indexing ahead of gist-only pattern.
- Hybrid RAG + wiki is pragmatic; contradiction surfacing is key guardrail.
- Recommend merge: add POST /chat, wire taxonomy, optional wiki folder split.
- Ecosystem matrix: SuperLocalMemory, M2A, Mem0, etc.

## Unique Insights

- Positions mem-weaver synthesis as Karpathy simplicity + Spisak scale levers.
- Future: memory decay, tiered memory, graph traversal, MCP.

## Contradictions

Claims embeddings + RRF hybrid done; conflicts with [[claude-mem-weaver-competitive-analysis]] — [[mem-weaver-as-built-status]].

**Resolved (2026-05-24):** Codebase audit confirms hybrid search, Phase 4, and ingest pipeline built. See [[mem-weaver-as-built-status]].

Related concepts: [[mem-weaver-architecture]] [[memory-synthesis-vs-rag]] [[mem-weaver-as-built-status]]
