---
title: mcp-server
---

# MCP Server Integration

The `mcp-server` Python library or FastAPI extension serves as a thin wrapper to expose `/query`, `/ingest`, and `/chat` endpoints from your prompt harness, making MemWeaver a live memory layer for the IDE. This integration enhances coding efficiency by providing real-time access to relevant information.

The `mcp-server` can be easily integrated into the existing prompt harness to enable cursor-based calls to wiki searches during coding sessions. This integration enhances MemWeaver's functionality as a live memory layer for IDEs.

### Integration Instructions:
- Use existing FastAPI endpoints or the `mcp-server` Python library to integrate MCP servers with your prompt harness.