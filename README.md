# Project Wiki Template

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
