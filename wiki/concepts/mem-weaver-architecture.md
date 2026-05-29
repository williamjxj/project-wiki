---
type: concept
sources:
  - claude-middleware-delegator-plan
  - claude-second-brain-implementation
  - claude-architecture-inspiration
  - chatgpt-mem-weaver-v2-roadmap
  - notebooklm-dual-llm-architecture-design
last_updated: 2026-05-29
---

# mem-weaver Architecture

## Consensus

- **Middleware delegator:** FastAPI daemon between any LLM client and wiki store — `POST /ingest` (202 async), `GET /query` (FTS5 BM25), `GET /health`.
- **Storage triad:** SQLite (pages, qa_pairs, wiki_links, FTS5) + Markdown vault (Obsidian-compatible) + optional embeddings (sqlite-vec).
- **Ingest pipeline:** validate → Ollama summarize → write raw → generate/update wiki page → index SQLite → update index.md + log.md. Inputs are [[llm-outputs-as-synthetic-sources]] — treated as first-pass knowledge, not authoritative, until distilled through contradiction checks.
- **Query pipeline:** tokenize → FTS5/hybrid search → return ranked snippets (no LLM by default; optional `?summarize=true`).
- **Two product shapes in docs:** middleware API (`/ingest`, `/query`) largely built; second-brain chat loop (`POST /chat`) designed but was the main v2 gap.

- **Phased roadmap alignment:** [[notebooklm-dual-llm-architecture-design]] proposes a 3-phase build (Core Pipeline → Retrieval & Integration → Hardening) that independently converges on the same progression as mem-weaver's actual Milestone A / Milestone B / Phase 4, from a different AI's architectural analysis.
- **Storage choice rationale:** NotebookLM's explicit SQLite+FTS5 vs ChromaDB tradeoff analysis retrospectively validates the project's no-Vector-DB choice for a single-user MacBook setup.

## Divergence

| Aspect | [[claude-middleware-delegator-plan]] | [[claude-second-brain-implementation]] | [[claude-architecture-inspiration]] |
|--------|--------------------------------------|----------------------------------------|-------------------------------------|
| Primary entry | Generic Q+A JSON from any client | Next.js chat + WikiSidebar | Merge both: add `/chat`, keep `/ingest` |
| Wiki layout | `wiki/concepts/<slug>.md` | Tiered folders + `_index.md` routing | Karpathy folders: sources/, concepts/, synthesis/ |
| Vector search | Phase 4+ in plan | Phase 4 marked done (sqlite-vec) | Hybrid RRF recommended at scale |

## Decision

**Target architecture:** Karpathy compilation + SQLite indexing + hybrid search + `POST /chat` feedback loop — **largely implemented** per [[mem-weaver-as-built-status]]. Remaining wiring: value gate, `_index.md` format alignment.

Related: [[implementation-milestones]], [[mem-weaver-as-built-status]], [[dual-llm-memory-pipeline]], [[agent-skills-taxonomy]], [[llm-wiki-paradigm]]
