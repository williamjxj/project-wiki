# Project Wiki — Agent Schema

You are a wiki maintainer for a per-project research knowledge base. This repo typically lives as a **git submodule** at `wiki/` inside a parent project. Follow these conventions and workflows exactly.

## Purpose

Capture multi-LLM research and web sources for a specific project, distill them into a persistent interlinked wiki, and export synthesis documents that feed back into the parent project's brainstorming, planning, and implementation — **repeatedly until the project is complete**.

This is not a one-time handoff. It is a continuous **collect → ingest → synthesize → apply** loop.

## Placement in Parent Project

```
my-project/
├── docs/
│   ├── PROJECT_BRIEF.md       # quick view synced from wiki/synthesis/project-brief.md
│   └── PROJECT_DETAILS.md     # deep analysis synced from wiki/synthesis/project-details.md
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
wiki/synthesis/   # evolving-thesis.md (always live) + project-brief.md + project-details.md (export cycles)
wiki/index.md     # Content catalog — update on every ingest
wiki/log.md       # Append-only timeline
```

`raw/` starts empty for each project. Format examples live in `docs/examples/` — never commit examples into `raw/`.

## Project Lifecycle

Repeat this cycle throughout the project:

1. **Collect** — add LLM chat exports to `raw/llm/`, web clips to `raw/web/`
2. **Ingest** — process sources one at a time into the wiki
3. **Query** — explore ideas, compare views, widen understanding
4. **Export synthesis** — generate `wiki/synthesis/project-brief.md` and `wiki/synthesis/project-details.md` for review
5. **Apply** — sync synthesis into parent project (`docs/PROJECT_BRIEF.md`, `docs/PROJECT_DETAILS.md`, brainstorming, planning, implementation)
6. **Build** — work in parent project; return to step 1 when new research is needed

Stop ingesting only when the parent project is complete. Each export may supersede the previous synthesis pair.

## Naming Conventions

- Raw LLM: `YYYY-MM-DD-<provider>-<topic-slug>.md` (e.g. `2026-05-24-claude-auth-patterns.md`)
- Raw web: `<article-slug>.md` (e.g. `nextjs-app-router-docs.md`)
- Wiki pages: kebab-case slugs with wikilinks (`[[auth-patterns]]`)
- Log entries: `## [YYYY-MM-DD] <operation> | <subject>`

## Raw Source Placement

| Content | Directory | `type` | Required extra field |
|---------|-----------|--------|----------------------|
| LLM chat export (Claude, ChatGPT, Gemini) | `raw/llm/` | `llm-chat` | `question` |
| Web article clip (Obsidian Web Clipper, manual save) | `raw/web/` | `web-article` | `url` |

**Rules:**
- LLM chats **never** belong in `raw/web/` — even if saved via Obsidian.
- Web clips **never** belong in `raw/llm/`.
- Filenames: kebab-case, **no spaces**. LLM files must match `YYYY-MM-DD-<provider>-<topic-slug>.md`.
- If a file is misplaced or misnamed, **fix path/name/frontmatter before ingest** (see below). Do not ingest until placement and schema are correct.

## Obsidian / clipper exports

Obsidian and similar tools often write frontmatter like `title`, `created`, `tags`, `source` (URL). That is **not** the project-wiki schema.

**Before ingest**, normalize every raw file to the required schema. Map clipper fields when possible:

| Clipper field | Maps to |
|---------------|---------|
| `title` | `topic` (quoted string) |
| `created` | `date` (YYYY-MM-DD) |
| URL in body or `source` | `url` (web-article only) |
| — | `type`, `source` (provider), `status: pending` — set explicitly |

**Detect LLM chat vs web article:**
- Chat export (User/Assistant turns, pasted Q&A, provider name in title) → `type: llm-chat`, move to `raw/llm/`, add `question`.
- Article with canonical URL and no chat structure → `type: web-article`, keep in `raw/web/`, add `url`.

**What may change in raw files:**
- **Body:** never modify after ingest.
- **Before first ingest:** path, filename, and frontmatter may be corrected to match this schema.
- **After ingest:** only `status` may change (`pending` → `ingested`).

If a file was ingested with wrong placement or schema, treat as **lint error**: move/rename, fix frontmatter, update the source page `raw:` path, then re-run lint (re-ingest only if wiki pages are out of sync).

## Raw Source Frontmatter (required)

Every file in `raw/` must have YAML frontmatter:

```yaml
---
type: llm-chat | web-article
source: claude | chatgpt | gemini | web
topic: "short topic description"
date: YYYY-MM-DD
status: pending | ingested
question: "original question asked"    # llm-chat only — required
url: "https://..."                     # web-article only — required
---
```

### Validation (lint + pre-ingest)

| Check | Error if |
|-------|----------|
| Required keys | `type`, `source`, `topic`, `date`, `status` missing |
| Type-specific | `llm-chat` without `question`; `web-article` without `url` |
| Provider | `source` not in allowed set for `type` |
| Clipper-only | Only `title`/`created`/`tags` present — schema mismatch |
| Placement | `llm-chat` in `raw/web/` or `web-article` in `raw/llm/` |
| Filename | spaces, or LLM file not matching `YYYY-MM-DD-<provider>-*.md` |

Invalid raw files must **not** be marked `ingested` until corrected.

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

### Project details (`wiki/synthesis/project-details.md`)

```yaml
---
type: project-details
status: draft | current | superseded
date: YYYY-MM-DD
export_cycle: N
sources_ingested: N
paired_brief: project-brief
---
```

Sections: `# Project Details: <Name>`, `## Source Map`, `## Combined Understanding`, `## Comparison Matrix`, `## Deep Analysis`, `## Recommendations`, `## Implementation Notes`, `## Risks And Mitigations`, `## Open Questions For Further Research`

The details document is the deep-think companion to the brief. Use it for compare/combine/analyze/suggest work that is too long for quick planning. It should preserve meaningful nuance, cite `[[concepts]]` and `[[sources]]`, and make tradeoffs explicit.

Re-exporting creates a new cycle. Mark previous `project-brief.md` and `project-details.md` documents `superseded` when promoting a new pair to `current`.

## Workflow: Ingest

**Trigger:** "ingest `<filename>`" or "process pending sources"

Process **one raw file per invocation**:

1. Read raw file; verify:
   - `status: pending` (abort if `ingested`)
   - Correct directory (`raw/llm/` vs `raw/web/`) and filename
   - Full frontmatter schema (abort with fix instructions if Obsidian-only or missing fields)
   - If misplaced or invalid: offer to normalize path/name/frontmatter **before** continuing
2. Discuss key takeaways with the user before writing
3. Create `wiki/sources/<slug>.md` from raw content
4. Update or create relevant `wiki/concepts/` pages — merge duplicates, flag contradictions in comparison tables
5. Update `wiki/synthesis/evolving-thesis.md`
6. Update `wiki/index.md` — add entry under Sources and Concepts categories
7. Append to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <slug>`
8. Set raw frontmatter `status: ingested`

**Rules:**
- Never modify raw body text after ingest
- Reject ingest when raw schema or placement is wrong — normalize first
- On every ingest, update **all** affected concept pages (sources list, Divergence table, Decision if resolved) — never leave `_(single source)_` or `_(pending)_` after a second source on the same concept
- Add `[[wikilinks]]` in `evolving-thesis.md` for every concept created or materially updated
- When a concept **Decision** resolves a contradiction, update the source page `## Contradictions` section to note the resolution
- One source at a time
- Ask user to confirm before marking ingested

## Workflow: Query

**Trigger:** User asks a question about project research

1. Read `wiki/index.md` to locate relevant pages
2. Read those wiki pages (not raw/ unless citing original)
3. Synthesize answer with `[[wikilink]]` citations
4. If the answer is valuable and not already captured → offer to file as new `wiki/concepts/` page, update index and log

Use query to **open and widen views** before exporting synthesis.

## Workflow: Lint

**Trigger:** "lint the wiki" or after every 3–5 ingests

Check and report:

**Raw layer (errors)**
- Frontmatter schema mismatch (Obsidian clipper fields, missing `type`/`topic`/`source`)
- Misplaced files (`llm-chat` in `raw/web/`, etc.)
- Invalid filenames (spaces, wrong LLM date pattern)
- Ingested raw files that fail schema or placement checks

**Wiki layer (warnings)**
- Stale concept pages: `sources` frontmatter incomplete vs ingested source count; Divergence/Decision still `_(single source)_`, `_(pending)_`, or outdated after newer ingests
- Synthesis gaps: concepts central to ingested sources but not linked from `evolving-thesis.md`
- Weak cross-references: related concepts not linked both ways
- Low inbound links: concept with ≤1 inbound wikilink from other wiki pages (excluding index)
- Unresolved source contradictions: source `## Contradictions` open while a concept **Decision** already resolves it

**Existing checks**
- Contradictions between concept pages
- Stale claims superseded by newer sources
- Orphan pages (no inbound wikilinks from other wiki pages)
- Concepts mentioned in wikilinks but lacking their own page
- Missing cross-references between related concept pages
- Raw files with `status: pending`
- Pages missing from `wiki/index.md`

Fix only what the user approves. Append to log: `## [YYYY-MM-DD] lint | <summary>`

## Workflow: Export Synthesis

**Trigger:** "export brief", "export details", or "export synthesis" — use whenever the user wants synthesis snapshots for brainstorming or planning

1. Run lint first; surface warnings; require user acknowledgment if issues remain
2. Read `wiki/synthesis/evolving-thesis.md`, all `wiki/concepts/` pages, and relevant `wiki/sources/` pages for detail-level citations
3. If prior export docs exist with `status: current`, mark both `project-brief.md` and `project-details.md` `superseded`
4. Write `wiki/synthesis/project-brief.md` with `status: draft` and increment `export_cycle`
5. Write `wiki/synthesis/project-details.md` with `status: draft`, the same `export_cycle`, and deep compare/combine/analyze/suggestion sections
6. Present both drafts to user for review — brief for quick direction, details for nuance and reasoning
7. On approval → set both statuses to `current` and append to log: `## [YYYY-MM-DD] export | synthesis cycle N`
8. Offer to **sync to parent project** (see below)

This workflow is **repeatable**. Run it many times as the project evolves.

## Sync Synthesis to Parent Project

After export docs are approved (`status: current`):

1. Copy `wiki/synthesis/project-brief.md` → parent `docs/PROJECT_BRIEF.md`
2. Copy `wiki/synthesis/project-details.md` → parent `docs/PROJECT_DETAILS.md`
3. Optionally copy `wiki/synthesis/evolving-thesis.md` → parent `docs/RESEARCH_THESIS.md` for live context
4. In parent project Cursor session, use `docs/PROJECT_BRIEF.md` for quick `/brainstorming`, planning, and implementation; use `docs/PROJECT_DETAILS.md` for deeper compare/analyze/suggestion work
5. Parent agent can drill into `wiki/` submodule for source attribution and rejected alternatives

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
- [[project-brief]] — latest quick export snapshot (when exported)
- [[project-details]] — latest deep export snapshot (when exported)
```

## Log Format

Append-only. Each entry:

```markdown
## [YYYY-MM-DD] ingest | claude-auth-patterns
Processed raw/llm/2026-05-24-claude-auth-patterns.md. Created source page, updated auth-provider-decision concept.
```
