---
type: concept
sources: [chatgpt-llm-based-project-workflow, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Decision Records

## Consensus

Store **decisions**, not just notes. Structured records make knowledge actionable for agentic coding.

Required fields (merged from sources):

```yaml
decision: Use Next.js App Router
why: Better RSC support; AI ecosystem alignment
tradeoffs: More complexity; fast-moving ecosystem
confidence: high
source: claude                    # Claude addition
runner_up: Remix                  # Claude addition
status: current | superseded      # Gemini addition via supersession
```

Claude's critical addition: **source attribution** (which LLM suggested it) and **runner-up alternative** — makes dev context defensible.

Gemini adds: decay-weighted confidence and [[compounding-knowledge-layer]] systematic supersession.

Related outputs: ADRs, `decisions.md`, tech stack docs, constraints, implementation plans.

## Divergence

| Source | Emphasis |
|--------|----------|
| ChatGPT | YAML decision objects as storage primitive |
| Claude | Source attribution + runner-up for engineering defensibility |
| Gemini | Decay-weighted confidence + supersession lifecycle |

## Decision

**Lean: adopt all three extensions** — decision + rationale + confidence + source + runner-up + supersession status.
