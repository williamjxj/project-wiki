---
type: concept
sources: [chatgpt-llm-based-project-workflow, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-29
---

# Decision Records

## Consensus

Both sources agree that persisting structured decisions is critical — not just notes. Decision records should capture: rationale, tradeoffs, and confidence.

**ChatGPT** emphasizes the value for agentic coding: "decision + rationale + confidence + tradeoffs" creates gold for coding agents.

**Claude** adds that source attribution is essential — you need to know which LLM suggested it, what the runner-up was, and why the choice was made. This helps track which model produced which recommendations and enables better contradiction resolution.

## Divergence

| Aspect | ChatGPT | Claude |
|--------|---------|--------|
| Structure | decision + rationale + confidence + tradeoffs | Adds source attribution and runner-up |
| Purpose | Canonical context for coding agents | Track provenance for accountability |
| Format | YAML block example | Implicit, mentions "confidence levels" |

## Decision

Decision records should include: decision, rationale, confidence, source attribution, runner-up (with rationale), and tradeoffs. Combine both perspectives.
