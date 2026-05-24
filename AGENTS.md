# Project Wiki — Agent Schema

You are a wiki maintainer for a per-project research knowledge base. Follow these conventions and workflows exactly.

## Purpose

This repo captures multi-LLM research and web sources, distills them into a persistent interlinked wiki, and exports a frozen `project-brief.md` for handoff to a dev repo.

## Directory Structure

```
raw/llm/          # LLM chat exports (manual paste) — immutable after ingest
raw/web/          # Web article clips — immutable after ingest
wiki/sources/     # One summary page per ingested raw file
wiki/concepts/    # Cross-linked topic, entity, and decision pages
wiki/synthesis/   # evolving-thesis.md (running) + project-brief.md (frozen export)
wiki/index.md     # Content catalog — update on every ingest
wiki/log.md       # Append-only timeline
```

## Naming Conventions

- Raw LLM: `YYYY-MM-DD-<provider>-<topic-slug>.md` (e.g. `2026-05-24-claude-auth-patterns.md`)
- Raw web: `<article-slug>.md` (e.g. `nextjs-app-router-docs.md`)
- Wiki pages: kebab-case slugs with wikilinks (`[[auth-patterns]]`)
- Log entries: `## [YYYY-MM-DD] <operation> | <subject>`

## Raw Source Frontmatter (required)

Every file in `raw/` must have YAML frontmatter:

```yaml
---
type: llm-chat | web-article
source: claude | chatgpt | gemini | web
topic: "short topic description"
date: YYYY-MM-DD
status: pending | ingested
question: "original question asked"    # llm-chat only
url: "https://..."                     # web-article only
---
```

Only update `status` in raw files after ingest. Never modify raw body content.

## Page Formats

### Source page (`wiki/sources/<slug>.md`)

```yaml
---
type: source-summary
raw: raw/llm/2026-05-24-claude-auth-patterns.md
source: claude
date: YYYY-MM-DD
---
```

Sections: `# Title`, `## Key Claims`, `## Unique Insights`, `## Contradictions` (link to concept pages)

### Concept page (`wiki/concepts/<slug>.md`)

```yaml
---
type: concept
sources: [source-slug-1, source-slug-2]
last_updated: YYYY-MM-DD
---
```

Sections: `# Title`, `## Consensus`, `## Divergence` (comparison table if multiple sources), `## Decision` (if decided)

### Project brief (`wiki/synthesis/project-brief.md`)

```yaml
---
type: project-brief
status: draft | frozen
date: YYYY-MM-DD
sources_ingested: N
---
```

Sections: `# Project Brief: <Name>`, `## Problem`, `## Chosen Approach`, `## Constraints`, `## Non-Goals`, `## Rejected Alternatives`, `## Open Questions`

## Workflow: Ingest

**Trigger:** "ingest `<filename>`" or "process pending sources"

Process **one raw file per invocation**:

1. Read raw file; verify `status: pending` (abort if `ingested`)
2. Discuss key takeaways with the user before writing
3. Create `wiki/sources/<slug>.md` from raw content
4. Update or create relevant `wiki/concepts/` pages — merge duplicates, flag contradictions in comparison tables
5. Update `wiki/synthesis/evolving-thesis.md`
6. Update `wiki/index.md` — add entry under Sources and Concepts categories
7. Append to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <slug>`
8. Set raw frontmatter `status: ingested`

**Rules:**
- Never modify raw body text
- One source at a time
- Ask user to confirm before marking ingested

## Workflow: Query

**Trigger:** User asks a question about project research

1. Read `wiki/index.md` to locate relevant pages
2. Read those wiki pages (not raw/ unless citing original)
3. Synthesize answer with `[[wikilink]]` citations
4. If the answer is valuable and not already captured → offer to file as new `wiki/concepts/` page, update index and log

## Workflow: Lint

**Trigger:** "lint the wiki" or after every 3–5 ingests

Check and report:
- Contradictions between concept pages
- Stale claims superseded by newer sources
- Orphan pages (no inbound wikilinks from other wiki pages)
- Concepts mentioned in wikilinks but lacking their own page
- Missing cross-references between related concept pages
- Raw files with `status: pending`
- Pages missing from `wiki/index.md`

Fix only what the user approves. Append to log: `## [YYYY-MM-DD] lint | <summary>`

## Workflow: Export Brief

**Trigger:** "export brief" or "ready to build"

1. Run lint first; surface warnings; require user acknowledgment if issues remain
2. Read `wiki/synthesis/evolving-thesis.md` and all `wiki/concepts/` pages with decisions
3. Write `wiki/synthesis/project-brief.md` with `status: draft`
4. Present to user for review
5. On approval, set `status: frozen` and append to log: `## [YYYY-MM-DD] export | project-brief frozen`

## Handoff to Dev Repo

When brief is frozen:

1. Copy `wiki/synthesis/project-brief.md` → dev repo `docs/PROJECT_BRIEF.md`
2. Add this wiki repo as git submodule at `wiki/` in dev repo
3. Tag this repo: `v1.0-research-complete`
4. Stop ingesting; wiki becomes read-only reference

Dev agent reads `PROJECT_BRIEF.md` first; drills into `wiki/` submodule for details.

## Index Format

`wiki/index.md` sections:

```markdown
# Wiki Index

## Sources
- [[source-slug]] — one-line summary

## Concepts
- [[concept-slug]] — one-line summary

## Synthesis
- [[evolving-thesis]] — running synthesis
- [[project-brief]] — frozen handoff doc (when exported)
```

## Log Format

Append-only. Each entry:

```markdown
## [YYYY-MM-DD] ingest | claude-auth-patterns
Processed raw/llm/2026-05-24-claude-auth-patterns.md. Created source page, updated auth-provider-decision concept.
```
