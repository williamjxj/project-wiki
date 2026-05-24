---
type: concept
sources:
  - claude-architecture-inspiration
  - chatgpt-mem-weaver-v2-roadmap
  - claude-mem-weaver-competitive-analysis
  - claude-phase-4-hardening-plan
last_updated: 2026-05-24
---

# mem-weaver As-Built Status

> Audited against `/Users/william.jiang/my-playgrounds/mem-weaver` on 2026-05-24.

## Consensus

**v1 backend is substantially built.** FastAPI delegator, ingest worker, SQLite+FTS5, hybrid search (sqlite-vec + RRF), contradiction guardrails, wikilink graph, DLQ, `POST /chat` (SSE), and MCP server all exist in code.

## Divergence

| Capability | Codebase audit (2026-05-24) | [[claude-mem-weaver-competitive-analysis]] (2026-05-15) |
|------------|----------------------------|--------------------------------------------------------|
| Hybrid semantic search | **Done** — `embedder.py`, `query_search.py`, `002_semantic_search.sql` | Claims not built; **stale** |
| Phase 4 hardening | **Done** — contradictions, `wiki_graph.py`, DLQ, `/stats` | Partially reflected |
| POST /chat | **Done** — `main.py` SSE + background ingest | Claims Phase A absent; **stale** |
| MCP server | **Done** — `mcp_server.py`, `memory_api.py` | Claims no MCP; **stale** |
| Value gate (SKIP/PROCESS) | **Missing** — ingest always summarizes | Correct at time of writing |
| `_index.md` pipe-table routing | **Partial** — `classifier.py` + `wiki_retriever.py` expect `_index.md`; ingest writes `wiki/index.md` | Correct gap |
| Public cloud LLM client | **Partial** — `public_llm.py` uses **Ollama only**, not Anthropic/OpenAI | Correct naming gap |

## Decision

**Reconciled via codebase audit (2026-05-24).** [[claude-mem-weaver-competitive-analysis]] is largely **stale** on backend completeness. Trust [[claude-architecture-inspiration]] and [[chatgpt-mem-weaver-v2-roadmap]] for ingest/search/MCP/chat status.

**Remaining gaps vs design:** (1) value gate in ingest, (2) align `_index.md` format between ingest and chat retriever, (3) optional cloud LLM client if product requires hosted models.

Related: [[mem-weaver-architecture]], [[mem-weaver-known-gaps]], [[implementation-milestones]]
