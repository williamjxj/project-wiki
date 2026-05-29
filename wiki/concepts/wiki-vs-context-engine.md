---
type: concept
sources: [chatgpt-llm-based-project-workflow, claude-multi-llm-research-synthesis-workflow, gemini-llm-wiki-multi-agent]
last_updated: 2026-05-24
---

# Wiki vs Context Engine

## Consensus

All sources agree the underlying Karpathy idea is powerful: transient chats → persistent structured knowledge that dev tools consume. The [[compounding-knowledge-layer]] solves RAG's ephemerality problem.

## Divergence

| Source | View |
|--------|------|
| ChatGPT ([[chatgpt-llm-based-project-workflow]]) | Don't build a "wiki" — evolve to **Canonical Context Engine** / **Project Intelligence Layer**. "Wiki" implies static, human-written, manually organized. |
| Gemini ([[gemini-llm-wiki-multi-agent]]) | Fully embrace **LLM-Wiki** as compiled, compounding knowledge layer in Obsidian vault. Wiki is dynamic, AI-maintained, graph-structured. |
| Claude ([[claude-multi-llm-research-synthesis-workflow]]) | Workflow maps **perfectly onto Karpathy's llm-wiki pattern**. Markdown + git wiki with explicit structure. |

**Resolution:** 2:1 against ChatGPT's reframe. Gemini and Claude treat "LLM-Wiki" as a *compiling*, AI-maintained artifact — not a static human wiki. ChatGPT's "context engine" may describe the same architecture with different product naming.

## Decision

**Lean: adopt LLM-Wiki naming and Karpathy structure.** ChatGPT's reframe is useful for positioning but doesn't change the architecture. Current project-wiki submodule already implements this pattern.
