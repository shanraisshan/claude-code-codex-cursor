# Context Window Comparison Report

> **Last Updated:** 2026-02-03

## Claude Code

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Opus 4.5 | 200k | 64k | Premium model, complex reasoning |
| Sonnet 4.5 | 200k (1M beta) | 64k | Recommended default, use `sonnet[1m]` for extended context |
| Haiku 4.5 | 200k | 64k | Fastest, high-volume tasks |

**Reference:** [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models)

### Model Selection

- During session: `/model <alias>`
- At startup: `claude --model <alias>`
- Environment: `ANTHROPIC_MODEL=<alias>`
- Aliases: `opus`, `sonnet`, `haiku`, `opusplan`
- Extended context: `claude --betas context-1m-2025-08-07`

### Key Features

- All 4.5 models support extended thinking
- 64k max output (up from 4k-32k in previous generations)
- Automatic context compaction at 75-92% utilization

---

## Codex CLI

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| GPT-5.2-Codex | 400k | 128k | Default since Jan 2026, context compaction support |
| GPT-5.1-Codex-Max | 400k+ | 128k | Native context compaction, works across millions of tokens |
| GPT-5.1-Codex-Mini | 400k | 128k | Lighter, more affordable variant |
| codex-1 | 192k | - | Specialized o3 variant for coding |
| codex-mini-latest | 200k | 100k | **Default model**, fine-tuned o4-mini, low-latency |
| o3 | 200k | 100k | Latest reasoning model |
| o4-mini | 200k | 100k | Fast, efficient reasoning |

**Reference:** [OpenAI Models](https://platform.openai.com/docs/models)

### Key Features

- Native context compaction for million-token projects
- Model switching mid-session with `/model` command
- ChatGPT account sign-in (no manual API key needed)

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
| GPT-5 | 272k | 128k | Heavyweight reasoning |
| GPT-5 Fast | 272k | 128k | Faster GPT-5 variant |
| GPT-5 Mini | 272k | 128k | Cost-optimized |
| GPT-5 Nano | 272k | 128k | Speed-optimized |
| GPT-5-Codex | 272k | 128k | Code-specialized |
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
| Gemini 2.5 Pro | 200k (1M max) | 8k | Strong for design/debugging |
| Gemini 2.5 Flash | 1M | 8k | Max mode only |
| Gemini 2.0 Pro (exp) | 60k | 8k | Experimental |

### xAI Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Grok Code Fast 1 | 256k | - | 70.8% SWE-bench, fastest, $0.20/M input |

### DeepSeek Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| DeepSeek Coder V2 | 128k | - | Open-source, cost-effective |
| DeepSeek V3 | 64-128k | - | Native Cursor support, free |

### Cursor Native Models

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Composer 1 | 150-180k | - | Native MoE model, 250 tokens/sec, $1.25/M input |
| Cursor Small | 60k | 8k | Free, rapid edits |

**Reference:** [Cursor Models](https://cursor.com/docs/models)

### Context Mode Comparison

| Mode | Context Range | Cost | Speed |
|------|---------------|------|-------|
| Normal | 60k - 400k | Standard | Fast |
| Max | 200k - 1M | Premium | Slower |

---

## Gemini CLI

| Model | Context Window | Max Output | Status |
|-------|----------------|------------|--------|
| Gemini 3 Pro Preview | 1M | 65k | Current flagship |
| Gemini 3 Flash Preview | 1M | 65k | Balanced speed/intelligence |
| Gemini 3 Pro Image Preview | 65k | 32k | Image generation |
| Gemini 2.5 Pro | 1M | 65k | Retires June 17, 2026 |
| Gemini 2.5 Flash | 1M | 65k | Retires June 17, 2026 |
| Gemini 2.5 Flash-Lite | 1M | 65k | Retires July 22, 2026 |
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
