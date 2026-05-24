---
name: wiki-lint
description: Health-check the project wiki for contradictions, orphans, and sync issues. Use when the user says "lint the wiki" or after several ingests.
---

# Wiki Lint

Report wiki health issues. Fix only what the user approves.

## Checks

### Errors (raw layer)

1. **Frontmatter schema** — every file in `raw/` must have `type`, `source`, `topic`, `date`, `status`; plus `question` (llm-chat) or `url` (web-article). Flag Obsidian-only fields (`title`, `created`, `tags`) without required keys.
2. **Misplaced raw files** — `type: llm-chat` (or chat-shaped content) in `raw/web/`; `type: web-article` in `raw/llm/`.
3. **Invalid filenames** — spaces; LLM files not matching `YYYY-MM-DD-<provider>-<topic-slug>.md`.
4. **Ingested but invalid** — `status: ingested` on files that fail schema or placement checks.

### Errors (wiki integrity)

5. **Missing pages** — wikilinks pointing to non-existent pages
6. **Index sync** — pages on disk but missing from `wiki/index.md`

### Warnings (staleness after multi-source ingest)

7. **Stale concept pages** — `sources` frontmatter lists fewer slugs than relevant ingested sources; Divergence/Decision contains `_(single source)_`, `_(pending)_`, or outdated single-provider text when 2+ sources exist
8. **Synthesis gaps** — concepts referenced heavily in source pages or index but absent from `evolving-thesis.md` wikilinks
9. **Weak cross-references** — related concepts (same source summaries, shared topics) not linked to each other; one-way links where bidirectional is expected
10. **Low inbound links** — concept with ≤1 inbound wikilink from pages other than `index.md`
11. **Unresolved source contradictions** — source `## Contradictions` still open while a concept **Decision** documents resolution (e.g. `[[wiki-vs-context-engine]]`)

### Info

12. **Contradictions** — conflicting claims across concept pages not yet decided
13. **Orphan pages** — wiki pages with no inbound wikilinks
14. **Pending raw files** — `status: pending` in `raw/`

## Steps

1. Scan all files in `raw/llm/` and `raw/web/` — validate frontmatter, placement, filenames
2. Count ingested sources; scan `wiki/sources/`, `wiki/concepts/`, `wiki/synthesis/`
3. Cross-reference concept `sources` frontmatter vs actual source pages
4. Cross-reference `wiki/index.md` and wikilinks across pages
5. Check `evolving-thesis.md` for links to concepts that appear in 2+ source summaries or have **Decision** sections
6. **Report** findings with severity (error / warning / info)
7. **Do not fix** unless user approves specific items
8. After approved fixes, append to log: `## [YYYY-MM-DD] lint | <N> issues found, <M> fixed`

## Fix guidance (when user approves)

| Issue | Fix |
|-------|-----|
| Schema mismatch | Normalize frontmatter per AGENTS.md; map Obsidian `title`→`topic`, `created`→`date` |
| Misplaced LLM chat | Move to `raw/llm/`, rename, update source page `raw:` path |
| Stale concept | Expand `sources`, refresh Divergence table, resolve or update Decision |
| Synthesis gap | Add `[[concept-slug]]` to `evolving-thesis.md` |
| Resolved contradiction | Add resolution note + wikilink on source page Contradictions |

## Output Format

```markdown
## Wiki Lint Report

### Errors
- Raw frontmatter schema mismatch — `raw/web/foo.md`: Obsidian fields only; missing `type`, `topic`
- Misplaced raw files — `raw/web/bar.md`: llm-chat content in raw/web/

### Warnings
- Stale concept pages — [[context-fragmentation]]: sources frontmatter [chatgpt] only; Divergence says "single source"
- Synthesis gaps — [[multi-pass-distillation]] not linked from evolving-thesis.md

### Info
- ...

### Pending Ingests
- raw/llm/2026-05-24-chatgpt-auth-patterns.md (pending)
```
