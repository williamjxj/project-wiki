---
type: source-summary
raw: raw/llm/2026-04-21-notebooklm-dual-llm-architecture-design.md
source: notebooklm
date: 2026-04-21
---

# NotebookLM Dual-LLM Architecture Design

> NotebookLM's comprehensive design for a Second Brain + Memory system on MacBook Pro. Proposes a dual-LLM pipeline with public reasoning engine (Claude/GPT), local Ollama compiler, FastAPI delegator, and markdown wiki store.

## Key Claims

- **Dual-LLM architecture:** Public LLM as reasoning engine + local Ollama as background memory compiler, with FastAPI delegator orchestrating both.
- **Three implementation phases:** Phase 1 (core pipeline — `/ingest`, Ollama summarizer, markdown writer) → Phase 2 (retrieval — `/query`, ChromaDB or SQLite+FTS5, prompt templates) → Phase 3 (hardening — contradiction detection, re-summarization, Obsidian compat, dashboard).
- **80-90% token cost reduction** by replacing raw chat history (~10k+ tokens) with wiki summaries (~1-2k tokens).
- **SQLite+FTS5 as ChromaDB alternative:** Recommends SQLite with FTS5 for single-user MacBook setups to avoid Vector DB operational overhead.
- **"Lost in the Middle" mitigation:** Using 1-3 highly relevant wiki summaries (instead of 10+ retrieved chunks) reduces the risk of context being ignored.
- **Git-based data versioning:** The wiki directory as a Git repo enables change tracking, rollback of bad summaries, and branch experimentation.

## Unique Insights

- Only source that explicitly recommends SQLite+FTS5 over ChromaDB for single-user setups — aligns with mem-weaver's actual implementation choice.
- Provides cost quantification (80-90% token savings) not found in other sources.
- "Lost in the Middle" problem framing for the wiki summary retrieval design.
- Git-based wiki versioning as a core architectural property rather than an afterthought.
- 3-phase roadmap from NotebookLM's perspective, independently converging on the same phases the project actually followed.

## Contradictions

- None significant. Strongly aligned with [[claude-dual-llm-memory-pipeline]], [[gemini-second-brain-design]], and [[claude-middleware-delegator-plan]] on the dual-LLM architecture pattern.

## Related

- [[dual-llm-memory-pipeline]] — core pipeline architecture (notebooklm validates the same design)
- [[mem-weaver-architecture]] — aligns on FastAPI delegator, storage triad, and phased roadmap
- [[agent-skills-taxonomy]] — mentions Agent Skills layer for categorization
