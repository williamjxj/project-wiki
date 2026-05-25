---
type: source-summary
raw: raw/web/rag-graphrag-to-llm-knowledge-runtime.md
source: web
date: 2026-05-25
---

# LLM Wiki 深度解析：从 RAG、GraphRAG 到大模型知识运行时

> YouTube 视频 by TGLTommy (2026-04-30). Systematically explains LLM Wiki as a paradigm that shifts knowledge synthesis from query phase to ingestion phase.

## Key Claims

- **LLM Wiki is not a RAG variant** — it fundamentally shifts knowledge synthesis from "query phase" to "ingestion phase". Each ingest/query/research cycle becomes an incremental investment in a long-term knowledge asset.
- **Three-layer architecture:** Raw Sources (immutable original data) → Wiki (curated, cross-linked summaries) → Schema (type-safe frontmatter + governance metadata)
- **Complete workflow:** Ingest → Query → Save → Lint → Research — a closed loop for iterative knowledge building.
- **Long-term governance requires:** Confidence (uncertainty markers), Supersession (replace stale claims), Review Queue (flagging new claims for human audit).
- **Critical risk:** Hallucination write-back — LLM summarizing incorrectly into the wiki, then using that incorrect summary in future queries, creating a self-reinforcing error loop.

## Unique Insights

- Positions LLM Wiki as the "knowledge runtime" — a persistent, self-maintaining layer between raw data and LLM reasoning, analogous to how an operating system manages memory between hardware and applications.
- Explicitly contrasts LLM Wiki with RAG (query-time retrieval of raw chunks), GraphRAG (entity-relation graph queries), and AI note tools (web UI, no structured ingestion pipeline).
- Frames "save" as a first-class workflow step (not just write-to-disk) — intentional commit of synthesized knowledge after human or automated review.
- Identifies error self-reinforcement as the critical failure mode: incorrect LLM output → written to wiki → retrieved as context → biases future LLM output.

## Contradictions

- _(single source — no contradictions identified yet)_
