---
type: source-summary
raw: raw/llm/2026-05-12-chatgpt-mem-weaver-v2-roadmap.md
source: chatgpt
date: 2026-05-12
---

# mem-weaver v2 Roadmap

## Key Claims

- v1 Phase B pipeline strong; Phase A POST /chat is main missing link.
- P0: POST /chat + wire SKILL_TAXONOMY in code.
- P1: Next.js + WikiSidebar, wiki hierarchy folders, multi-article retrieval.
- Embedding + hybrid marked done (embedder.py, query_search.py, RRF tests).
- Product positioning: memory for AI coding agents vs generic second brain.
- MCP recommended as high ROI vs chat UI alone.

## Unique Insights

- File-level blueprint for /chat endpoint modules.

## Contradictions

Hybrid done vs [[claude-mem-weaver-competitive-analysis]] FTS5-only — [[mem-weaver-as-built-status]].

**Resolved (2026-05-24):** Hybrid search and POST /chat confirmed in mem-weaver repo. Competitive-analysis claims superseded. See [[mem-weaver-as-built-status]].

Related concepts: [[mem-weaver-architecture]] [[mem-weaver-as-built-status]] [[implementation-milestones]]
