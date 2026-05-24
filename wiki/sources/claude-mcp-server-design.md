---
type: source-summary
raw: raw/llm/2026-05-23-claude-mcp-server-design.md
source: claude
date: 2026-05-23
---

# MCP Server Design

## Key Claims

- Standalone stdio FastMCP with 4 tools: wiki_search, wiki_ingest, wiki_get_page, wiki_stats.
- /chat omitted — IDE already is the LLM.
- Shared memory_api service layer; HTTP routes delegate to same functions.
- Avoid uvicorn + MCP ingest concurrently (two workers, same artifacts).
- wiki_search: hybrid default, limit 1–20, modes hybrid|keyword|semantic.
- summarize stays HTTP-only.

## Unique Insights

- Two entry points, one brain — MCP avoids HTTP hop but must share service layer.

## Contradictions

MCP-first vs Next.js chat priority tension with [[claude-frontend-admin-integration]] — see [[implementation-milestones]].

## Related sources

[[claude-mcp-server-plan]], [[implementation-milestones]], [[chatgpt-mem-weaver-v2-roadmap]]

Related concepts: [[implementation-milestones]] [[mem-weaver-architecture]] [[mem-weaver-known-gaps]]
