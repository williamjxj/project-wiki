---
type: concept
sources:
  - rag-graphrag-to-llm-knowledge-runtime
last_updated: 2026-05-25
---

# LLM Wiki Paradigm

## Consensus

- **Core shift:** LLM Wiki moves knowledge synthesis from query phase (RAG) to ingestion phase. Instead of retrieving raw chunks per query, the LLM incrementally compiles and maintains a persistent wiki — each ingest improves the knowledge asset permanently.
- **Three-layer architecture:**
  - **Raw Sources** — immutable originals (chat exports, web clips, documents)
  - **Wiki** — curated, cross-linked summaries organized as source pages + concept pages
  - **Schema** — type-safe frontmatter, governance metadata (confidence, supersession, status)
- **Workflow loop:** Ingest → Query → Save → Lint → Research — closed loop where each step feeds the next. "Save" is an intentional commit (not automatic write).
- **Knowledge Runtime framing:** LLM Wiki acts as a persistent middleware layer between raw data and LLM reasoning — analogous to an OS managing memory between hardware and applications.
- **Contrast with alternatives:**
  - **RAG:** Query-time retrieval of raw chunks — good for large corpora, no persistent synthesis
  - **GraphRAG:** Entity-relation graph queries — structured but complex, no prose synthesis
  - **AI note tools:** Web UI with flat notes — no structured ingestion pipeline or governance

## Divergence

_(single source — no divergence identified yet)_

## Decision

_(pending — no cross-source comparison yet)_

Related: [[memory-synthesis-vs-rag]], [[knowledge-governance]], [[mem-weaver-architecture]]
