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

## [2026-05-25] lint | weak cross-references, orphan wikilink fixed

Fixed 3 warnings: added `[[llm-wiki-paradigm]]` to mem-weaver-architecture Related, added `[[knowledge-governance]]` to mem-weaver-known-gaps Related, replaced orphan `[[TGLTommy]]` wikilink with plain text.

## [2026-05-25] ingest | rag-graphrag-to-llm-knowledge-runtime

Processed raw/web/rag-graphrag-to-llm-knowledge-runtime.md. First web source ingested. Created source page, created [[llm-wiki-paradigm]] and [[knowledge-governance]] concept pages, updated [[memory-synthesis-vs-rag]] with LLM Wiki paradigm comparison, updated [[evolving-thesis]] with knowledge governance gaps and hallucination write-back risk.

## [2026-05-29] export | synthesis cycle 2
Exported [[project-brief]] (cycle 2, 28 sources) and [[project-details]] (first-ever deep analysis) with `status: current`. Key additions vs cycle 1: as-built status table, firm/open decisions tables, comparison matrix across 5 providers, prioritized recommendations, and risk assessment. [[project-details]] adds source map, concept maturity table, deep analysis with epistemology and hallucination write-back risk, and 8-item recommendation roadmap.

## [2026-05-29] lint | 3 warnings: 3 fixed

Ran full lint pass. Findings and fixes:
- **W1 (HIGH)** — `mvp-scope.md` had duplicated sections (merge artifact). Merged into single Consensus/Divergence/Decision page.
- **W2 (MEDIUM)** — 9 core concepts missing from [[evolving-thesis]]: [[compounding-knowledge-layer]], [[decision-records]], [[implementation-readiness]], [[llm-outputs-as-synthetic-sources]], [[multi-pass-distillation]], [[mvp-scope]], [[purpose-steering]], [[semantic-deduplication]], [[wiki-vs-context-engine]]. Added wikilinks to Multi-LLM workflow and Pipeline operator sections.
- **W3 (LOW)** — [[llm-outputs-as-synthetic-sources]] had only 1 inbound link (≤1 threshold). Cross-linked from [[dual-llm-memory-pipeline]] and [[mem-weaver-architecture]].

All 3 warnings fixed.

## [2026-05-29] tracking fix | 4 orphaned sources registered
Reconciled 4 sources that had source pages and concept references but were missing from index.md, log.md, and evolving-thesis tracking: [[chatgpt-llm-based-project-workflow]], [[claude-multi-llm-research-synthesis-workflow]], [[gemini-llm-wiki-multi-agent]], [[2026-05-25-cluade-pipeline-plan]]. Updated index.md (External perspectives + Implementation specs), evolving-thesis (workflow section + pipeline operator section), and count (24→28).

## [2026-05-29] ingest | notebooklm-dual-llm-architecture-design
Processed raw/llm/2026-04-21-notebooklm-dual-llm-architecture-design.md. First NotebookLM source. Created source page, added to [[dual-llm-memory-pipeline]] and [[mem-weaver-architecture]], updated evolving-thesis with SQLite+FTS5 validation note.

## [2026-05-24] lint | 28 warnings found, 28 fixed

Applied all approved lint fixes:

- Audited `/Users/william.jiang/my-playgrounds/mem-weaver` — updated [[mem-weaver-as-built-status]] Decision
- Resolved [[dual-llm-memory-pipeline]] and [[agent-skills-taxonomy]] Decision sections
- Added [[agent-skills-taxonomy]] to [[evolving-thesis]]; refreshed Open Questions and Emerging Decisions
- Cross-linked all 7 concept pages
- Expanded [[implementation-milestones]] sources (+4 plan/integration sources)
- Added `## Related sources` sections to 17 source pages
- Updated 9 source `## Contradictions` sections with resolution notes
