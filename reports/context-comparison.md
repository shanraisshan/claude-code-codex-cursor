# Context Window Comparison Report

> **Last Updated:** 2026-02-04

## Claude Code

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Opus 4.5 | 200k | 64k | Premium model, complex reasoning, 67% lower cost than predecessor |
| Sonnet 4.5 | 200k (1M beta) | 64k | Recommended default, context awareness feature, best coding model |
| Haiku 4.5 | 200k | 64k | Fastest, context awareness feature, unbeatable for UI work |

**Legacy Models (Still Available):**
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

- All 4.5 models support extended thinking (31,999 token budget by default)
- 64k max output (up from 4k-32k in previous generations)
- Automatic context compaction at 75-92% utilization
- **Context awareness**: Sonnet 4.5 and Haiku 4.5 track remaining context window throughout conversation
- Context budget: 200K (standard), 500K (Enterprise), 1M (beta for tier 4 orgs)

---

## Codex CLI

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| GPT-5.2-Codex | 400k | 128k | Latest model (Jan 14, 2026), native compaction, reliable tool calling |
| GPT-5.1-Codex-Max | Multi-window (millions) | N/A | First model natively trained for compaction |
| GPT-5-Codex | 200k | N/A | Standard model with 200K context window |
| codex-mini-latest | ~200k | N/A | **DEPRECATED** - Removed Jan 16, 2026 |

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

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Claude 4.5 Sonnet | 200k (1M max) | 64k | Premium, Agent/Thinking modes |
| Claude 4.1 Opus | 200k | 64k | Max mode only, deep reasoning |
| Claude 4 Sonnet 1M | 1M | 64k | Max mode only, extended context |
| Claude 4 Sonnet | 200k | 64k | Normal and Max modes |
| Claude 4 Opus | 200k | 64k | Max mode only |
| Claude 3.7 Sonnet | 200k | 64k | Normal and Max modes |
| Claude 3.5 Sonnet | 200k | 64k | Fast and reliable |
| Claude 3.5 Haiku | 60k | 8k | Speed-optimized |

### OpenAI Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| GPT-5.1 Codex Max | 200k (400k max) | 128k | Added Jan 2026, improved tool calls |
| GPT-5.1 High | 200k (400k max) | 128k | Frontier coding model |
| GPT-5 Mini | 200k | 128k | Fast, lightweight option |
| GPT-5 Nano | 200k | 128k | Ultra-fast for simple tasks |
| GPT 4.1 | 200k (1M max) | 8k | Normal and Max modes |
| GPT-4o | 128k | 16k | All-purpose |
| GPT-4o mini | 60k | 8k | Free (500/day) |
| o3 | 200k | 8k | Reasoning optimized |
| o4-mini | 200k | 8k | Normal and Max modes |
| o3-mini | 200k | 8k | Agent/Thinking modes |
| o1 | 200k | 8k | Thinking mode |
| o1 Mini | 128k | 8k | Thinking mode |

### Google Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Gemini 3 Pro Preview | 200k (1M max) | 8k | Top performer on SWE-bench (76.2-78%) |
| Gemini 2.5 Pro | 200k (1M max) | 8k | Strong for design/debugging |
| Gemini 2.5 Flash | 200k (1M max) | 8k | Fast inference, extended context |

### xAI Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Grok 4 | 200k (2M max) | - | Real-time web search integration |
| Grok Code Fast | 200k | - | Optimized for speed |

### DeepSeek Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| DeepSeek V3 | 200k | - | Native support since v0.44+, hosted on US servers |
| DeepSeek R1 | 200k | - | Native support since v0.45+, free within Pro plan |

### Cursor Native Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Composer 1 | ~200k | - | 4x faster than comparable models, <30s response |

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

| Model | Context Window | Max Output | Status |
|-------|----------------|------------|--------|
| Gemini 3 Pro Preview | 1M | 65k | Current flagship |
| Gemini 3 Flash Preview | 1M | 65k | Balanced speed/intelligence |
| Gemini 3 Pro Image Preview | 65k | 32k | Image generation |
| Gemini 2.5 Pro | 1M | 65k | Stable |
| Gemini 2.5 Flash | 1M | 65k | Stable |
| Gemini 2.5 Flash-Lite | 1M | 65k | Stable |
| Gemini 2.5 Flash Image | 65k | 32k | Stable |
| Gemini 2.5 Flash Live | 131k | 8k | Preview |
| Gemini 2.0 Flash | 1M | 8k | **Deprecated** - March 31, 2026 |
| Gemini 2.0 Flash-Lite | 1M | 8k | **Deprecated** - March 31, 2026 |

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
