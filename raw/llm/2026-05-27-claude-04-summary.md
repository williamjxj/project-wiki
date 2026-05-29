---
type: llm-chat
source: claude
topic: 04-summary
date: '2026-05-27'
status: pending
question: random question
---

## 🍆 Karpathy Autoresearch


```mermaid
flowchart LR
    A[Pick painful niche] --> B[Design tiny autoresearch loop]
    B --> C[Run experiments automatically]
    C --> D[See which setup works best]
    D --> E[Turn best setup into simple agent product]
    E --> F[Charge monthly subscription]
```

### 🍅 [program.md]https://github.com/karpathy/autoresearch/blob/master/program.md)

- Cold Email: Reply Rate
- Landing Page: CRO-Convertion Rate Optimization
- Ad Creatives: Conversion Rate
- Push Notifications:
- Chatbot Scripts: CSS-Customer Satisfaction Score

```text
read autoresearch/program.md, and then build our new /website/program.md file on top of that, but relevant to our website-speed benchmarking autoresearch objective
```

### 🥭 Github Actions

Autopilot


### 🍆 5 AI workflows

- PRD
- System Architecture
- Features with Details
- UI/UX Webframes
- Master of Prompts


### 🍍 open-webui

- Docker + DS / MiniMax (minimax-m2.7) /Kimi + RAG 
- ~/my-tools/open-webui

### 🥥 anything-LLM

- Docker + OpenRouter (DeepSeek V3.2) + RAG
- OpenRoute BYOK (Bring Your Own Key)
- ~/my-tools/anything-llm
 
### 🥝 ragflow

- https://cloud.ragflow.io/
- ~/my-tools/ragflow

### Site-RAG-chatbot

- Add signup/login
- DS/MiniMax/Kimi LLMs
- upload local docx/pdf/md
- ~/my-apps/site-rag-chatbot (python+fastapi + nextjs+tailwindcss+shadcn/ui)

### Why NOT Ollama

- toooo slow

### markitdown

### Karpathy llm-wiki

- https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
- https://x.com/karpathy/status/2039805659525644595


## 🇨🇳 常用国产 LLM API 国内/国际对照表

| 模型 / 平台 | 国内 Base URL | 国际 Base URL (海外推荐) | 常用/最新模型名 (Model ID) |
| :--- | :--- | :--- | :--- |
| **DeepSeek** | `https://api.deepseek.com/v1` | `https://api.deepseek.com/v1` | `deepseek-chat` (V3), `deepseek-reasoner` (R1) |
| **Kimi (Moonshot)** | `https://api.moonshot.cn/v1` | `https://api.moonshot.ai/v1` | `moonshot-v1-8k`, `kimi-k2.5` |
| **MiniMax** | `https://api.minimaxi.com/v1` | `https://api.minimax.io/v1` | `abab6.5s-chat`, `abab7-chat` |
| **智谱 GLM** | `https://open.bigmodel.cn/api/paas/v4` | `https://open.bigmodel.com/api/paas/v4` | `glm-4-plus`, `glm-4-air`, `glm-4-flash` |

### 💡 核心避坑指南
1. **Key 全球通用**：你在国内平台注册并生成的 API Key，在国际版域名下完全通用，无需重复开通。
2. **DeepSeek 特殊说明**：DeepSeek 的域名是全球通用的，但在海外访问 `api.deepseek.com` 通常会自动路由到最优节点。
3. **OpenAI SDK 兼容性**：上述四个平台均完美支持标准 `openai` Python 库，只需更换 `base_url` 和 `api_key` 即可。
4. **加拿大使用建议**：在加拿大运行代码时，**务必使用 .ai / .io / .com（国际版）域名**，以避免因跨境网络审查导致的连接超时或请求重定向。

```python
# 国内 Base URL 列表
DEEPSEEK_CN = "https://api.deepseek.com/v1"       # 通用
KIMI_CN = "https://api.moonshot.cn/v1"            # 国内
MINIMAX_CN = "https://api.minimaxi.com/v1"        # 国内
GLM_CN = "https://open.bigmodel.cn/api/paas/v4"  # 国内
```

>[!TIP] API URL=.cn

| Provider | Was | Fixed to |
|---|---|---|
| **Kimi** | `api.moonshot.ai` + `kimi-k2.5` | `api.moonshot.cn` + `moonshot-v1-8k` |
| **MiniMax** | `api.minimax.io` | `api.minimax.chat` |
| **GLM** | `open.bigmodel.com` (doesn't exist) | `open.bigmodel.cn` |

Also added `max_tokens=100` to all calls to avoid runaway responses during connectivity tests.


### ls -l

```bash
ls -laSh 文件大小排序
ls -lt 文件日期排序
ls -alt 日期排序
ls -la  隐含文件/目录
find -L raw/ -type f | wc -l # Count all files including through symlinks
```

### Bash is all you Need

- Claude Code instead of having Searhc, Lint, Execute, etc tools, we have: grep, tail, npm run lint, find, ls, cat
- hermes, openclaw, uipro, agent, claude, codex, opencode, cursor, copilot, specify, openspec, vite
- vercel, jq, graphify, ffmepg, ollama, 

```bash
for dir in raw/*/; do
  count=$(find -L "$dir" -type f | wc -l | tr -d ' ')
  echo "$count  $dir"
done
```

### Tool-Role Mapping

```text
┌──────────────────────────────────────────────────────────┐
│  LAYER              TOOL                ROLE             │
├──────────────────────────────────────────────────────────┤
│  Build middleware   Cursor / Claude Code  Write Python   │
│  Spec/schema        openspec / BMAD       AGENTS.md      │
│  Automate wiki ops  Codex CLI             Run agent tasks│
│  Capture input      Superpowers           POST /ingest   │
└──────────────────────────────────────────────────────────┘
```

### MemWeaver

- stateless
- local RAG pipeline where the "documents" are LLM-generated summaries of your own conversations,
- dual-LLM memory pipeline
- The local Ollama model acts as a private "memory manager" — it never sees the internet, costs nothing per call, and converts raw Q&A exchanges into structured wiki-style knowledge
- The public cloud LLM (Anthropic, OpenAI, etc.) acts as the "reasoning engine" — but instead of receiving noisy raw history, it receives clean, categorized, distilled knowledge as context
- Each new question triggers a skill-like retrieval: the most relevant wiki summary for that topic is injected into the prompt, not a dump of previous turns


classify, dense, incremental, structured, 

Claude For MemWeaver:

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
