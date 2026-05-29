---
type: concept
sources: [claude-multi-llm-research-synthesis-workflow, 2026-05-26-claude-distill-canonical, 2026-05-27-claude-04-summary]
last_updated: 2026-05-29
---

# Research to Implementation Pipeline

## Consensus

The unified pipeline spans multi-LLM collection → wiki distillation → dev context packaging → coding tools. Key refinements:

**When to multi-source**: only for complex, architectural, or long-lived topics. Simple one-off questions don't benefit from triangulation. Different LLMs have genuinely different knowledge distributions — Claude reasons better, GPT-4 has broader coverage, Gemini is stronger on code details.

**Core discipline**: Never paste raw chat logs into coding tools. Always Collect → Distill → One canonical file → Ingest first.

**Complementary pattern — Karpathy autoresearch**: a related loop that automates the research phase itself: pick niche → design tiny loop → run experiments → measure → productize. The autoresearch loop generates the research; the llm-wiki pattern structures and distills it.

## Divergence

_(Single comparison — both sources from Claude, consistent.)_

## Decision

The pipeline is confirmed. Add a decision gate: before multi-source collection, evaluate whether the topic warrants the investment (complex/architectural/long-lived = yes; simple one-off = no).
