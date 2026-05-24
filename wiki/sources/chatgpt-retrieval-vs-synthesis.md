---
type: source-summary
raw: raw/llm/2026-04-21-chatgpt-retrieval-vs-synthesis.md
source: chatgpt
date: 2026-04-21
---

# LLM Memory: Retrieval vs Synthesis (ChatGPT)

## Key Claims

- Two camps: vector/RAG retrieval vs LLM-driven summarization/wiki (Karpathy pattern).
- Public APIs (OpenAI, Anthropic) have no native long-term memory — persistence must be engineered.
- Claude Memory Tool stores info via client-side file directory read/write.
- Hybrid pipeline: public LLM answers; local Ollama summarizes Q+A into S₁; next query injects S₁ not raw history.
- Trade-offs: summary quality vs token savings; dual-call latency; privacy partial (summaries still go to cloud).
- Memory store grows — needs lint/prune like Karpathy wiki to avoid contradictions.
- Implementation: Ollama Anthropic-compatible API for summarization; public API with memory as system message.

## Unique Insights

- User's design follows Karpathy, Hindsight, MemGPT patterns but hacked on generic public API.
- Limit memory to 2–3 most relevant entries to manage token budget.

## Contradictions

Emphasizes per-turn summarization loop; [[claude-dual-llm-memory-pipeline]] recommends batching — flagged in [[dual-llm-memory-pipeline]].

**Resolved:** Per-turn vs batch reconciled in [[dual-llm-memory-pipeline]] — ship per-turn async; add value gate later.

## Related sources

[[claude-dual-llm-memory-pipeline]], [[gemini-llm-memory-research]], [[chatgpt-api-token-context-management]]

Related concepts: [[memory-synthesis-vs-rag]] [[dual-llm-memory-pipeline]]
