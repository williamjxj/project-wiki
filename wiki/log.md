# Wiki Log

> Append-only timeline of wiki operations.

## [2026-05-24] init | project wiki created

Initialized project wiki from project-wiki template.

## [2026-05-24] ingest | chatgpt-llm-based-project-workflow

Processed `raw/llm/2026-05-24-chatgpt-llm-based-project-workflow.md`. Created source page and 10 concept pages. Updated evolving-thesis.

## [2026-05-24] ingest | gemini-llm-wiki-multi-agent

Processed `raw/llm/2026-05-24-gemini-llm-wiki-multi-agent.md`. Created source page and 4 concept pages. Updated 5 existing concepts with cross-source comparison.

## [2026-05-24] ingest | claude-multi-llm-research-synthesis-workflow

Processed `raw/llm/2026-05-24-claude-multi-llm-research-synthesis-workflow.md`. Created source page and 3 concept pages. Updated 10 existing concepts with 3-source comparison. Updated evolving-thesis to sources_ingested: 3.

## [2026-05-24] lint | 15 issues found, 15 fixed

Fixed: moved 3 raw files to `raw/llm/` with kebab-case names and AGENTS.md frontmatter; updated source page `raw:` paths; refreshed 9 stale concept pages with 3-source Decisions; added cross-links in evolving-thesis; resolved ChatGPT source Contradictions section; improved inbound links for purpose-steering and related concepts.

## [2026-05-24] export | project-brief cycle 1 (draft)

Generated `wiki/synthesis/project-brief.md` from 3 ingested sources. Status: draft — pending user approval.

## [2026-05-25] ingest | 2026-05-25-cluade-pipeline-plan

Processed raw/llm/2026-05-25-cluade-pipeline-plan.md via pipeline operator live test. Created source page; updated pipeline-operator and mvp-scope concepts; appended thesis delta.

## [2026-05-26] lint | index validation fixed, 23 warnings cleared

Fixed `_INDEX_ENTRY_RE` regex in `pipeline/wiki_core/lint.py` — was missing `re.MULTILINE` flag, causing `^` to only match string start. Lint falsely reported every page as `index_out_of_sync`. After fix: zero false positives.

Also reorganized `index.md`: moved `2026-05-25-cluade-pipeline-plan` to Sources and `pipeline-operator` to Concepts (both were only in Synthesis). Added wikilink from evolving-thesis to resolve orphan page. Bumped `sources_ingested` counters to 4 across brief and thesis.

## [2026-05-26] ingest | distill-ingest

Processed `raw/llm/2026-05-26-claude-distill-ingest.md`. Created source page. Updated evolving-thesis with thesis delta section. No new concept pages (user opted for source-only ingest).

## 2023-10-04 ingest | distill-canonical

## [2026-05-26] export | project-brief cycle 2
Approved project brief export.

## [2023-10-14] ingest | llm-web-api-context-token-management
- Ingested and summarized the document "LLM网页对话框与API调用：上下文及Token内存管理详解" comparing context handling between web interfaces and API calls.

## [2026-05-26] ingest | test-no-fm

- Status: pending
- Type: web-clip
- Source: web
- Date: 2026-05-26

## [2023-10-04] ingest | test-no-fm
- Frontmatter was detected as missing and auto-injected.
- The content appears straightforward, containing only a simple heading and some text.
- No specific concepts or insights were noted; however, the absence of frontmatter is notable.

## [2023-10-26] ingest | context-management-web-api
- Analysis created for `context-management-web-api` concept.

## [2023-10-16] ingest | distill-canon

Summary of the document outlining key claims, unique insights, and recommended updates to existing concepts such as `mcp-server`, `prompt-harness`, and `memweaver-integration`. This ensures MemWeaver's functionality is enhanced through MCP server integration and robust multi-source collection.

## [2026-05-26] export | project-brief cycle 3
Approved project brief export (auto-pipeline).
