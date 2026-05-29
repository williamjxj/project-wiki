---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, distill-ingest]
last_updated: 2026-05-29
---

# Context Fragmentation

## Consensus

All three sources independently confirm context fragmentation as the core engineering problem — though each frames it differently:

- **ChatGPT** states it most directly: "The biggest problem today is NOT coding. It is context fragmentation." Engineers collect scattered, duplicated, contradictory information from multiple LLMs with no canonical source of truth, leading to agent confusion and degraded implementation quality.
- **Gemini** frames it as the transition from "stateless prompt-response loops to stateful, compounding knowledge architectures" — the implicit acknowledgment that isolated LLM sessions produce fragmented context by design.
- **distill-ingest** operationalizes the response: the 5-signal filter (Specificity, Actionability, Non-obviousness, Consensus, Contradiction) exists specifically to reject content that contributes to fragmentation — idle summaries, generic advice, and confirmatory filler.

**Convergent evidence:** Four of the 5-signal filter criteria directly counter fragmentation effects. The compounding-knowledge-layer concept exists specifically as the anti-fragmentation structure. Every other concept page in the wiki (18 total) implicitly depends on solving this problem first.

## Divergence

| Aspect | ChatGPT | Gemini | distill-ingest |
|--------|---------|--------|----------------|
| Framing | Direct problem statement — "biggest problem today" | Framed as architectural transition | Implicit — anti-patterns to filter out |
| Proposed solution | Context compression pipeline | Stateful compounding architecture | 5-signal filter as first line of defense |
| Emphasis | Vision/moat argument | Architectural transformation | Concrete methodology |

## Decision

Context fragmentation is confirmed as the foundational problem by multi-source consensus. The solution has three layers: (1) 5-signal filter at collection time (distill-ingest), (2) compounding knowledge layer for persistent structure (Gemini), (3) context compression for delivery (ChatGPT). All three are required — none alone is sufficient.
