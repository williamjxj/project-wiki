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
