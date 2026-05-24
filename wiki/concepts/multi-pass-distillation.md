---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Multi-Pass Distillation

## Consensus

Do not go raw → final in one step ([[chatgpt-llm-based-project-workflow]]). Use progressive refinement:

```
raw → clustered → summarized → canonicalized → implementation-oriented
```

Each pass reduces noise and increases actionability. Works with [[semantic-deduplication]] at the clustering stage and [[decision-records]] at the canonicalization stage.

Gemini implements this via [[two-stage-ingestion]] (analyze → write). Claude's ingest-one-at-a-time + lint rhythm is a manual multi-pass. ChatGPT names five explicit distillation stages.

## Divergence

| Source | View |
|--------|------|
| ChatGPT | Five-stage pipeline: raw → clustered → summarized → canonicalized → implementation-oriented |
| Gemini | Two-stage ingest compiler; multi-pass at wiki compilation layer |
| Claude | One source per ingest + lint every 3–5 ingests as quality passes |

## Decision

**Lean: ChatGPT's five-stage model as the conceptual frame; Gemini's [[two-stage-ingestion]] as the operational ingest implementation; Claude's lint cadence as the quality gate between passes.**
