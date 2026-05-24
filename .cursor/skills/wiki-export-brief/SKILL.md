---
name: wiki-export-brief
description: Generate a frozen project brief for dev repo handoff. Use when the user says "export brief" or "ready to build".
---

# Wiki Export Brief

Generate `wiki/synthesis/project-brief.md` from the evolving wiki. Requires lint first.

## Prerequisites

1. Run wiki-lint (or quick lint check) before exporting
2. Surface any remaining warnings — user must acknowledge before proceeding

## Steps

1. **Lint** — run lint checks; report issues
2. **Read** `wiki/synthesis/evolving-thesis.md` and all `wiki/concepts/` pages
3. **Count** ingested sources: `grep -rl "status: ingested" raw/` or count source pages
4. **Write** `wiki/synthesis/project-brief.md` with `status: draft`:

   Sections (all required):
   - `# Project Brief: <Project Name>` — ask user if unknown
   - `## Problem`
   - `## Chosen Approach` — from Emerging Decisions in evolving-thesis and concept Decision sections
   - `## Constraints`
   - `## Non-Goals`
   - `## Rejected Alternatives` — from Divergence tables where options were rejected
   - `## Open Questions` — unresolved items

5. **Present** draft to user for review
6. On approval → set frontmatter `status: frozen`, update date, set `sources_ingested` count
7. **Append** to log: `## [YYYY-MM-DD] export | project-brief frozen`
8. **Remind user** of handoff steps from AGENTS.md:
   - Copy to dev repo `docs/PROJECT_BRIEF.md`
   - Add wiki as git submodule
   - Tag wiki repo `v1.0-research-complete`

## Guardrails

- Brief must be self-contained — readable without opening raw/ or other wiki pages
- Do not freeze without user approval
- Include rejected alternatives, not just the chosen approach
- Do not silently drop open questions
