---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Semantic Deduplication

## Consensus

Multi-LLM outputs are heavily repetitive (~80% overlap per ChatGPT). Dedup is critical to avoid context pollution and agent confusion.

## Divergence

| Source | Dedup mechanism |
|--------|----------------|
| ChatGPT | Embedding clustering, semantic overlap, contradiction detection, novelty scoring |
| Gemini | [[two-stage-ingestion]] Stage 1 analysis; PageIndex tree indexing for long docs |
| Claude | [[contradictions-tracking]] + lint passes; explicit UNRESOLVED flags |

## Decision

**Lean: combine approaches.** LLM-based two-stage analysis for ingest (Gemini/Claude); add embedding clustering at scale (ChatGPT); lint for contradictions (Claude). Not mutually exclusive.
