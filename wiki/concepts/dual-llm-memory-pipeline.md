---
type: concept
sources:
  - claude-dual-llm-memory-pipeline
  - chatgpt-retrieval-vs-synthesis
  - gemini-llm-memory-research
  - claude-second-brain-prd
  - claude-second-brain-implementation
  - gemini-second-brain-design
  - claude-middleware-delegator-plan
  - chatgpt-mem-weaver-v2-roadmap
  - notebooklm-dual-llm-architecture-design
last_updated: 2026-05-29
---

# Dual-LLM Memory Pipeline

## Consensus

- **Two roles:** a local Ollama model compiles Q+A into wiki-style memory; a public cloud LLM (Claude/GPT) answers questions using distilled context, not raw chat history.
- **Phase A (sync):** classify topic → retrieve relevant wiki summary → inject into public LLM prompt → return answer.
- **Phase B (async):** after the user gets an answer, Ollama updates wiki pages in the background so turn latency equals public LLM only.
- **Core insight:** raw Q+A history is noisy; compiled wiki summaries are denser, more useful context than linear message replay.
- **Economic/privacy split:** Ollama is free/local and keeps raw conversations private; cloud LLM sees only distilled output.
- **Synthetic source framing:** Raw Q+A from LLMs is [[llm-outputs-as-synthetic-sources]] — useful first-pass signal, not ground truth. The wiki compilation (Phase B) is where verified knowledge emerges via contradiction tracking and human review.

- **Storage validated:** [[notebooklm-dual-llm-architecture-design]] independently recommends SQLite+FTS5 over ChromaDB for single-user setups — the same choice mem-weaver made — and provides cost quantification (80–90% token reduction via wiki context).
- **"Lost in the Middle" mitigation:** NotebookLM suggests limiting retrieved context to 1–3 focused wiki summaries, directly addressing a risk not discussed in other sources.

## Divergence

| Topic | [[claude-dual-llm-memory-pipeline]] | [[gemini-llm-memory-research]] | [[chatgpt-retrieval-vs-synthesis]] |
|-------|--------------------------------------|--------------------------------|-------------------------------------|
| Summary trigger | Batch 3–5 turns before update | Value gate + incremental merge | Per-turn summarization acceptable but costly |
| Topic buckets | Start with 5–8 fixed categories | Keyword scan of index first; Ollama fallback | Semantic search or tags for retrieval |
| Short-term buffer | Version summaries; optional batching | Keep last 3 raw messages alongside wiki | Limit to 2–3 most relevant memory entries |
| Public LLM in loop | Explicit in architecture | Explicit | Hybrid with trade-offs on summary quality |

## Decision

**As-built (mem-weaver):** per-turn async ingest on every Q+A (no batching, no value gate yet). **Target:** add Gemini-style value gate (`SKIP`/`PROCESS`) before summarize; optional batching for high-frequency sessions.

**Taxonomy:** coded `SKILL_TAXONOMY` in `classifier.py` (done); `_index.md` pipe-table routing partial — see [[agent-skills-taxonomy]].

Resolves batch-vs-per-turn tension: **ship per-turn async now; add gate + batching as optimizations.**

Related: [[memory-synthesis-vs-rag]], [[mem-weaver-architecture]], [[agent-skills-taxonomy]]
