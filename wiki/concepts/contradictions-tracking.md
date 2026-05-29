---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Contradictions Tracking

## Consensus

Where multi-LLM input earns its keep ([[claude-multi-llm-research-synthesis-workflow]]). Without explicit tracking, multi-LLM outputs **amplify hallucinations** — agents pick arbitrary winners from conflicting advice.

Tracking surfaces:
- Dedicated `contradictions.md` with UNRESOLVED status (Claude)
- Concept page Divergence tables (this project's approach)
- Stage 1 structural analysis conflict detection (Gemini [[two-stage-ingestion]])
- Embedding cluster contradiction detection (ChatGPT [[semantic-deduplication]])

Resolved contradictions use [[compounding-knowledge-layer]] systematic supersession — mark stale, link override.

Works with [[human-review-gate]] — human resolves UNRESOLVED items before dev context export. Wiki lint finds stale contradictions after every 3–5 ingests.

Example format:

```markdown
## [Topic]: Auth Strategy
- Claude: Use JWT + refresh tokens
- GPT: Use opaque tokens for security
- Gemini: Both, with JWT for internal, opaque for public
- Status: UNRESOLVED — research OAuth2 RFC before deciding
```

## Divergence

| Source | Mechanism |
|--------|-----------|
| Claude | Dedicated `contradictions.md`; lint-driven discovery |
| ChatGPT | Automated contradiction detection in embedding clusters |
| Gemini | Stage 1 analysis + supersession lifecycle |

## Decision

**Use concept Divergence tables + lint for now; generate `contradictions.md` at export-brief time from UNRESOLVED items.** Resolved in [[wiki-vs-context-engine]] and other concept Decisions.
