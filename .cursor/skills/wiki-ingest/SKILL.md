---
name: wiki-ingest
description: Ingest one raw source file into the project wiki. Use when the user says "ingest", adds a file to raw/, or asks to process pending sources.
---

# Wiki Ingest

Ingest **one** raw source into the wiki. Read `AGENTS.md` for full schema; this skill enforces the rigid parts.

## Before Starting

1. Read `AGENTS.md` if you haven't this session
2. Identify the target file in `raw/llm/` or `raw/web/`
3. Verify frontmatter `status: pending` — abort if already `ingested`

## Steps

1. **Read** the raw file completely
2. **Discuss** key takeaways with the user — do not skip this step
3. **Create** `wiki/sources/<slug>.md` using the source page format from AGENTS.md
4. **Update** relevant `wiki/concepts/` pages:
   - Merge duplicate claims from other sources
   - Add comparison table rows for divergent recommendations
   - Flag contradictions explicitly — never silently pick a winner
5. **Update** `wiki/synthesis/evolving-thesis.md` — revise Current Understanding, Open Questions, Emerging Decisions
6. **Update** `wiki/index.md` — add entries under Sources and Concepts
7. **Append** to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <slug>`
8. **Ask user to confirm** before setting raw frontmatter `status: ingested`

## Guardrails

- ONE file per invocation
- NEVER modify raw body text — only update frontmatter `status`
- ALWAYS update index.md and log.md
- ALWAYS discuss takeaways before writing wiki pages
- If multiple pending files exist, process one and stop
