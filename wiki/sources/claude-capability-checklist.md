---
type: source-summary
raw: raw/llm/2026-05-15-claude-capability-checklist.md
source: claude
date: 2026-05-15
---

# Memory Capability Checklist

## Key Claims

- Short stance: local-first, hybrid search, auto wiki compile; explicitly no KG/temporal/scoping in one line.
- Target list: semantic + episodic + procedural memory, KG, hybrid FTS+vec+RRF, contradiction detect, MCP, SSE streaming.
- Procedural memory alongside semantic/episodic as goal.
- Bilingual EN/ZH capability labels.

## Unique Insights

- Stakeholder checklist, not architecture proof — internal tension on graph/scoping.

## Contradictions

Self-contradictory: line 10 denies KG; longer list includes KG — scope as now vs target.

**Clarified (2026-05-24):** Short "no KG" line = current state; longer list = target. Hybrid search now built. See [[mem-weaver-as-built-status]].

Related concepts: [[mem-weaver-known-gaps]] [[mem-weaver-as-built-status]]
