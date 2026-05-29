---
type: concept
sources: [chatgpt-llm-based-project-workflow, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-29
---

# Wiki vs Context Engine

## Consensus

Both ChatGPT and Claude validate the core Karpathy pattern but frame it differently. ChatGPT argues the system should NOT be called a "wiki" (too static/manual) and prefers "Canonical Context Engine" or "Project Intelligence Layer." Claude keeps the "wiki" framing and provides operational detail on how the LLM maintains it.

## Divergence

| Aspect | ChatGPT | Claude |
|--------|---------|--------|
| Naming | "Context Engine" — wiki implies static human-edited | "Wiki" — the LLM maintains it, you browse |
| Tone | Product-oriented (commercially viable, Perplexity+Notion comparison) | Engineering-oriented (operational details, lint rhythm, tool recommendations) |
| Focus | Vision — context compression as moat, context packs as killer feature | Operations — contradictions tracking, human review gate, decision records |

## Decision

Adopt "LLM-Wiki" as the architectural pattern name (Karpathy's original). The product distinction ("Context Engine") is acknowledged but kept as future product positioning — the current implementation is a markdown wiki maintained by an LLM.
