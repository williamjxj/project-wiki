---
name: wiki-export-synthesis
description: Generate paired quick and deep synthesis snapshots from the wiki for parent project brainstorming. Use when the user says "export brief", "export details", or "export synthesis" — repeatable throughout the project lifecycle.
---

# Wiki Export Synthesis

Generate paired export docs from the evolving wiki:

- `wiki/synthesis/project-brief.md` — quick planning view
- `wiki/synthesis/project-details.md` — deep compare/combine/analyze/suggest view

Requires lint first. **This is repeatable** — run after each research batch or when revisiting project direction.

## Prerequisites

1. Run wiki-lint (or quick lint check) before exporting
2. Surface any remaining warnings — user must acknowledge before proceeding

## Steps

1. **Lint** — run lint checks; report issues
2. **Read** `wiki/synthesis/evolving-thesis.md`, all `wiki/concepts/` pages, and relevant `wiki/sources/` pages for detail-level citations
3. **Count** ingested sources: count files in `wiki/sources/` or `grep -rl "status: ingested" raw/`
4. **Supersede prior exports** — if `project-brief.md` or `project-details.md` exists with `status: current`, change to `superseded`
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

6. **Write** `wiki/synthesis/project-details.md` with `status: draft`, the same `export_cycle`, and these required sections:
   - `# Project Details: <Project Name>` — same project name as the brief
   - `## Source Map` — source and concept coverage, with `[[wikilink]]` citations
   - `## Combined Understanding` — synthesized view across sources
   - `## Comparison Matrix` — concrete tradeoffs, agreements, and disagreements
   - `## Deep Analysis` — reasoning behind choices and unresolved tensions
   - `## Recommendations` — suggested actions, ordered by confidence and impact
   - `## Implementation Notes` — practical implications for the parent project
   - `## Risks And Mitigations`
   - `## Open Questions For Further Research`

7. **Present** both drafts to user — brief for quick direction, details for nuance and reasoning
8. On approval → set both statuses to `current`, update date and `sources_ingested` count
9. **Append** to log: `## [YYYY-MM-DD] export | synthesis cycle N`
10. **Offer to sync** to parent project:
   - `cp wiki/synthesis/project-brief.md ../docs/PROJECT_BRIEF.md` (adjust path for submodule layout)
   - `cp wiki/synthesis/project-details.md ../docs/PROJECT_DETAILS.md` (adjust path for submodule layout)
   - Optionally sync `evolving-thesis.md` to `docs/RESEARCH_THESIS.md`

## Guardrails

- Brief must be readable without opening raw/ — but link to wiki concept pages for depth
- Details must preserve nuance from concepts and source summaries without copying raw content wholesale
- Do not set either export doc to `current` without user approval
- Include rejected alternatives, comparisons, recommendations, and open questions — these widen views
- This is not a one-time handoff; expect multiple export cycles per project
- Do not tell user to archive or stop ingesting — research continues until project complete
