# Wiki Log

> Append-only timeline of wiki operations.

## [2026-05-24] init | project wiki created

Initialized project wiki from project-wiki template.

## [2026-05-24] ingest | batch — 22 raw/llm sources

Normalized frontmatter and filenames for all 22 files in `raw/llm/` (schema + `YYYY-MM-DD-<provider>-*.md` pattern). Created 22 source pages, 7 concept pages, updated [[evolving-thesis]] and [[index]].

Sources ingested (in research order):

1. `2026-04-21-claude-dual-llm-memory-pipeline.md` → [[claude-dual-llm-memory-pipeline]]
2. `2026-04-21-chatgpt-retrieval-vs-synthesis.md` → [[chatgpt-retrieval-vs-synthesis]]
3. `2026-05-15-gemini-llm-memory-research.md` → [[gemini-llm-memory-research]]
4. `2026-05-13-chatgpt-api-token-context-management.md` → [[chatgpt-api-token-context-management]]
5. `2026-05-11-claude-second-brain-prd.md` → [[claude-second-brain-prd]]
6. `2026-05-11-claude-second-brain-implementation.md` → [[claude-second-brain-implementation]]
7. `2026-04-22-claude-middleware-delegator-plan.md` → [[claude-middleware-delegator-plan]]
8. `2026-04-21-gemini-second-brain-design.md` → [[gemini-second-brain-design]]
9. `2026-05-11-claude-architecture-inspiration.md` → [[claude-architecture-inspiration]]
10. `2026-04-21-claude-fastapi-skeleton-design.md` → [[claude-fastapi-skeleton-design]]
11. `2026-04-21-claude-fastapi-skeleton-plan.md` → [[claude-fastapi-skeleton-plan]]
12. `2026-04-21-claude-milestone-b-typed-models-design.md` → [[claude-milestone-b-typed-models-design]]
13. `2026-04-21-claude-milestone-b-typed-models-plan.md` → [[claude-milestone-b-typed-models-plan]]
14. `2026-04-22-claude-phase-4-hardening-plan.md` → [[claude-phase-4-hardening-plan]]
15. `2026-05-11-claude-chat-app-frontend-design.md` → [[claude-chat-app-frontend-design]]
16. `2026-05-23-claude-mcp-server-design.md` → [[claude-mcp-server-design]]
17. `2026-05-23-claude-mcp-server-plan.md` → [[claude-mcp-server-plan]]
18. `2026-05-12-chatgpt-mem-weaver-v2-roadmap.md` → [[chatgpt-mem-weaver-v2-roadmap]]
19. `2026-05-15-claude-mem-weaver-competitive-analysis.md` → [[claude-mem-weaver-competitive-analysis]]
20. `2026-05-11-claude-frontend-admin-integration.md` → [[claude-frontend-admin-integration]]
21. `2026-05-15-claude-capability-checklist.md` → [[claude-capability-checklist]]
22. `2026-05-13-claude-mem-weaver-gaps.md` → [[claude-mem-weaver-gaps]]

Concept pages created/updated: [[dual-llm-memory-pipeline]], [[memory-synthesis-vs-rag]], [[mem-weaver-architecture]], [[agent-skills-taxonomy]], [[mem-weaver-known-gaps]], [[mem-weaver-as-built-status]], [[implementation-milestones]].

## [2026-05-24] lint | 28 warnings found, 28 fixed

Applied all approved lint fixes:

- Audited `/Users/william.jiang/my-playgrounds/mem-weaver` — updated [[mem-weaver-as-built-status]] Decision
- Resolved [[dual-llm-memory-pipeline]] and [[agent-skills-taxonomy]] Decision sections
- Added [[agent-skills-taxonomy]] to [[evolving-thesis]]; refreshed Open Questions and Emerging Decisions
- Cross-linked all 7 concept pages
- Expanded [[implementation-milestones]] sources (+4 plan/integration sources)
- Added `## Related sources` sections to 17 source pages
- Updated 9 source `## Contradictions` sections with resolution notes
