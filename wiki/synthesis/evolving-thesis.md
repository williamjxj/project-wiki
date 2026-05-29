---
type: synthesis
status: evolving
last_updated: 2026-05-29
sources_ingested: 28
---

# Evolving Thesis

> Running synthesis across all ingested sources. Updated after every ingest.

## Current Understanding

**mem-weaver** is a local-first **dual-LLM memory system** for a MacBook Pro "second brain": a local Ollama model compiles Q+A exchanges into a persistent, searchable **LLM-wiki** (Karpathy pattern) organized with **Agent Skills** taxonomy ([[agent-skills-taxonomy]]), while chat answers use compiled wiki context instead of raw history.

### Core loop ([[dual-llm-memory-pipeline]])

1. **Phase A (sync):** User asks Q → delegator classifies topic → retrieves compiled wiki summary Sₖ → LLM answers with Sₖ as context (not raw history).
2. **Phase B (async):** After answer returns, Ollama incrementally merges Q+A into wiki pages — user never waits on local LLM.

This follows [[memory-synthesis-vs-rag]]: synthesis-first compilation plus hybrid retrieval (FTS5 + sqlite-vec + RRF) at query time.

### Architecture ([[mem-weaver-architecture]])

- **FastAPI middleware delegator:** `POST /ingest`, `GET /query`, `POST /chat` (SSE), MCP stdio — **implemented** in parent repo.
- **Storage triad:** SQLite + Markdown vault + sqlite-vec embeddings. [[notebooklm-dual-llm-architecture-design]] validates the SQLite+FTS5-first choice over standalone vector DBs for single-user setups.
- **Entry points:** Next.js chat UI ([[claude-chat-app-frontend-design]]) and MCP ([[claude-mcp-server-design]]) share `memory_api`.

### Implementation progress ([[implementation-milestones]])

Milestones A/B, Phase 4 hardening, hybrid search, `/chat`, and MCP are **done** per [[mem-weaver-as-built-status]] codebase audit (2026-05-24). [[claude-mem-weaver-competitive-analysis]] is stale on backend completeness.

### LLM Wiki paradigm ([[llm-wiki-paradigm]], [[knowledge-governance]])

The LLM Wiki paradigm (from [[rag-graphrag-to-llm-knowledge-runtime]]) reframes the project: what mem-weaver implements is a **knowledge runtime** — a persistent middleware layer between raw data and LLM reasoning. Key insights:

- **Synthesis shifts to ingestion phase:** Each ingest permanently improves the knowledge asset, rather than starting from scratch per query (RAG pattern). This aligns with mem-weaver's Phase B (async) compilation.
- **Three-layer architecture** mirrors this very wiki: Raw Sources → Wiki (source + concept pages) → Schema (frontmatter, governance metadata).
- **Knowledge governance gaps:** The video identifies confidence markers, supersession, and review queues as essential for long-term health. mem-weaver lacks all three — a critical gap as the wiki accumulates auto-synthesized claims.
- **Hallucination write-back** is the critical risk: LLM-written wiki content that later gets retrieved as context creates a self-reinforcing error loop. This compounds over multiple ingest cycles.

### Multi-LLM research workflow ([[chatgpt-llm-based-project-workflow]], [[claude-multi-llm-research-synthesis-workflow]], [[gemini-llm-wiki-multi-agent]])

Three independent LLM analyses converge on a shared workflow that this wiki embodies:
- **Collect → Ingest → Synthesize → Export → Apply** — iterating per the [[claude-multi-llm-research-synthesis-workflow]] six-step loop. The wiki is the intermediate layer between multi-LLM research and implementation.
- **[[context-fragmentation]]** is the root problem: scattered, contradictory research across chats and docs. [[context-compression]] (10k pages → 20 → 2 → prompts) is the moat.
- **[[compounding-knowledge-layer]]:** The wiki is not a static dump — each ingest compounds previous knowledge, making the asset more valuable over time ([[gemini-llm-wiki-multi-agent]]).
- **[[multi-pass-distillation]]:** Raw → clustered → summarized → canonicalized → implementation-oriented — do not go raw to final in one pass ([[chatgpt-llm-based-project-workflow]]).
- **[[semantic-deduplication]]:** ~80% of LLM outputs are repetitive but differently phrased; deduplication is the critical processing stage ([[chatgpt-llm-based-project-workflow]]).
- **[[wiki-vs-context-engine]]:** ChatGPT argues against static "wiki" framing in favor of a live "context engine" — resolved as a 2:1 lean toward the LLM-Wiki (compiling) pattern.
- **[[llm-outputs-as-synthetic-sources]]:** LLM chat exports are first-pass synthetic knowledge, not ground truth — wiki distillation is where verified signal emerges ([[claude-multi-llm-research-synthesis-workflow]]).
- **[[decision-records]]:** Store (decision + rationale + confidence + tradeoffs), not undifferentiated notes — this is what makes wiki output useful for agentic coding ([[chatgpt-llm-based-project-workflow]]).
- **[[purpose-steering]]:** `purpose.md` alongside `schema.md` prevents knowledge graph drift — schema tells *how* to build, purpose tells *why* ([[gemini-llm-wiki-multi-agent]]).
- **[[context-packs]]** are the export vehicle — scoped, compressed context bundles per feature, not raw wiki dumps ([[claude-multi-llm-research-synthesis-workflow]]).
- **[[contradictions-tracking]]** is where multi-LLM input earns its keep — explicit `UNRESOLVED` status before dev starts.
- **[[human-review-gate]]** is non-negotiable between wiki and implementation — never feed unreviewed synthesis to a code agent.
- **[[two-stage-ingestion]]**: structural analysis → then generation and linkage (avoids single-pass failures on long transcripts, per [[gemini-llm-wiki-multi-agent]]).
- **[[closed-loop-harvesting]]**: dev session logs from Cursor/Claude Code re-enter the wiki, keeping it evergreen ([[gemini-llm-wiki-multi-agent]]).

### Pipeline operator ([[pipeline-operator]]) and scope ([[mvp-scope]])

The [[2026-05-25-cluade-pipeline-plan]] proposes a shared pipeline core (Python) that Web UI, automation, and MCP all attach to — independent of the specific UI framework (Open WebUI Pipelines vs custom FastAPI). The as-built [[research-to-implementation-pipeline]] ships wiki_core → CLI/API → UI → MCP sidecar.

**Scope boundary:** [[mvp-scope]] defines the project as markdown + git + manual skills; the pipeline operator (FastAPI or Open WebUI) is an **optional acceleration layer** for v2, not a replacement for AGENTS.md authority. The ultimate success criterion is [[implementation-readiness]]: "Can Cursor implement this correctly?" ([[chatgpt-llm-based-project-workflow]]).

### Known gaps ([[mem-weaver-known-gaps]])

- No value gate (`SKIP`/`PROCESS`) in ingest pipeline
- `_index.md` pipe-table vs `wiki/index.md` catalog mismatch blocks chat retrieval
- No explicit episodic/semantic/procedural memory taxonomy
- Flat wikilink graph; no temporal validity; no multi-tenant scoping
- `public_llm.py` uses Ollama only — no hosted Anthropic/OpenAI client yet

## Open Questions

1. **Index format:** Unify ingest output on `_index.md` pipe-table or retarget chat retriever to `wiki/index.md` + hybrid search?
2. **Entry point priority:** Ship Next.js chat UI next, or focus on MCP polish for Cursor/IDE workflow?
3. **Cloud LLM:** Add Anthropic/OpenAI client to `public_llm.py` or keep Ollama-only for local-first?
4. **Vector store at scale:** sqlite-vec sufficient or migrate to external store (ChromaDB per [[gemini-second-brain-design]])?
5. **Product scope:** Solo dev / Obsidian tool vs broader SaaS — affects auth and scoping.
6. **Hallucination write-back:** How to detect/prevent LLM-written wiki content that self-reinforces errors over multiple ingest cycles? ([[knowledge-governance]])

## Emerging Decisions

| Decision | Status | Basis |
|----------|--------|-------|
| Dual-LLM synthesis over raw history replay | **Decided** | All v1 sources + PRD; per-turn async ingest in codebase |
| Hybrid wiki compile + search retrieval | **Decided** | Implemented: FTS5 + sqlite-vec + RRF |
| SKILL_TAXONOMY in classifier | **Decided** | Wired in code; index file format gap remains |
| Obsidian for wiki editing | **Leaning yes** | [[claude-frontend-admin-integration]] |
| MCP + shared memory_api | **Decided** | Both implemented |
| OSS/local-first; skip VC memory startup | **Leaning yes** | [[claude-mem-weaver-competitive-analysis]] |
| Value gate before summarize | **Next build** | [[mem-weaver-known-gaps]], [[dual-llm-memory-pipeline]] |
| As-built feature snapshot | **Resolved** | [[mem-weaver-as-built-status]] audit 2026-05-24 |
| Knowledge governance (confidence, supersession, review queue) | **Open challenge** | [[knowledge-governance]] — LLM Wiki paradigm identifies these as essential for auto-synthesized wikis; not yet designed |
| Hallucination write-back detection | **Needs research** | [[knowledge-governance]] — critical risk for LLM-compiled wikis; no prevention mechanism exists |
