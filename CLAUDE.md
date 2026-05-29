# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This is **project-wiki** — a per-project research knowledge base (template), based on [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). It contains **no application code**: there is no build, no test suite, no package manager. The "work" is maintaining a Markdown knowledge base by running four workflows (ingest, query, lint, export synthesis) against curated research sources.

It is designed to live as a **git submodule** mounted at `wiki/` inside a parent application project. The `main` branch is the pristine skeleton; app-specific research belongs on feature/app branches.

## Authoritative schema: read AGENTS.md first

`AGENTS.md` is the single source of truth for all conventions — frontmatter schemas, naming rules, page formats, validation checks, and the exact step-by-step procedure for each workflow. **Read it before doing any wiki operation.** This file (CLAUDE.md) only summarizes the big picture; AGENTS.md has the rules you must follow exactly.

The `.cursor/skills/` directory (`wiki-ingest`, `wiki-query`, `wiki-lint`, `wiki-export-synthesis`) encodes the same workflows as Cursor skills. They are the portable/enforced version of AGENTS.md — when a user says "ingest", "lint the wiki", "export brief", "export details", "export synthesis", or asks a research question, follow the corresponding workflow.

## Three-layer architecture

Knowledge flows in one direction through three layers with distinct ownership:

1. **`raw/`** (user-owned, immutable after ingest) — verbatim source material. `raw/llm/` holds LLM chat exports (`type: llm-chat`, requires `question`); `raw/web/` holds web article clips (`type: web-article`, requires `url`). Every file needs the full YAML frontmatter schema in AGENTS.md. **Never edit a raw body after ingest** — only `status: pending → ingested` may change.
2. **`wiki/`** (agent-owned) — the distilled, cross-linked knowledge base:
   - `wiki/sources/` — one summary page per ingested raw file (Key Claims, Unique Insights, Contradictions)
   - `wiki/concepts/` — cross-linked topic/decision pages (Consensus, Divergence table, Decision)
   - `wiki/synthesis/evolving-thesis.md` — running synthesis, always live
   - `wiki/synthesis/project-brief.md` — quick export snapshots that cycle `draft → current → superseded`
   - `wiki/synthesis/project-details.md` — deep export snapshots for compare/combine/analyze/suggest work
   - `wiki/index.md` — catalog of every page; update on every ingest
   - `wiki/log.md` — append-only timeline (`## [YYYY-MM-DD] <op> | <subject>`)
3. **`docs/`** — design specs/examples, and (in a parent project) the synced `PROJECT_BRIEF.md` and `PROJECT_DETAILS.md`.

Pages are linked with `[[wikilink]]` slugs (kebab-case). Cross-links are load-bearing: lint flags orphans, missing inbound links, and concepts referenced but lacking a page.

## Core workflow rules (the ones easy to get wrong)

- **Ingest one source at a time.** Discuss takeaways with the user before writing pages. Batch ingests produce mushy synthesis.
- **Validate placement and frontmatter before ingest.** Obsidian/clipper exports arrive with `title`/`created`/`tags` — these are *not* the schema. Normalize path, filename, and frontmatter (map `title→topic`, `created→date`, set `type`/`source`/`status` explicitly) before processing. LLM chats never go in `raw/web/` and vice versa. Reject ingest on schema/placement errors.
- **On every ingest, update all affected concept pages** — sources list, Divergence table, Decision. Never leave `_(single source)_` or `_(pending)_` once a second source touches a concept.
- **Lint before export.** Export reads `evolving-thesis.md`, concept pages, and relevant source summaries; supersedes any `current` brief/details pair; writes new `draft` docs; and increments `export_cycle`. Workflows are repeatable — the wiki compounds across cycles.
- **Query reads `wiki/index.md` first**, then the relevant wiki pages — not `raw/` (unless citing originals), not general knowledge. Answer with `[[wikilink]]` citations.

## Submodule discipline (when used inside a parent project)

Wiki changes require **two commits**: first inside the submodule (`raw/` + `wiki/`), then in the parent to record the new submodule pointer plus any synced `docs/`. Never gitignore `wiki/` in the parent — that breaks submodule tracking. See README.md "Submodule setup and maintenance" for the full procedure.

## Markdown linting

`.markdownlint.json` disables line-length (MD013), duplicate-heading (MD024), inline-HTML (MD033), and several spacing rules — wiki pages intentionally use long lines, repeated section headings (Key Claims / Decision etc.), and Obsidian-style markup. Run markdownlint via your editor or `npx markdownlint-cli '**/*.md'` if checking formatting; there is no committed lint script.
