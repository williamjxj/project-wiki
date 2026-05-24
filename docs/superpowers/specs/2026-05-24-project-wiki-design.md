# Project Wiki Design Spec

**Date:** 2026-05-24  
**Status:** Approved  
**Repo:** `init-wiki` → per-project wiki template

## Summary

A per-project implementation of [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) for the research phase before software development. Multiple LLM conversations and web sources are ingested into a persistent, interlinked markdown wiki. When research is complete, a frozen `project-brief.md` and git submodule hand off context to a separate dev repo (Cursor, VS Code, etc.) for spec/plan/implement workflows.

## Goals

1. Capture multi-LLM research (Claude, ChatGPT, Gemini) without losing unique insights or hiding contradictions
2. Distill scattered chat exports into a compounding wiki — not one-off summaries
3. Produce a canonical, feasible `project-brief.md` as the primary handoff artifact
4. Link full wiki context into the dev repo via git submodule
5. Remain agent-agnostic via `AGENTS.md`; optional Cursor skills for workflow rigidity

## Non-Goals (v1)

- Web app or summarizer service
- Automated LLM chat export
- Embedding/RAG infrastructure or qmd search
- Obsidian vault config or plugins
- CLI tools
- Persistent cross-project personal wiki (each project gets its own wiki repo)

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Scope | Per-project wiki | Fresh knowledge base per idea; archived when dev starts |
| Agent | Agent-agnostic `AGENTS.md` | Works with Cursor, Claude Code, Codex, web chat |
| Handoff | Git submodule + brief copy | Dev repo starts from brief; full wiki available on demand |
| Source capture | Manual paste (LLM) + clipper (web) | No automation needed for v1 |
| Approach | Template + agent skills (Approach B) | Reliability without building an app |

## Architecture

Three layers (Karpathy pattern, project-scoped):

| Layer | Location | Owner | Mutability |
|-------|----------|-------|------------|
| Raw sources | `raw/` | Human curates | Immutable after ingest |
| Wiki | `wiki/` | LLM maintains | Updated on ingest/query/lint |
| Schema | `AGENTS.md` | Human + LLM co-evolve | Updated when conventions change |

### End-to-End Flow

```
Phase 1: Discovery
  Claude/ChatGPT/Gemini chats → raw/llm/  (manual paste)
  Web articles                → raw/web/  (Obsidian Web Clipper)

Phase 2: Wiki (this repo)
  Ingest skill → wiki/sources/, wiki/concepts/, synthesis/evolving-thesis.md
  Query/Lint   → compound knowledge, health-check
  Export brief → synthesis/project-brief.md (frozen)

Phase 3: Dev (separate repo)
  Copy brief → docs/PROJECT_BRIEF.md
  Submodule  → wiki/ (read-only reference)
  Cursor     → /brainstorming → plan → implement
```

## Directory Structure

```
<project-name>-wiki/
├── AGENTS.md                    # Schema: structure, conventions, workflows
├── README.md                    # Human quickstart (clone → research → handoff)
├── raw/
│   ├── llm/                     # Manual paste from Claude/ChatGPT/Gemini
│   │   └── YYYY-MM-DD-<provider>-<topic-slug>.md
│   └── web/                     # Obsidian Web Clipper / saved articles
│       └── <article-slug>.md
├── wiki/
│   ├── index.md                 # Content catalog (updated every ingest)
│   ├── log.md                   # Append-only timeline
│   ├── sources/                 # One page per ingested raw file
│   │   └── <source-slug>.md
│   ├── concepts/                # Cross-linked topic/entity/decision pages
│   │   └── <concept-slug>.md
│   └── synthesis/
│       ├── evolving-thesis.md   # Running synthesis (updated each ingest)
│       └── project-brief.md     # Frozen handoff doc (generated at export)
└── .cursor/skills/              # Optional workflow accelerators
    ├── wiki-ingest/
    ├── wiki-query/
    ├── wiki-lint/
    └── wiki-export-brief/
```

### Dev Repo Layout (after handoff)

```
my-saas-app/
├── docs/
│   └── PROJECT_BRIEF.md         # Copied from wiki/synthesis/project-brief.md
├── wiki/                        # git submodule → <project-name>-wiki repo
└── AGENTS.md                    # Dev agent schema (Cursor skills, MCP, etc.)
```

## Naming Conventions

- **Raw LLM files:** `2026-05-24-claude-auth-patterns.md` — date, provider, topic slug
- **Raw web files:** `nextjs-app-router-docs.md` — descriptive slug
- **Wiki pages:** kebab-case slugs; wikilinks between pages (`[[auth-patterns]]`)
- **Log entries:** `## [2026-05-24] ingest | claude-auth-patterns` — parseable prefix

## Raw Source Format

Every file in `raw/` requires YAML frontmatter:

```yaml
---
type: llm-chat | web-article
source: claude | chatgpt | gemini | web
topic: "auth patterns for SaaS MVP"
date: 2026-05-24
status: pending | ingested
question: "What auth approach for a B2B SaaS MVP?"   # llm-chat only
url: "https://..."                                     # web-article only
---
```

Agent sets `status: ingested` after processing. Files with `status: pending` are the ingest queue.

## AGENTS.md Workflows

### Ingest (one source at a time)

**Trigger:** User says "ingest `<filename>`" or "process pending sources"

1. Read raw file from `raw/llm/` or `raw/web/`
2. Discuss key takeaways with user
3. Create/update `wiki/sources/<slug>.md`
4. Update relevant `wiki/concepts/` pages — cross-link, merge duplicates, flag contradictions
5. Update `wiki/synthesis/evolving-thesis.md`
6. Update `wiki/index.md`
7. Append entry to `wiki/log.md`
8. Set raw file frontmatter `status: ingested`

**Rule:** Never modify content inside `raw/` files (only update frontmatter `status`).

### Query

**Trigger:** User asks a question about project research

1. Read `wiki/index.md` to locate relevant pages
2. Read those pages (not raw sources unless citation needed)
3. Synthesize answer with wikilink citations
4. If answer is valuable and new → file as new `wiki/concepts/` page; update index/log

### Lint

**Trigger:** User says "lint the wiki" or after every 3–5 ingests

Checks:
- Contradictions between concept pages
- Stale claims superseded by newer sources
- Orphan pages (no inbound wikilinks)
- Concepts mentioned but lacking their own page
- Missing cross-references
- Raw files still `status: pending`
- `index.md` out of sync with actual pages

Output: Report to user; fix only what user approves; log the lint pass.

### Export Brief

**Trigger:** User says "export brief" or "ready to build"

1. Run lint first (must pass or user acknowledges warnings)
2. Generate `wiki/synthesis/project-brief.md` from `evolving-thesis.md` + concept pages
3. Present brief to user for review/edits
4. On approval → set frontmatter `status: frozen`

## Page Formats

### Source Page (`wiki/sources/`)

```markdown
---
type: source-summary
raw: raw/llm/2026-05-24-claude-auth-patterns.md
source: claude
date: 2026-05-24
---

# Auth Patterns — Claude Research

## Key Claims
- Clerk is fastest for MVP [[auth-providers]]
- JWT + refresh tokens sufficient for B2B [[token-strategy]]

## Unique Insights
- Claude specifically warned about SSR cookie handling with Next.js App Router

## Contradictions
- ChatGPT recommended Auth0; Claude says overkill for MVP → see [[auth-provider-decision]]
```

### Concept Page (`wiki/concepts/`)

```markdown
---
type: concept
sources: [claude-auth-patterns, chatgpt-auth-patterns, gemini-auth-patterns]
last_updated: 2026-05-24
---

# Auth Provider Decision

## Consensus
All three LLMs agree: use a managed provider for MVP, not roll-your-own.

## Divergence
| Provider | Claude | ChatGPT | Gemini |
|----------|--------|---------|--------|
| Clerk    | ✅ Recommended | Mentioned | ✅ Recommended |
| Auth0    | ❌ Overkill | ✅ Recommended | — |
| NextAuth | — | Mentioned | ✅ If self-hosting |

## Decision
→ Clerk (fastest setup, good Next.js integration)
```

### Project Brief (`wiki/synthesis/project-brief.md`)

```markdown
---
type: project-brief
status: frozen
date: 2026-05-24
sources_ingested: 5
---

# Project Brief: My SaaS App

## Problem
...

## Chosen Approach
...

## Constraints
...

## Non-Goals
...

## Rejected Alternatives
...

## Open Questions
...
```

## Agent Skills

Four Cursor skills mirror AGENTS.md workflows. Skills enforce rigidity; AGENTS.md is the portable fallback for non-Cursor agents.

| Skill | Purpose | Key Guardrails |
|-------|---------|----------------|
| `wiki-ingest` | Process one raw source | One file per invocation; update index + log; never modify raw body |
| `wiki-query` | Answer from wiki | Read index first; cite wikilinks; offer to file answer as new page |
| `wiki-lint` | Health check | Report-only by default; fix only with user approval |
| `wiki-export-brief` | Generate handoff doc | Lint first; present draft for approval before freezing |

Each skill is a `SKILL.md` referencing AGENTS.md as source of truth — no duplicate logic.

## Handoff Protocol

When research is complete:

1. **Export brief** — run "export brief" in wiki repo
2. **Review & approve** — edit `project-brief.md` until satisfied
3. **Create dev repo** — `git init my-saas-app`
4. **Copy brief** — `cp wiki/synthesis/project-brief.md ../my-saas-app/docs/PROJECT_BRIEF.md`
5. **Add submodule** — `cd my-saas-app && git submodule add <wiki-repo-url> wiki`
6. **Archive wiki** — tag wiki repo: `v1.0-research-complete`
7. **Start dev** — open dev repo in Cursor with `PROJECT_BRIEF.md`; run `/brainstorming`

**Dev agent context priority:**
1. `docs/PROJECT_BRIEF.md` — primary (problem, approach, constraints, non-goals)
2. `wiki/` submodule — drill-down for details, rejected alternatives, source attribution
3. Dev repo `AGENTS.md` + skills — implementation workflows

Wiki repo stops receiving ingests after export. To resume research mid-build: re-open wiki, ingest new sources, re-export brief, `git submodule update` in dev repo.

## Error Handling

| Scenario | Handling |
|----------|----------|
| Duplicate info across LLM exports | Merge into existing concept pages; source page preserves attribution |
| Contradicting recommendations | Flag in concept page comparison table; don't silently pick a winner |
| User skips ingest review | Skill prompts for confirmation before marking ingested |
| Re-ingest same raw file | Block if `status: ingested`; create new raw file for updated chat |
| Wiki grows large mid-research | `index.md` sufficient up to ~100 pages; add qmd later if needed |
| Research resumes after dev started | Re-open wiki, ingest, re-export, update submodule pointer |
| Agent drift (ignores AGENTS.md) | Skills re-enforce; lint catches index/log sync issues |

## Verification (v1)

Workflow-based checks — no automated test suite:

| Check | How |
|-------|-----|
| Template bootstraps | Clone `init-wiki`; directory structure + AGENTS.md present |
| Ingest works | Drop sample raw file → ingest → source page + index + log updated |
| Multi-source synthesis | Ingest 2 LLM exports on same topic → concept page shows comparison |
| Query compounds | Ask question → answer filed as new wiki page |
| Lint catches issues | Create orphan page → lint flags it |
| Export produces brief | Export → `project-brief.md` self-contained without reading raw/ |
| Handoff works | Submodule + brief copy into empty dev repo → Cursor brainstorms from brief alone |

## v1 Deliverables

**In scope:**
- Complete directory template
- `AGENTS.md` with all four workflows
- Raw source frontmatter template + example files (one LLM, one web)
- Four Cursor skills (`wiki-ingest`, `wiki-query`, `wiki-lint`, `wiki-export-brief`)
- `README.md` quickstart
- Seed `wiki/index.md`, `wiki/log.md`, `wiki/synthesis/evolving-thesis.md`

**Out of scope:**
- qmd search / MCP integration
- Obsidian vault config
- Automated LLM chat export
- CLI tools
- Web UI

## References

- [Karpathy LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [Karpathy tweet: LLM Knowledge Bases](https://x.com/karpathy/status/2039805659525644595)
- [LLM-Wiki-Skilled (skills-based implementation)](https://github.com/TrueHOOHA/LLM-Wiki-Skilled)
