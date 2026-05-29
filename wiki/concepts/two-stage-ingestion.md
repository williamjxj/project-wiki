---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Two-Stage Ingestion

## Consensus

Ingestion must separate analysis from file generation ([[gemini-llm-wiki-multi-agent]]):

| Stage | Role | Input | Output |
|-------|------|-------|--------|
| **Stage 1: Structural Analysis** | Analytical reviewer | Raw transcripts, existing wiki, [[purpose-steering]] (`purpose.md`) | Conceptual maps, detected conflicts, recommended edits — **no file writes** |
| **Stage 2: Generation & Integration** | Technical writer | Stage 1 blueprint + `schema.md` | New/updated concept pages, bidirectional links, index/log updates |

Single-pass prompts fail on multi-megabyte transcripts. Aligns with [[multi-pass-distillation]] — specifically the ingest write path.

Claude's workflow mirrors this: discuss takeaways (Stage 1) → write wiki pages (Stage 2) → human confirm. ChatGPT's embedding dedup maps to Stage 1 analysis.

## Divergence

| Source | View |
|--------|------|
| Gemini | Two explicit LLM stages: analyze blueprint first, then write files |
| Claude | Discuss before writing + human confirm before marking ingested |
| ChatGPT | Embedding clustering + contradiction detection as automated Stage 1 |

## Decision

**Adopt two-stage ingest.** Stage 1 = analysis + dedup + [[contradictions-tracking]]; Stage 2 = wiki writes. Add embedding clustering post-MVP for scale (ChatGPT).
