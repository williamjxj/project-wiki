---
type: source-summary
raw: raw/llm/2026-04-21-claude-dual-llm-memory-pipeline.md
source: claude
date: 2026-04-21
---

# Dual-LLM Memory Pipeline (Claude)

## Key Claims

- Dual-LLM split: Ollama = private memory manager; cloud LLM = reasoning engine receiving distilled wiki context.
- Architecture is local RAG where documents are LLM-generated conversation summaries organized by topic.
- Batch wiki updates (3–5 turns) preferred over per-turn regeneration to avoid latency.
- Topic classification via keywords, embeddings, or Ollama classify step.
- Start with file-based store (one markdown per topic); migrate to SQLite/vectors later.
- Separate read latency from write: return public LLM answer first, update wiki async.
- Use 5–8 fixed topic buckets initially; version summaries before overwrite.

## Unique Insights

- Mirrors how experts maintain mental models rather than re-reading every email.
- Priming pattern: inject summary as synthetic user/assistant exchange before new question.

## Contradictions

None within single source; see [[dual-llm-memory-pipeline]] for cross-source batch vs per-turn divergence.

## Related sources

[[chatgpt-retrieval-vs-synthesis]], [[gemini-llm-memory-research]], [[chatgpt-api-token-context-management]], [[claude-second-brain-prd]]

Related concepts: [[dual-llm-memory-pipeline]] [[memory-synthesis-vs-rag]]
