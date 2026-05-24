---
type: source-summary
raw: raw/llm/2026-05-11-claude-chat-app-frontend-design.md
source: claude
date: 2026-05-11
---

# Chat App Frontend Design

## Key Claims

- chat-app/ Next.js 14 App Router + Tailwind + shadcn/ui.
- SSE streaming POST /chat; Next route handler proxies SSE.
- Phase A: classify + retrieve + Ollama stream; Phase B: background wiki compile.
- WikiSidebar via GET /wiki/{slug}; SSE events: token, done, error.
- New modules: classifier, wiki_retriever, public_llm.

## Unique Insights

- Accumulate streamed text off critical React state to reduce re-renders.
- Browser → Next first; backend /wiki reads vault directly.

## Contradictions

None.

## Related sources

[[claude-second-brain-implementation]], [[claude-frontend-admin-integration]], [[implementation-milestones]]

Related concepts: [[dual-llm-memory-pipeline]] [[implementation-milestones]] [[agent-skills-taxonomy]]
