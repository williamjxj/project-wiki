# Project Wiki Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a per-project LLM Wiki template (`project-wiki`) with directory scaffold, AGENTS.md schema, seed wiki files, example raw sources, four Cursor skills, and README quickstart.

**Architecture:** Karpathy's three-layer pattern (raw sources → wiki → schema) as a cloneable git template. Agent-agnostic `AGENTS.md` defines ingest/query/lint/export workflows; Cursor skills in `.cursor/skills/` enforce rigidity. No application code — markdown and skill files only.

**Tech Stack:** Markdown, YAML frontmatter, Git, Cursor Agent Skills

**Spec:** `docs/superpowers/specs/2026-05-24-project-wiki-design.md`

---

## File Map

| File | Responsibility |
|------|----------------|
| `AGENTS.md` | Portable schema: structure, naming, page formats, four workflows |
| `README.md` | Human quickstart: clone → research → handoff |
| `raw/llm/.gitkeep` | Placeholder for LLM chat exports |
| `raw/web/.gitkeep` | Placeholder for web article clips |
| `raw/llm/2026-05-24-claude-auth-patterns.example.md` | Example LLM raw source (pending) |
| `raw/web/nextjs-app-router-docs.example.md` | Example web raw source (pending) |
| `wiki/index.md` | Content catalog seed |
| `wiki/log.md` | Chronological audit trail seed |
| `wiki/synthesis/evolving-thesis.md` | Running synthesis seed |
| `wiki/sources/.gitkeep` | Placeholder for source summary pages |
| `wiki/concepts/.gitkeep` | Placeholder for concept pages |
| `.cursor/skills/wiki-ingest/SKILL.md` | Ingest one raw source workflow |
| `.cursor/skills/wiki-query/SKILL.md` | Query wiki with citations workflow |
| `.cursor/skills/wiki-lint/SKILL.md` | Health-check wiki workflow |
| `.cursor/skills/wiki-export-brief/SKILL.md` | Generate frozen project brief workflow |

---

### Task 1: Initialize Git Repo and Directory Scaffold

**Files:**
- Create: `raw/llm/.gitkeep`, `raw/web/.gitkeep`, `wiki/sources/.gitkeep`, `wiki/concepts/.gitkeep`, `wiki/synthesis/.gitkeep`
- Create: `.gitignore`

- [ ] **Step 1: Initialize git repo**

```bash
cd /Users/william.jiang/my-wiki/project-wiki
git init
```

Expected: `Initialized empty Git repository`

- [ ] **Step 2: Create directory scaffold**

```bash
mkdir -p raw/llm raw/web wiki/sources wiki/concepts wiki/synthesis .cursor/skills
touch raw/llm/.gitkeep raw/web/.gitkeep wiki/sources/.gitkeep wiki/concepts/.gitkeep wiki/synthesis/.gitkeep
```

- [ ] **Step 3: Create .gitignore**

Create `.gitignore`:

```
.DS_Store
.obsidian/workspace.json
.obsidian/workspace-mobile.json
```

- [ ] **Step 4: Verify scaffold**

```bash
find . -type d | sort
```

Expected directories include: `./raw/llm`, `./raw/web`, `./wiki/sources`, `./wiki/concepts`, `./wiki/synthesis`, `./.cursor/skills`

- [ ] **Step 5: Commit**

```bash
git add .gitignore raw/ wiki/ .cursor/
git commit -m "$(cat <<'EOF'
chore: scaffold project wiki directory structure

EOF
)"
```

---

### Task 2: Write AGENTS.md Schema

**Files:**
- Create: `AGENTS.md`

- [ ] **Step 1: Write AGENTS.md**

Create `AGENTS.md` with this content:

```markdown
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
```

- [ ] **Step 2: Verify AGENTS.md exists and contains all four workflows**

```bash
grep -c "Workflow: Ingest\|Workflow: Query\|Workflow: Lint\|Workflow: Export Brief" AGENTS.md
```

Expected: `4`

- [ ] **Step 3: Commit**

```bash
git add AGENTS.md
git commit -m "$(cat <<'EOF'
docs: add AGENTS.md wiki maintainer schema

EOF
)"
```

---

### Task 3: Write Seed Wiki Files

**Files:**
- Create: `wiki/index.md`, `wiki/log.md`, `wiki/synthesis/evolving-thesis.md`

- [ ] **Step 1: Create wiki/index.md**

```markdown
# Wiki Index

> Catalog of all wiki pages. Updated on every ingest.

## Sources

_(none yet)_

## Concepts

_(none yet)_

## Synthesis

- [[evolving-thesis]] — running synthesis of all ingested research
- [[project-brief]] — frozen handoff doc (generated at export)
```

- [ ] **Step 2: Create wiki/log.md**

```markdown
# Wiki Log

> Append-only timeline of wiki operations.

## [2026-05-24] init | project wiki created

Initialized project wiki from project-wiki template.
```

- [ ] **Step 3: Create wiki/synthesis/evolving-thesis.md**

```markdown
---
type: synthesis
status: evolving
last_updated: 2026-05-24
sources_ingested: 0
---

# Evolving Thesis

> Running synthesis across all ingested sources. Updated after every ingest.

## Current Understanding

_No sources ingested yet. Add raw files to `raw/llm/` or `raw/web/` and run ingest._

## Open Questions

_(to be filled as research progresses)_

## Emerging Decisions

_(to be filled as consensus forms)_
```

- [ ] **Step 4: Verify seed files**

```bash
test -f wiki/index.md && test -f wiki/log.md && test -f wiki/synthesis/evolving-thesis.md && echo "OK"
```

Expected: `OK`

- [ ] **Step 5: Commit**

```bash
git add wiki/index.md wiki/log.md wiki/synthesis/evolving-thesis.md
git commit -m "$(cat <<'EOF'
docs: add seed wiki index, log, and evolving thesis

EOF
)"
```

---

### Task 4: Write Example Raw Source Files

**Files:**
- Create: `raw/llm/2026-05-24-claude-auth-patterns.example.md`
- Create: `raw/web/nextjs-app-router-docs.example.md`

- [ ] **Step 1: Create example LLM raw source**

Create `raw/llm/2026-05-24-claude-auth-patterns.example.md`:

```markdown
---
type: llm-chat
source: claude
topic: "auth patterns for SaaS MVP"
date: 2026-05-24
status: pending
question: "What auth approach should I use for a B2B SaaS MVP built with Next.js?"
---

# Claude — Auth Patterns for SaaS MVP

## Recommendation

Use **Clerk** for a B2B SaaS MVP. Fastest time-to-ship, good Next.js App Router integration, handles org/team features out of the box.

## Key Points

- Don't roll your own auth for an MVP — security mistakes are costly
- JWT + refresh tokens are sufficient for API auth once users are authenticated via Clerk
- Watch out for SSR cookie handling with Next.js App Router middleware
- Auth0 is powerful but overkill for early-stage MVPs (complex pricing, steep setup)

## Alternatives Mentioned

- **NextAuth**: Good if self-hosting is required, but more setup than Clerk
- **Supabase Auth**: Viable if already using Supabase for database
- **Auth0**: Enterprise-grade but heavy for MVP stage
```

- [ ] **Step 2: Create example web raw source**

Create `raw/web/nextjs-app-router-docs.example.md`:

```markdown
---
type: web-article
source: web
topic: "Next.js App Router documentation"
date: 2026-05-24
status: pending
url: "https://nextjs.org/docs/app"
---

# Next.js App Router — Key Concepts

## Server Components

Default in App Router. Components render on the server unless marked `"use client"`.

## Middleware

Runs before routes. Used for auth checks, redirects, and header manipulation. Important for protecting routes and handling session cookies.

## Route Handlers

API endpoints in `app/api/` directory. Replace Pages Router `pages/api/`.

## Relevance to Auth

Middleware is the primary integration point for session-based auth providers (Clerk, Auth0, NextAuth) in App Router apps.
```

- [ ] **Step 3: Verify example files have required frontmatter**

```bash
grep -l "status: pending" raw/llm/*.example.md raw/web/*.example.md | wc -l
```

Expected: `2`

- [ ] **Step 4: Commit**

```bash
git add raw/llm/2026-05-24-claude-auth-patterns.example.md raw/web/nextjs-app-router-docs.example.md
git commit -m "$(cat <<'EOF'
docs: add example raw source files for LLM and web ingest

EOF
)"
```

---

### Task 5: Write README Quickstart

**Files:**
- Create: `README.md`

- [ ] **Step 1: Create README.md**

```markdown
# project-wiki

A per-project research wiki based on [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). Capture multi-LLM research, distill into a compounding wiki, export a project brief for dev handoff.

## Quick Start

### 1. Clone for your project

```bash
git clone <this-repo-url> my-project-wiki
cd my-project-wiki
```

### 2. Add raw sources

**LLM chats** — copy-paste into `raw/llm/`:

```
raw/llm/2026-05-24-claude-auth-patterns.md
raw/llm/2026-05-24-chatgpt-auth-patterns.md
raw/llm/2026-05-24-gemini-auth-patterns.md
```

Use the frontmatter template from `AGENTS.md`. Set `status: pending`.

**Web articles** — clip with Obsidian Web Clipper into `raw/web/`.

See `.example.md` files for format reference.

### 3. Ingest sources (one at a time)

In Cursor (or any agent reading `AGENTS.md`):

```
ingest 2026-05-24-claude-auth-patterns.md
```

Or attach the `wiki-ingest` skill. Review updates in `wiki/` before confirming.

### 4. Query and lint

```
What auth provider should we use?
lint the wiki
```

### 5. Export brief when ready to build

```
export brief
```

Review `wiki/synthesis/project-brief.md`. Approve to freeze.

### 6. Hand off to dev repo

```bash
# In dev repo
git init my-saas-app && cd my-saas-app
mkdir docs
cp ../my-project-wiki/wiki/synthesis/project-brief.md docs/PROJECT_BRIEF.md
git submodule add <my-project-wiki-repo-url> wiki
```

Open dev repo in Cursor. Start with `/brainstorming` using `docs/PROJECT_BRIEF.md`.

## Structure

```
raw/llm/              LLM chat exports
raw/web/              Web article clips
wiki/sources/         Per-source summaries
wiki/concepts/        Cross-linked topic pages
wiki/synthesis/       evolving-thesis.md + project-brief.md
wiki/index.md         Page catalog
wiki/log.md           Operation timeline
AGENTS.md             Agent schema (portable)
.cursor/skills/       Cursor workflow skills
```

## Cursor Skills

| Skill | Trigger |
|-------|---------|
| `wiki-ingest` | Process one pending raw source |
| `wiki-query` | Answer from wiki with citations |
| `wiki-lint` | Health-check the wiki |
| `wiki-export-brief` | Generate frozen project brief |

## References

- [Design spec](docs/superpowers/specs/2026-05-24-project-wiki-design.md)
- [Karpathy LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "$(cat <<'EOF'
docs: add README quickstart for project wiki workflow

EOF
)"
```

---

### Task 6: Create wiki-ingest Skill

**Files:**
- Create: `.cursor/skills/wiki-ingest/SKILL.md`

- [ ] **Step 1: Write wiki-ingest skill**

Create `.cursor/skills/wiki-ingest/SKILL.md`:

```markdown
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
```

- [ ] **Step 2: Verify skill file**

```bash
test -f .cursor/skills/wiki-ingest/SKILL.md && grep -q "name: wiki-ingest" .cursor/skills/wiki-ingest/SKILL.md && echo "OK"
```

Expected: `OK`

- [ ] **Step 3: Commit**

```bash
git add .cursor/skills/wiki-ingest/
git commit -m "$(cat <<'EOF'
feat: add wiki-ingest cursor skill

EOF
)"
```

---

### Task 7: Create wiki-query Skill

**Files:**
- Create: `.cursor/skills/wiki-query/SKILL.md`

- [ ] **Step 1: Write wiki-query skill**

Create `.cursor/skills/wiki-query/SKILL.md`:

```markdown
---
name: wiki-query
description: Answer a question using the project wiki with citations. Use when the user asks about project research, decisions, or synthesized knowledge.
---

# Wiki Query

Answer questions from the wiki, not from raw sources or general knowledge.

## Steps

1. **Read** `wiki/index.md` to locate relevant pages
2. **Read** the identified wiki pages (prefer wiki/ over raw/)
3. **Synthesize** an answer with `[[wikilink]]` citations to specific concept and source pages
4. **Assess** whether the answer adds new knowledge not already in the wiki
5. If valuable and new → **offer** to file as a new `wiki/concepts/<slug>.md` page, update index and log

## Guardrails

- Read index.md FIRST — do not grep raw/ directory
- Cite wikilinks, not vague references
- Do not answer from general knowledge when wiki pages exist on the topic
- Good answers compound — offer to file insights that would be lost in chat history
```

- [ ] **Step 2: Verify skill file**

```bash
test -f .cursor/skills/wiki-query/SKILL.md && grep -q "name: wiki-query" .cursor/skills/wiki-query/SKILL.md && echo "OK"
```

Expected: `OK`

- [ ] **Step 3: Commit**

```bash
git add .cursor/skills/wiki-query/
git commit -m "$(cat <<'EOF'
feat: add wiki-query cursor skill

EOF
)"
```

---

### Task 8: Create wiki-lint Skill

**Files:**
- Create: `.cursor/skills/wiki-lint/SKILL.md`

- [ ] **Step 1: Write wiki-lint skill**

Create `.cursor/skills/wiki-lint/SKILL.md`:

```markdown
---
name: wiki-lint
description: Health-check the project wiki for contradictions, orphans, and sync issues. Use when the user says "lint the wiki" or after several ingests.
---

# Wiki Lint

Report wiki health issues. Fix only what the user approves.

## Checks

1. **Contradictions** — conflicting claims across concept pages
2. **Stale claims** — older source claims not updated after newer sources ingested
3. **Orphan pages** — wiki pages with no inbound `[[wikilinks]]` from other wiki pages
4. **Missing pages** — wikilinks pointing to non-existent pages
5. **Pending raw files** — files in raw/ with `status: pending`
6. **Index sync** — pages on disk but missing from `wiki/index.md`
7. **Missing cross-references** — related concept pages not linking to each other

## Steps

1. Scan all files in `wiki/sources/`, `wiki/concepts/`, `wiki/synthesis/`
2. Cross-reference with `wiki/index.md` and wikilinks across pages
3. Scan `raw/` for pending files
4. **Report** findings as a structured list with severity (error / warning / info)
5. **Do not fix** unless user approves specific items
6. After approved fixes, append to log: `## [YYYY-MM-DD] lint | <N> issues found, <M> fixed`

## Output Format

```markdown
## Wiki Lint Report

### Errors
- ...

### Warnings
- ...

### Info
- ...

### Pending Ingests
- raw/llm/2026-05-24-chatgpt-auth-patterns.md (pending)
```
```

- [ ] **Step 2: Verify skill file**

```bash
test -f .cursor/skills/wiki-lint/SKILL.md && grep -q "name: wiki-lint" .cursor/skills/wiki-lint/SKILL.md && echo "OK"
```

Expected: `OK`

- [ ] **Step 3: Commit**

```bash
git add .cursor/skills/wiki-lint/
git commit -m "$(cat <<'EOF'
feat: add wiki-lint cursor skill

EOF
)"
```

---

### Task 9: Create wiki-export-brief Skill

**Files:**
- Create: `.cursor/skills/wiki-export-brief/SKILL.md`

- [ ] **Step 1: Write wiki-export-brief skill**

Create `.cursor/skills/wiki-export-brief/SKILL.md`:

```markdown
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
```

- [ ] **Step 2: Verify skill file**

```bash
test -f .cursor/skills/wiki-export-brief/SKILL.md && grep -q "name: wiki-export-brief" .cursor/skills/wiki-export-brief/SKILL.md && echo "OK"
```

Expected: `OK`

- [ ] **Step 3: Commit**

```bash
git add .cursor/skills/wiki-export-brief/
git commit -m "$(cat <<'EOF'
feat: add wiki-export-brief cursor skill

EOF
)"
```

---

### Task 10: End-to-End Verification

**Files:**
- Verify: all deliverables from spec

- [ ] **Step 1: Verify complete file tree**

```bash
cd /Users/william.jiang/my-wiki/project-wiki
required_files=(
  AGENTS.md
  README.md
  .gitignore
  wiki/index.md
  wiki/log.md
  wiki/synthesis/evolving-thesis.md
  raw/llm/2026-05-24-claude-auth-patterns.example.md
  raw/web/nextjs-app-router-docs.example.md
  .cursor/skills/wiki-ingest/SKILL.md
  .cursor/skills/wiki-query/SKILL.md
  .cursor/skills/wiki-lint/SKILL.md
  .cursor/skills/wiki-export-brief/SKILL.md
)
missing=0
for f in "${required_files[@]}"; do
  if [ ! -f "$f" ]; then echo "MISSING: $f"; missing=$((missing+1)); fi
done
if [ "$missing" -eq 0 ]; then echo "All ${#required_files[@]} required files present"; else echo "$missing missing"; fi
```

Expected: `All 12 required files present`

- [ ] **Step 2: Verify four workflows documented in AGENTS.md**

```bash
grep -c "^## Workflow:" AGENTS.md
```

Expected: `4`

- [ ] **Step 3: Verify four skills present**

```bash
ls .cursor/skills/*/SKILL.md | wc -l
```

Expected: `4`

- [ ] **Step 4: Manual smoke test — ingest example file**

Rename example to active file and run ingest in Cursor:

```bash
cp raw/llm/2026-05-24-claude-auth-patterns.example.md raw/llm/2026-05-24-claude-auth-patterns.md
```

In Cursor with `wiki-ingest` skill: `ingest 2026-05-24-claude-auth-patterns.md`

Verify after ingest:
- `wiki/sources/claude-auth-patterns.md` exists
- `wiki/index.md` lists the source
- `wiki/log.md` has ingest entry
- `raw/llm/2026-05-24-claude-auth-patterns.md` has `status: ingested`

- [ ] **Step 5: Final commit (if smoke test created wiki pages)**

```bash
git add -A
git status
git commit -m "$(cat <<'EOF'
chore: complete project wiki template v1

EOF
)" 
```

Only commit if there are staged changes from smoke test or prior uncommitted work.

---

## Spec Coverage Checklist

| Spec Requirement | Task |
|------------------|------|
| Directory template | Task 1 |
| AGENTS.md with four workflows | Task 2 |
| Seed index, log, evolving-thesis | Task 3 |
| Example raw files (LLM + web) | Task 4 |
| README quickstart | Task 5 |
| wiki-ingest skill | Task 6 |
| wiki-query skill | Task 7 |
| wiki-lint skill | Task 8 |
| wiki-export-brief skill | Task 9 |
| Verification | Task 10 |

All v1 deliverables covered. Out-of-scope items (qmd, Obsidian, CLI, web UI) intentionally excluded.
