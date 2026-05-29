---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Context Compression

## Consensus

Future winning systems are better **context engineering systems**, not better models ([[chatgpt-llm-based-project-workflow]]).

```
10,000 pages → 20 pages → 2 pages → implementation prompts
```

Compression enables [[context-packs]] and [[implementation-readiness]] without overwhelming agent context windows.

- ChatGPT: tiered compression as core competitive moat
- Gemini: `llms-full.txt` capped at 5MB; portable Anthropic Skills as dense capability packages
- Claude: compile targeted context per task — **don't dump the full wiki**

## Divergence

| Source | View |
|--------|------|
| ChatGPT | Aggressive multi-tier compression (10K → 2 pages) |
| Gemini | Standardized export formats with size caps and Skills packaging |
| Claude | Per-task targeted packs, not whole-wiki compression |

## Decision

**Lean: per-task [[context-packs]] (Claude) as primary handoff; tiered compression (ChatGPT) as the design principle; Gemini export formats (`llms.txt`, Skills) as optional packaging layer.**
