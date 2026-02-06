# Context Window Comparison Report

> **Last Updated:** 2026-02-06

## Claude Code

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| Opus 4.6 | 200k (1M beta) | 128k | $5.00 | $25.00 | Latest model (Feb 5, 2026), adaptive thinking, first Opus with 1M context |
| Opus 4.5 | 200k | 64k | $5.00 | $25.00 | Premium model, complex reasoning, 67% lower cost than predecessor |
| Sonnet 4.5 | 200k (1M beta) | 64k | $3.00 | $15.00 | Recommended default, context awareness feature, best coding model |
| Haiku 4.5 | 200k | 64k | $1.00 | $5.00 | Fastest, context awareness feature, unbeatable for UI work |

**Legacy Models (Still Available):**
- Opus 4.5: 200k tokens, 64k max output
- Opus 4.1: 200k tokens, 32k max output
- Sonnet 4: 200k / 1M beta, 64k max output
- Sonnet 3.7: 200k tokens, 64k / 128k beta max output
- Opus 4: 200k tokens, 32k max output
- Haiku 3: 200k tokens, 4k max output

**Reference:** [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models)

### Model Selection

- During session: `/model <alias>`
- At startup: `claude --model <alias>`
- Environment: `ANTHROPIC_MODEL=<alias>`
- Aliases: `opus`, `sonnet`, `haiku`, `opusplan`
- Extended context: `claude --betas context-1m-2025-08-07`

### Key Features

- Opus 4.6 supports adaptive thinking with 4 effort levels (low, medium, high, max)
- All 4.5 models support extended thinking (31,999 token budget by default)
- 128k max output for Opus 4.6; 64k for other 4.5 models
- Automatic context compaction at 75-92% utilization
- **Context awareness**: Sonnet 4.5 and Haiku 4.5 track remaining context window throughout conversation
- Context budget: 200K (standard), 500K (Enterprise), 1M (beta for tier 4 orgs)

---

## Codex CLI

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| GPT-5.3-Codex | 400k | 128k | TBD | TBD | Latest model (Feb 5, 2026), "Perfect Recall" attention, 25% faster |
| GPT-5.2-Codex | 400k | 128k | $1.75 | $14.00 | Native compaction, reliable tool calling (Jan 14, 2026) |
| GPT-5.1-Codex-Max | Multi-window (millions) | N/A | $1.25 | $10.00 | First model natively trained for compaction |
| GPT-5-Codex | 200k | N/A | $1.25 | $10.00 | Standard model with 200K context window |
| codex-mini-latest | ~200k | N/A | - | - | **DEPRECATED** - Removed Jan 16, 2026 |

**Reference:** [OpenAI Models](https://platform.openai.com/docs/models)

### Key Features

- **Context compaction** is now a core feature (not experimental)
- Automatically summarizes conversation history when approaching limits
- Enables long-running coding tasks spanning millions of tokens
- Model switching mid-session with `/model` command
- ChatGPT account sign-in (no manual API key needed)
- Agent Skills system production-ready

---

## Cursor

### Anthropic Models

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| Claude 4.6 Opus | 200k (1M max) | 64k | $5.00 | $25.00 | Latest Opus model, deep reasoning |
| Claude 4.5 Sonnet | 200k (1M max) | 64k | $3.00 | $15.00 | Premium, Agent/Thinking modes |
| Claude 4.5 Opus | 200k | 64k | $5.00 | $25.00 | Deep reasoning |
| Claude 4.5 Haiku | 200k | 64k | $1.00 | $5.00 | Fast and efficient |
| Claude 4 Sonnet 1M | 1M | 64k | $3.00 | $15.00 | Max mode only, extended context |
| Claude 4 Sonnet | 200k | 64k | $3.00 | $15.00 | Normal and Max modes |
| Claude 4 Opus | 200k | 64k | $5.00 | $25.00 | Max mode only |
| Claude 3.7 Sonnet | 200k | 64k | $3.00 | $15.00 | Normal and Max modes |
| Claude 3.5 Sonnet | 200k | 64k | $3.00 | $15.00 | Fast and reliable |
| Claude 3.5 Haiku | 60k | 8k | $0.80 | $4.00 | Speed-optimized |

### OpenAI Models

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| GPT-5.2 (all variants) | 272k | - | $2.00 | $8.00 | Latest generation |
| GPT-5.2-Codex | 272k | - | $1.75 | $14.00 | Code-optimized |
| GPT-5.1 Codex Max | 200k (400k max) | 128k | $1.25 | $10.00 | Improved tool calls |
| GPT-5.1 High | 200k (400k max) | 128k | $1.25 | $10.00 | Frontier coding model |
| GPT-5 Fast | 272k | - | $1.25 | $10.00 | Speed-optimized |
| GPT-5 Mini | 200k | 128k | $0.40 | $1.60 | Fast, lightweight option |
| GPT-5 Nano | 200k | 128k | $0.15 | $0.60 | Ultra-fast for simple tasks |
| GPT 4.1 | 200k (1M max) | 8k | $2.00 | $8.00 | Normal and Max modes |
| GPT-4o | 128k | 16k | $2.50 | $10.00 | All-purpose |
| GPT-4o mini | 60k | 8k | $0.15 | $0.60 | Free (500/day) |
| o3 | 200k | 8k | $2.00 | $8.00 | Reasoning optimized |
| o4-mini | 200k | 8k | $1.10 | $4.40 | Normal and Max modes |
| o3-mini | 200k | 8k | $1.10 | $4.40 | Agent/Thinking modes |
| o1 | 200k | 8k | $15.00 | $60.00 | Thinking mode |
| o1 Mini | 128k | 8k | $1.10 | $4.40 | Thinking mode |

### Google Models

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| Gemini 3 Pro Preview | 200k (1M max) | 8k | $2.00 | $12.00 | Top performer on SWE-bench (76.2-78%) |
| Gemini 3 Pro Image Preview | 200k (1M max) | 8k | $2.00 | $12.00 | Multimodal with image generation |
| Gemini 3 Flash | 200k (1M max) | 8k | $0.50 | $3.00 | Fast inference |
| Gemini 2.5 Pro | 200k (1M max) | 8k | $1.25 | $10.00 | Strong for design/debugging |
| Gemini 2.5 Flash | 200k (1M max) | 8k | $0.30 | $2.50 | Fast inference, extended context |

### xAI Models

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| Grok 4 | 200k (2M max) | - | $3.00 | $15.00 | Real-time web search integration |
| Grok Code | 256k | - | $2.00 | $10.00 | Code-optimized |
| Grok Code Fast | 200k | - | $0.60 | $4.00 | Optimized for speed |

### DeepSeek Models

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| DeepSeek V3 | 64k-128k | - | $0.27 | $1.10 | Native support, hosted on US servers |
| DeepSeek V3.1 | 128k | - | $0.27 | $1.10 | Upgraded context from V3 |
| DeepSeek R1 | 200k | - | $0.55 | $2.19 | Native support, free within Pro plan |

### Cursor Native Models

| Model | Context Window | Max Output | Input $/M | Output $/M | Notes |
|-------|----------------|------------|-----------|------------|-------|
| Composer 1 | ~200k | - | N/A | N/A | 4x faster than comparable models, <30s response |

> **Note:** Cursor uses subscription pricing ($20/mo Pro, $40/mo Business). API prices shown above are the underlying provider rates, not what Cursor users pay directly.

**Reference:** [Cursor Models](https://cursor.com/docs/models)

### Context Mode Comparison

| Mode | Context Range | Cost | Speed |
|------|---------------|------|-------|
| Normal | 60k - 400k | Standard | Fast |
| Max | 200k - 2M | Premium | Slower |

### Key Features

- Dynamic context discovery reduces token usage by 46.9% for MCP tool calls
- Automatic summarization when context window fills
- Chat history preserved as files for context recovery
- Efficient updates via Merkle tree-based change detection

---

## Gemini CLI

| Model | Context Window | Max Output | Input $/M | Output $/M | Status |
|-------|----------------|------------|-----------|------------|--------|
| Gemini 3 Pro Preview | 1M | 65k | $2.00 | $12.00 | Current flagship |
| Gemini 3 Flash Preview | 1M | 65k | $0.50 | $3.00 | Balanced speed/intelligence - Launched Feb 4, 2026 |
| Gemini 3 Pro Image Preview | 65k | 32k | $2.00 | $12.00 | Image generation |
| Gemini 2.5 Pro | 1M | 65k | $1.25 | $10.00 | Stable |
| Gemini 2.5 Flash | 1M | 65k | $0.30 | $2.50 | Stable |
| Gemini 2.5 Flash-Lite | 1M | 65k | $0.10 | $0.40 | Stable |
| Gemini 2.5 Flash Image | 65k | 32k | $0.30 | $2.50 | Stable |
| Gemini 2.5 Flash Preview | 1M | 65k | $0.30 | $2.50 | Experimental features (Preview) |
| Gemini 2.5 Flash TTS | 8k | 16k | $0.30 | $2.50 | Text-to-speech (Preview) |
| Gemini 2.5 Flash Live | 131k | 8k | $0.30 | $2.50 | Preview |
| Gemini 2.0 Flash | 1M | 8k | $0.10 | $0.40 | **Deprecated** - March 31, 2026 |
| Gemini 2.0 Flash-Lite | 1M | 8k | $0.08 | $0.30 | **Deprecated** - March 31, 2026 |

**Reference:** [Gemini API](https://ai.google.dev/gemini-api/docs/models)

### Deprecation Timeline

| Model | Shutdown Date |
|-------|---------------|
| Gemini 2.0 Flash | March 31, 2026 |
| Gemini 2.0 Flash-Lite | March 31, 2026 |
| Gemini 2.5 Pro | June 17, 2026 |
| Gemini 2.5 Flash | June 17, 2026 |
| Gemini 2.5 Flash-Lite | July 22, 2026 |

### Retired Models

| Model | Context Window | Retirement Date |
|-------|----------------|-----------------|
| Gemini 1.5 Pro | 2M | Sept 24, 2025 |
| Gemini 1.5 Flash | 1M | Sept 24, 2025 |

> **Note:** The 2M token context window is no longer available. Maximum context is now 1M tokens.

---

## Research Sources

### Claude Code
- [Anthropic Models Documentation](https://docs.anthropic.com/en/docs/about-claude/models)
- [Claude Code Model Configuration](https://code.claude.com/docs/en/model-config)

### Codex CLI
- [OpenAI Platform Models](https://platform.openai.com/docs/models)
- [OpenAI Codex Blog](https://openai.com/index/introducing-o3-and-o4-mini/)

### Cursor
- [Cursor Models Documentation](https://cursor.com/docs/models)
- [Cursor Changelog](https://cursor.com/changelog)

### Gemini CLI
- [Gemini API Models](https://ai.google.dev/gemini-api/docs/models)
- [Gemini CLI GitHub](https://github.com/google-gemini/gemini-cli)
- [Gemini Deprecations](https://ai.google.dev/gemini-api/docs/deprecations)
