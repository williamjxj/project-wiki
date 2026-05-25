---
type: concept
sources:
  - rag-graphrag-to-llm-knowledge-runtime
last_updated: 2026-05-25
---

# Knowledge Governance

## Consensus

- **Confidence:** Knowledge base entries need explicit uncertainty markers — indicating whether a claim is verified, synthesized, speculative, or known-stale. Prevents treating LLM output as ground truth.
- **Supersession:** Claims must be replaceable. When newer sources contradict or update older ones, the old claim should be marked superseded (not deleted), preserving audit trail.
- **Review Queue:** Newly ingested or auto-synthesized content that exceeds a certainty threshold should enter a review queue for human verification before being used as authoritative context.
- **Hallucination write-back risk:** The most dangerous failure mode in LLM Wiki — an LLM synthesizes incorrect information during ingestion, writes it to the wiki, and later retrieves its own incorrect output as context, creating a self-reinforcing error loop. This compounds over multiple cycles.

## Divergence

_(single source — no divergence identified yet)_

## Decision

_(pending — no cross-source comparison yet)_

Related: [[llm-wiki-paradigm]], [[memory-synthesis-vs-rag]]
