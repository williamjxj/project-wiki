---
type: source-summary
raw: raw/llm/2026-05-26-claude-distill-canonical.md
source: claude
date: 2026-05-26
---

# Claude: Distill Canonical

## Key Claims

1. **Add MCP server to MemWeaver** — existing `/query`, `/ingest`, `/chat` FastAPI endpoints map directly to MCP tools, making the wiki a live IDE memory layer.
2. **Multi-LLM workflow discipline**: ask same question across LLMs → cherry-pick best answers → distill into single `.md` → drop in project root → ingest into MemWeaver. Never paste raw chat logs.
3. **Multi-source is worth it when**: topics are complex, architectural, or long-lived. Skip for simple one-off questions.
4. **Golden rule**: Collect → Distill → One canonical file → Ingest.

## Unique Insights

- Decision heuristic for multi-source collection: complex/architectural/long-lived topics benefit from triangulation across LLMs (Claude reasons better, GPT-4 has broader coverage, Gemini stronger on code). Simple one-off questions don't.
- MemWeaver-specific MCP integration path: existing endpoints are already MCP-compatible, just need a thin wrapper.
- Triangulation observation: different LLMs have genuinely different knowledge distributions — not just different phrasing.

## Contradictions

- Consistent with all earlier sources. This is a practical summary targeting the MemWeaver implementation specifically.
