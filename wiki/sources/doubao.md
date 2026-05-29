---
type: source-summary
raw: raw/web/doubao.md
source: web
date: 2026-05-26
---

# Doubao: LLM Web Dialogue vs API Context & Token Management

## Key Claims

1. **Web UI vs API core difference**: web UIs auto-accumulate full chat history in every turn (uncontrollable token consumption). API gives developers full control over context — what to include, what to trim.
2. **API context management strategies**: single-turn isolation, fixed sliding window (keep N turns), token hard truncation (trim from head when threshold exceeded).
3. **Advanced memory techniques**: dialogue summarization (compress old turns into one summary), key information extraction (retain core rules/persona, discard chit-chat), system prompt persistence (keep fixed system prompt, trim only dynamic history).
4. **Memory architecture**: short-term (recent raw conversation) + long-term (DB/vector store) + RAG retrieval augmentation + consolidation/forgetting (archive old, prune low-frequency).

## Unique Insights

- Chinese-language deep dive into token management for API-based LLM applications — practical strategies rarely covered in English-language sources.
- **Multi-session isolation architecture**: per-user/per-session independent context maintenance — important for production SaaS deployments.
- **Memory consolidation/forgetting**: periodic compression of old conversations into summary form; automatic cleanup of unused/low-frequency history. This operationalizes knowledge decay (cf. Gemini's Ebbinghaus decay concept).
- Standard API context processing flow: receive query → read history → trim/dedup/summarize/retrieve → assemble prompt → validate token count → call API → save response → async update long-term memory.

## Contradictions

- Compatible with earlier sources. Provides practical token/memory management details that complement Gemini's theoretical knowledge decay model.
