---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Implementation Readiness

## Consensus

The success criterion for the entire system ([[chatgpt-llm-based-project-workflow]]):

> Can Cursor (or equivalent agentic coding tool) implement this correctly?

All 3 sources agree: optimize for implementation readiness, not knowledge browsing.

- ChatGPT: explicit north-star metric; drives [[context-packs]] and [[context-compression]]
- Gemini: "Can coding agents implement correctly?" via pre-compiled verified technical reference
- Claude: dev context package with constraints → decisions → acceptance criteria → tasks

Drives output format: PRDs, ADRs, tech stack, constraints, implementation plans, and [[context-packs]] rather than encyclopedic wiki pages.

## Divergence

| Source | View |
|--------|------|
| ChatGPT | Names "implementation readiness" explicitly as the moat |
| Gemini | Implied via standardized exports and MCP-mounted compiled wiki |
| Claude | Implied via Phase 3 dev context package structure |

## Decision

**Confirmed north-star across all 3 sources.** [[implementation-readiness]] is the primary success metric.
