# Template Checklist

Use this before cloning `main` into a project-specific wiki branch.

## Main Branch Must Stay Pristine

- `raw/llm/` contains only `.gitkeep`
- `raw/web/` contains only `.gitkeep`
- `wiki/sources/` contains only `.gitkeep`
- `wiki/concepts/` contains only `.gitkeep`
- `wiki/synthesis/` contains only `.gitkeep` and `evolving-thesis.md`
- `wiki/index.md` has no project-specific sources or concepts
- `wiki/log.md` has only template-level entries
- No generated `wiki/synthesis/project-brief.md` exists on `main`
- No generated `wiki/synthesis/project-details.md` exists on `main`

## Project Branches May Add

- Raw LLM chats in `raw/llm/`
- Raw web clips in `raw/web/`
- Source summaries in `wiki/sources/`
- Concept pages in `wiki/concepts/`
- Export docs in `wiki/synthesis/project-brief.md` and `wiki/synthesis/project-details.md`

Project-specific research should never be merged back into `main`.
