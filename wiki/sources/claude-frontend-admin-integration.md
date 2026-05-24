---
type: source-summary
raw: raw/llm/2026-05-11-claude-frontend-admin-integration.md
source: claude
date: 2026-05-11
---

# Frontend & Admin Integration

## Key Claims

- Obsidian is immediate wiki UX over wiki/ folder — no extra dev for browse/edit/graph.
- Next.js chat UI with WikiSidebar; fork Vercel AI chatbot or OpenAI cookbook clones.
- Admin split: Obsidian plugins (Dataview, Tasks) vs custom Next admin for pipeline stats.
- Optional Metabase/Grafana if stats exposed via API.
- Auth: NextAuth (frontend) / FastAPI Users (backend multi-user).

## Unique Insights

- Don't rebuild Obsidian for markdown admin — use vault + plugins.

## Contradictions

Next.js chat emphasis vs MCP-first in [[chatgpt-mem-weaver-v2-roadmap]] — integration priority differs.

## Related sources

[[claude-chat-app-frontend-design]], [[implementation-milestones]], [[claude-architecture-inspiration]]

Related concepts: [[implementation-milestones]] [[mem-weaver-architecture]]
