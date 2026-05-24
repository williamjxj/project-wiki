# Project Wiki — Agent Schema

You are a wiki maintainer for a per-project research knowledge base. This repo typically lives as a **git submodule** at `wiki/` inside a parent project. Follow these conventions and workflows exactly.

## Purpose

Capture multi-LLM research and web sources for a specific project, distill them into a persistent interlinked wiki, and export synthesis documents that feed back into the parent project's brainstorming, planning, and implementation — **repeatedly until the project is complete**.

This is not a one-time handoff. It is a continuous **collect → ingest → synthesize → apply** loop.

## Placement in Parent Project

```
my-project/
├── docs/
│   └── PROJECT_BRIEF.md       # synced from wiki/synthesis/project-brief.md
├── wiki/                      # project-wiki submodule
│   ├── raw/
│   ├── wiki/
│   └── AGENTS.md
├── src/
└── ...
```

## Directory Structure

```
raw/llm/          # LLM chat exports (manual paste) — immutable after ingest
raw/web/          # Web article clips — immutable after ingest
wiki/sources/     # One summary page per ingested raw file
wiki/concepts/    # Cross-linked topic, entity, and decision pages
wiki/synthesis/   # evolving-thesis.md (always live) + project-brief.md (export cycles)
wiki/index.md     # Content catalog — update on every ingest
wiki/log.md       # Append-only timeline
```

`raw/` starts empty for each project. Format examples live in `docs/examples/` — never commit examples into `raw/`.

## Project Lifecycle

Repeat this cycle throughout the project:

1. **Collect** — add LLM chat exports to `raw/llm/`, web clips to `raw/web/`
2. **Ingest** — process sources one at a time into the wiki
3. **Query** — explore ideas, compare views, widen understanding
4. **Export brief** — generate `wiki/synthesis/project-brief.md` for review
5. **Apply** — sync synthesis into parent project (`docs/PROJECT_BRIEF.md`, brainstorming, planning, implementation)
6. **Build** — work in parent project; return to step 1 when new research is needed

Stop ingesting only when the parent project is complete. Each export may supersede the previous brief.

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
status: draft | current | superseded
date: YYYY-MM-DD
export_cycle: N
sources_ingested: N
---
```

Sections: `# Project Brief: <Name>`, `## Problem`, `## Current Understanding`, `## Chosen Approach`, `## Constraints`, `## Non-Goals`, `## Rejected Alternatives`, `## Open Questions`

Re-exporting creates a new cycle. Mark the previous brief `superseded` when promoting a new one to `current`.

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

Use query to **open and widen views** before exporting a brief.

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

**Trigger:** "export brief" — use whenever the user wants a synthesis snapshot for brainstorming or planning

1. Run lint first; surface warnings; require user acknowledgment if issues remain
2. Read `wiki/synthesis/evolving-thesis.md` and all `wiki/concepts/` pages
3. If a prior brief exists with `status: current`, mark it `superseded`
4. Write `wiki/synthesis/project-brief.md` with `status: draft` and increment `export_cycle`
5. Present to user for review — aim to widen views, not just confirm existing decisions
6. On approval → set `status: current` and append to log: `## [YYYY-MM-DD] export | project-brief cycle N`
7. Offer to **sync to parent project** (see below)

This workflow is **repeatable**. Run it many times as the project evolves.

## Sync Synthesis to Parent Project

After a brief is approved (`status: current`):

1. Copy `wiki/synthesis/project-brief.md` → parent `docs/PROJECT_BRIEF.md`
2. Optionally copy `wiki/synthesis/evolving-thesis.md` → parent `docs/RESEARCH_THESIS.md` for deeper context
3. In parent project Cursor session, use `docs/PROJECT_BRIEF.md` for `/brainstorming`, planning, and implementation
4. Parent agent can drill into `wiki/` submodule for source attribution and rejected alternatives

Commit both submodule changes and parent `docs/` updates when syncing.

## Index Format

`wiki/index.md` sections:

```markdown
# Wiki Index

## Sources
- [[source-slug]] — one-line summary

## Concepts
- [[concept-slug]] — one-line summary

## Synthesis
- [[evolving-thesis]] — running synthesis (always live)
- [[project-brief]] — latest export snapshot (when exported)
```

## Log Format

Append-only. Each entry:

```markdown
## [YYYY-MM-DD] ingest | claude-auth-patterns
Processed raw/llm/2026-05-24-claude-auth-patterns.md. Created source page, updated auth-provider-decision concept.
```
