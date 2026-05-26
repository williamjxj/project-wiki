---
type: llm-chat
source: claude
topic: distill canonical
date: '2026-05-26'
status: ingested
question: what is distill canonical
---

Claude For Mem-Weaver:

---

**① MemWeaver — MCP vs Prompt Harness**

Your prompt harness is already solid (`.cursorrules`, `CLAUDE.md`, `AGENTS.md`). The real gap: **add MCP server**. Your `/query`, `/ingest`, and `/chat` FastAPI endpoints map perfectly to MCP tools. Once exposed, Cursor/Claude Code can call your wiki search mid-coding session — making MemWeaver a live memory layer for your IDE, not just a standalone app. Use `mcp-server` Python lib or FastAPI MCP extension — it's a thin wrapper on what you already have.

---

**② Multi-LLM → Coding Tools**

The workflow: ask the same architectural/design question across Claude, ChatGPT, Gemini → cherry-pick the best answers → distill into a single `.md` file → drop it in your project root. Cursor and Claude Code auto-read `CLAUDE.md` and `llms.txt` in the project directory. OpenCode reads `AGENTS.md`. Then `/ingest` that file into MemWeaver so it's searchable forever. Key discipline: **never paste raw chat logs** — always distill first.

---

**③ Is Multi-Source Collection Worth It?**

**Yes, when:** the topic is complex, architectural, or long-lived (e.g. "best RAG chunking strategy"). Different LLMs have genuinely different knowledge — Claude reasons better, GPT-4 has broader coverage, Gemini is stronger on code details. Triangulating gives you more robust decisions.

**Skip it when:** it's a simple one-off question, or you're collecting without distilling. Raw dumps = noise. The golden rule: **Collect → Distill → One canonical file → Ingest**. That's exactly what MemWeaver is designed to do — you're already on the right path.
