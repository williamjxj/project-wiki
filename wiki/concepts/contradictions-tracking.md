---
type: concept
sources: [claude-multi-llm-research-synthesis-workflow, gemini-llm-wiki-multi-agent, distill-ingest]
last_updated: 2026-05-29
---

# Contradictions Tracking

## Consensus

Both sources address contradictions. Claude flags them explicitly with UNRESOLVED status. Gemini goes further with **systematic supersession**: when new info contradicts existing, the compiling agent marks the old claim as stale, appends a timestamped link to the newer overriding assertion, and archives the older version for historical auditability.

Claude's approach alerts the user to decide. Gemini's approach resolves automatically through supersession while preserving history.

## Divergence

| Aspect | Claude | Gemini |
|--------|-------|--------|
| Status | UNRESOLVED — requires human decision | SUPERSEDED — auto-resolved, archived |
| Resolution | Human review gate decides | System marks old as stale, links to new |
| History tracking | Contradictions page | Archived versions with timestamps |

## Decision

Use all three approaches. Contradictions that can be resolved through supersession (newer source overrides older) follow Gemini's pattern. Contradictions requiring judgment remain UNRESOLVED and go through Claude's human review gate. In all cases, frame contradictions as **design space exploration** (distill-ingest reframe) — disagreements define the solution landscape, not bugs to eliminate. Each contradiction becomes a tradeoff with explicit pro/con for each option.
