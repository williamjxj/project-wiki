---
title: 'Distill Canonical'
date: 2023-10-16
type: source-summary
status: pending

## Key Claims:

1. **MCP Server Addition**: Integrate an MCP server into your prompt harness to enable cursor-based calls to wiki searches during coding sessions, enhancing MemWeaver's functionality as a live memory layer for IDEs.
2. **Multi-LLM Workflow**: Use multiple LLMs (Claude, ChatGPT, Gemini) to answer the same question and distill the best answers into a single `.md` file before ingesting it into MemWeaver for long-term searchability.
3. **Distillation Process**: Always distill chat logs rather than pasting them directly; this ensures cleaner, more useful content.

## Unique Insights:
- The MCP server can be easily integrated via existing FastAPI endpoints or the `mcp-server` Python library.
- The process of multi-source collection and distillation is critical for handling complex topics where different LLMs offer unique insights.
