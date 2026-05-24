---
type: concept
sources:
  - chatgpt-retrieval-vs-synthesis
  - claude-architecture-inspiration
  - chatgpt-api-token-context-management
last_updated: 2026-05-24
---

# Memory Synthesis vs RAG Retrieval

## Consensus

- **RAG:** embed query, retrieve raw chunks from vector store, append to prompt at query time — good for factual lookup, starts from scratch each time.
- **LLM Wiki (synthesis):** LLM incrementally writes/maintains persistent wiki pages; knowledge "compiles" over time (Karpathy pattern).
- **Hybrid is pragmatic:** compile conversations into wiki (synthesis) plus search/index at query time (FTS5, embeddings, RRF) — not either/or.
- **API advantage over web chat:** developers control context per request — sliding window, summarization, selective recall — enabling custom memory architectures impossible in auto-accumulating web UIs.

## Divergence

| Approach | Strength | Weakness |
|----------|----------|----------|
| Vector/RAG | Good for large document corpora | Raw retrieval can miss synthesis; context bloat if chunks are verbose |
| LLM Wiki synthesis | Compact, human-readable, compounding knowledge | Summary quality depends on local model; risk of over-compression |
| Graph memory (Hindsight, MemGPT) | Entity/relation reasoning | Higher complexity; mem-weaver wikilinks are flat today |

## Decision

Adopt **synthesis-first wiki compilation** with **hybrid retrieval** (FTS5 + sqlite-vec + RRF) for query — aligned across [[claude-architecture-inspiration]] and [[chatgpt-mem-weaver-v2-roadmap]]. Confirmed implemented in mem-weaver codebase per [[mem-weaver-as-built-status]].

Related: [[dual-llm-memory-pipeline]], [[mem-weaver-architecture]]
