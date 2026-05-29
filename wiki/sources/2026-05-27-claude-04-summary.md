---
type: source-summary
raw: raw/llm/2026-05-27-claude-04-summary.md
source: claude
date: 2026-05-27
---

# Claude: Karpathy Autoresearch

## Key Claims

1. **Karpathy autoresearch pattern**: pick a painful niche → design tiny automated research loop → run experiments automatically → identify best setup → turn into simple agent product → monetize.
2. **5 AI workflows**: PRD → System Architecture → Features with Details → UI/UX Webframes → Master of Prompts — a workflow pipeline for AI-assisted development.
3. **Tool landscape**: Open-WebUI (Docker + DeepSeek/MiniMax/Kimi + RAG), AnythingLLM (Docker + OpenRouter + RAG), RAGFlow (cloud), custom Site-RAG-chatbot (FastAPI + Next.js).
4. **Chinese LLM API providers**: DeepSeek, Kimi (Moonshot), MiniMax, GLM (Zhipu) — with domestic vs international base URLs and model IDs.

## Unique Insights

- Notes that Ollama is "too slow" for practical use — prefers cloud-based Chinese LLM providers for local tooling.
- Provides specific Chinese LLM API configuration reference (base URLs, model names) — useful for developers working with Chinese AI infrastructure.
- The "5 AI workflows" template (PRD → System Arch → Features → UI/UX → Prompts) is a practical task decomposition for agentic coding.

## Contradictions

- This is a personal notes document, not a structured LLM analysis. Content is consistent with earlier sources — no contradictions with established concepts.
- The autoresearch pattern is complementary to the llm-wiki pattern: autoresearch automates the research loop, llm-wiki structures the output.
