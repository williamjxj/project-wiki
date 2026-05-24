---
type: concept
sources: [gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow, chatgpt-llm-based-project-workflow]
last_updated: 2026-05-24
---

# Compounding Knowledge Layer

## Consensus

The LLM-Wiki is a **persistent, compounding artifact** — not ephemeral RAG. All three sources agree this is the core value proposition.

| Ephemeral RAG | Compiling LLM-Wiki |
|---------------|-------------------|
| Re-discovers docs every query | Knowledge persists and accumulates |
| No analytical progress retained | Contradictions flagged, cross-refs built |
| Token overhead on repeat processing | Pre-compiled baseline for dev agents |
| Static flat summaries | Dynamic graph where new info refines/updates existing concepts |

Lifecycle management (Gemini): decay-weighted confidence, systematic supersession, typed entity graph.

Operational rhythm (Claude): ingest one-at-a-time, lint every 3–5 ingests, query → file back.

Epistemic framing (Claude): treat LLM outputs as [[llm-outputs-as-synthetic-sources]] — wiki distillation is where truth emerges.

## Divergence

| Source | View |
|--------|------|
| Gemini + Claude | Embrace "LLM-Wiki" as compiled intermediate layer |
| ChatGPT | Same architecture, different product name ([[wiki-vs-context-engine]]) |

## Decision

**Lean: LLM-Wiki as compounding knowledge layer.** Resolved — this is the architectural center.
