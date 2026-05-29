---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent]
last_updated: 2026-05-29
---

# Semantic Deduplication

## Consensus

ChatGPT identifies semantic deduplication as the most important pipeline stage — ~80% of LLM output is repetitive but phrased differently.

Gemini approaches deduplication through the **two-stage compiler** pattern: Stage 1 analysis maps conceptual entities and identifies overlaps before any files are written. This structural analysis serves as the dedup gate — overlapping claims are detected and consolidated in the blueprint before generation occurs.

Both sources agree deduplication must happen before content is written to the wiki.

## Divergence

| Aspect | ChatGPT | Gemini |
|--------|---------|--------|
| Mechanism | Embedding clustering (OpenAI/VoyageAI/BGE) | Structural analysis in Stage 1 of two-stage ingestion |
| When | During pipeline processing | During Stage 1 (analysis) before Stage 2 (generation) |
| Granularity | Semantic similarity scoring | Entity and claim overlap detection |

## Decision

Combine both approaches. Use Gemini's two-stage ingestion structure (analysis → generation) as the pipeline architecture, with ChatGPT's embedding-based semantic similarity scoring as the dedup mechanism within Stage 1 analysis.
