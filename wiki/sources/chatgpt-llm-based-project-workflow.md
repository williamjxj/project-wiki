---
type: source-summary
raw: raw/llm/2026-05-24-chatgpt-llm-based-project-workflow.md
source: chatgpt
date: 2026-05-24
---

# ChatGPT: LLM-Based Project Workflow

## Key Claims

1. **Context fragmentation is the real problem** — not coding ability. Engineers have scattered, duplicated, contradictory outputs from ChatGPT, Claude, Gemini, Reddit, docs, PDFs, and notes, with no canonical source of truth.
2. **Semantic deduplication is the most critical pipeline stage** — ~80% of LLM output is repetitive but phrased differently. Without dedup, context windows are polluted, agents confused, implementation quality degraded.
3. **Store decisions, not notes** — the system should persist decision + rationale + confidence + tradeoffs. This is far more valuable for agentic coding than traditional note-taking.
4. **Context compression is the real competitive moat** — future winners are not better models but better context engineering: 10,000 pages → 20 pages → 2 pages → implementation prompts.
5. **Multi-pass distillation is essential** — raw → clustered → summarized → canonicalized → implementation-oriented, not raw → final in one step.
6. **Implementation readiness is the north star** — every output should answer "Can Cursor implement this correctly?"

## Unique Insights

- The system should be called a "Canonical Context Engine" or "Project Intelligence Layer" rather than a "wiki", which implies static human-edited content.
- A "Context Packs" feature could be the killer app: per-module optimized bundles (arch + APIs + DB schema + constraints + coding conventions + implementation order) generated on demand for coding agents.
- The long-term vision is an "AI-native software engineering memory system" where every discussion, decision, implementation, bug, and PR continuously improves project intelligence.
- Suggests avoiding UI-first development — start with pipeline quality and CLI; UI is post-MVP.
- Identifies the product gap: AI coding tools lack durable memory and canonical project understanding. The proposed system = Perplexity + Notion + Cursor Memory + Deep Research + ADR system for engineering.

## Contradictions

- ChatGPT argues the system should NOT be called a "wiki" (too static/manual), preferring "Context Engine" — this is a naming tension resolved in [[wiki-vs-context-engine]] by keeping "LLM-Wiki" as the architectural pattern name while acknowledging the product distinction.
