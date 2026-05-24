---
type: source-summary
raw: raw/llm/2026-05-13-chatgpt-api-token-context-management.md
source: chatgpt
date: 2026-05-13
---

# API vs Web UI Token Management (Doubao research)

## Key Claims

- Web chat auto-accumulates full history; tokens uncontrolled by user.
- API gives full control: per-request context, sliding window, hard token truncation.
- Pre-request processing: dedupe, compress, summarize, extract key facts — impossible in web UI.
- Layered memory: short-term recent dialogue + long-term DB/vector recall.
- RAG: vectorize history, retrieve relevant fragments only.
- Standard API flow: receive Q → read history → process → assemble prompt → validate tokens → call API → async update long-term memory.

## Unique Insights

- API context control is the foundational enabler for custom memory architectures.
- Forgetting/archival architecture as explicit design pattern.

## Contradictions

None — supports why mem-weaver must be API-based, not web-chat dependent.

## Related sources

[[chatgpt-retrieval-vs-synthesis]], [[claude-dual-llm-memory-pipeline]], [[memory-synthesis-vs-rag]]

Related concepts: [[memory-synthesis-vs-rag]]
