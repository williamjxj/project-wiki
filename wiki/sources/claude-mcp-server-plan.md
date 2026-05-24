---
type: source-summary
raw: raw/llm/2026-05-23-claude-mcp-server-plan.md
source: claude
date: 2026-05-23
---

# MCP Server Plan

## Key Claims

- Ten-task rollout: fastmcp dep → memory_api → main.py delegation → mcp_server.py → tests → README + .cursor/mcp.json.example.
- enqueue_ingest raises IngestQueueFullError; MCP JSON error, HTTP 503.
- Slim results in MCP only; HTTP returns full pipeline rows.
- tests/test_memory_api.py + tests/test_mcp_server.py with FastMCP Client.

## Unique Insights

- Dual adapter pattern: same service, different error/response shapes.

## Contradictions

None.

## Related sources

[[claude-mcp-server-design]], [[implementation-milestones]], [[mem-weaver-as-built-status]]

Related concepts: [[implementation-milestones]]
