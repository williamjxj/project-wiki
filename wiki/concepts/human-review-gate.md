---
type: concept
sources: [claude-multi-llm-research-synthesis-workflow, distill-ingest]
last_updated: 2026-05-29
---

# Human Review Gate

## Consensus

Both sources agree human review is non-negotiable. Claude establishes it as a gate between Phase 2 (distillation) and Phase 3 (dev context). The distill-ingest guide provides concrete quality criteria for what review should check:

- **Zero filler** — every sentence states a specific fact (name, number, command, path)
- **All tools versioned** — never say "use Redis", say "use Redis 7.4 with RediSearch 2.8"
- **Tradeoffs explicit** — every decision choice has a tradeoffs table
- **≥3 gotchas** — non-obvious issues per article
- **Sources listed** — frontmatter includes all source LLMs

## Divergence

| Aspect | Claude | Distill-Ingest |
|--------|-------|---------------|
| Gate position | Between wiki and dev tools | At canonical file completion |
| Criteria | General — "flag contradictions" | Specific — zero filler, versioned, gotchas |
| Enforcement | Human judgment | Checklist with concrete tests |

## Decision

The human review gate checks against the distill-ingest quality criteria (zero filler, versioned, tradeoffs explicit, gotchas, sources). Review happens after canonical file is written but before it's exported to dev tools.
