---
name: wiki-export-brief
description: Generate a synthesis snapshot from the wiki for parent project brainstorming. Use when the user says "export brief" — repeatable throughout the project lifecycle.
---

# Wiki Export Brief

Generate `wiki/synthesis/project-brief.md` from the evolving wiki. Requires lint first. **This is repeatable** — run after each research batch or when revisiting project direction.

## Prerequisites

1. Run wiki-lint (or quick lint check) before exporting
2. Surface any remaining warnings — user must acknowledge before proceeding

## Steps

1. **Lint** — run lint checks; report issues
2. **Read** `wiki/synthesis/evolving-thesis.md` and all `wiki/concepts/` pages
3. **Count** ingested sources: count files in `wiki/sources/` or `grep -rl "status: ingested" raw/`
4. **Supersede prior brief** — if `project-brief.md` exists with `status: current`, change to `superseded`
5. **Write** `wiki/synthesis/project-brief.md` with `status: draft` and increment `export_cycle`:

   Sections (all required):
   - `# Project Brief: <Project Name>` — ask user if unknown
   - `## Problem`
   - `## Current Understanding` — from evolving-thesis
   - `## Chosen Approach` — from Emerging Decisions and concept Decision sections (note tentative vs firm)
   - `## Constraints`
   - `## Non-Goals`
   - `## Rejected Alternatives` — from Divergence tables
   - `## Open Questions` — unresolved items to widen exploration

6. **Present** draft to user — aim to open views, not just summarize
7. On approval → set `status: current`, update date and `sources_ingested` count
8. **Append** to log: `## [YYYY-MM-DD] export | project-brief cycle N`
9. **Offer to sync** to parent project:
   - `cp wiki/synthesis/project-brief.md ../docs/PROJECT_BRIEF.md` (adjust path for submodule layout)
   - Optionally sync `evolving-thesis.md` to `docs/RESEARCH_THESIS.md`

## Guardrails

- Brief must be readable without opening raw/ — but link to wiki concept pages for depth
- Do not set `current` without user approval
- Include rejected alternatives and open questions — these widen views
- This is not a one-time handoff; expect multiple export cycles per project
- Do not tell user to archive or stop ingesting — research continues until project complete
