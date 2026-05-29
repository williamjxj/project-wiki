---
type: concept
sources: [chatgpt-llm-based-project-workflow, doubao]
last_updated: 2026-05-29
---

# Context Compression

## Consensus

Context compression operates at two levels:

**Research pipeline level** (ChatGPT): multi-tier compression from raw research to implementation prompts — 10,000 pages → 20 pages → 2 pages. This is the competitive moat for AI-assisted engineering.

**API call level** (doubao): token/memory management strategies for LLM API calls:
- **Sliding window**: keep only last N turns, discard oldest
- **Token hard truncation**: trim from head when threshold exceeded
- **Dialogue summarization**: compress old multi-turn conversations into summaries
- **Key information extraction**: retain core rules/persona, discard chit-chat
- **System prompt persistence**: keep fixed system, trim only dynamic history

**Memory architecture**: short-term memory (recent raw conversation) + long-term memory (DB/vector store) + RAG retrieval + consolidation/forgetting (periodic archive of old, prune low-frequency).

## Divergence

| Aspect | ChatGPT | Doubao |
|--------|---------|--------|
| Level | Research pipeline (pages → prompts) | API call (token/memory management) |
| Mechanism | Multi-tier distillation | Sliding window, summarization, truncation |
| Goal | Implementation readiness for coding agents | Token cost control for API calls |

## Decision

Both levels are complementary. The research pipeline level compresses raw knowledge into implementation context. The API call level manages how that context is fed to the LLM at runtime. Both are needed for a complete system.
