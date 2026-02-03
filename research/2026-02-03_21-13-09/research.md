# Context Window Research Session

**Started:** 2026-02-03 21:13:09
**Status:** Complete

---

## Claude Code Research
**Agent:** Dr. Sarah Chen
**Status:** Complete
**Research Date:** 2026-02-03
**Documentation Version:** Latest (February 2026)

### Models Found

| Model | Model ID | Context Window | Max Output | Notes |
|-------|----------|----------------|------------|-------|
| Opus 4.5 | claude-opus-4-5-20251101 | 200K tokens | 64K tokens | Premium model combining maximum intelligence with practical performance. Default for complex reasoning tasks. |
| Sonnet 4.5 | claude-sonnet-4-5-20250929 | 200K tokens / 1M tokens (beta) | 64K tokens | **Default model**. Best for complex agents and coding. 1M context requires `context-1m-2025-08-07` beta header. Long context pricing applies >200K. |
| Haiku 4.5 | claude-haiku-4-5-20251001 | 200K tokens | 64K tokens | Fastest model with near-frontier intelligence. Best for speed-critical tasks. |
| Sonnet 4 | claude-sonnet-4-20250514 | 200K tokens / 1M tokens (beta) | 64K tokens | Legacy model. Still available but migration to 4.5 recommended. Supports 1M context with beta header. |
| Haiku 3.5 | claude-3-5-haiku-20241022 | 200K tokens | 4K tokens | Legacy model. Limited output compared to newer models. |

### Key Findings

- **Default Model**: Sonnet 4.5 is the default and recommended model for most Claude Code use cases, offering the best balance of intelligence, speed, and cost
- **Extended Context Beta**: Both Sonnet 4.5 and Sonnet 4 support 1M token context windows when using the `context-1m-2025-08-07` beta header via the `--betas` flag
- **Extended Thinking**: All Claude 4.5 models (Opus, Sonnet, Haiku) support extended thinking and interleaved thinking features
- **Output Limits**: Claude 4.5 models support up to 64K tokens output, significantly higher than Haiku 3.5's 4K limit
- **Model Selection**: Can be changed via `/model` command (interactive), `--model` flag (single session), or `ANTHROPIC_MODEL` environment variable (permanent)
- **Legacy Models**: Claude Opus 4 and 4.1 have been removed from Claude Code. Only Opus 4.5 is currently available
- **Knowledge Cutoffs**:
  - Opus 4.5: May 2025 (reliable), Aug 2025 (training data)
  - Sonnet 4.5: Jan 2025 (reliable), Jul 2025 (training data)
  - Haiku 4.5: Feb 2025 (reliable), Jul 2025 (training data)

### Context Window Capabilities

**Standard Context (All Models):**
- 200K tokens (~150,000 words or ~680,000 unicode characters)
- No special configuration required
- Standard pricing applies

**Extended Context (Sonnet 4.5 & Sonnet 4 only):**
- 1M tokens (~750,000 words or ~3.4M unicode characters)
- Requires beta header: `claude --betas context-1m-2025-08-07`
- Long context pricing applies to tokens exceeding 200K
- Currently in beta for usage tier 4 organizations and custom rate limit users

### Configuration Methods

1. **Interactive Mode**: Use `/model` command to switch models
2. **Session Flag**: `claude --model opus` or `claude --model claude-sonnet-4-5-20250929`
3. **Environment Variable**: Set `ANTHROPIC_MODEL` in shell config
4. **Beta Features**: Use `--betas interleaved-thinking` or `--betas context-1m-2025-08-07`

### Pricing (Per Million Tokens)

| Model | Input Cost | Output Cost |
|-------|-----------|-------------|
| Opus 4.5 | $5 | $25 |
| Sonnet 4.5 | $3 | $15 |
| Haiku 4.5 | $1 | $5 |

Note: Long context pricing (>200K tokens) and extended thinking have additional costs. See official pricing page for details.

### Model Aliases

- `opus` → claude-opus-4-5-20251101
- `sonnet` → claude-sonnet-4-5-20250929
- `haiku` → claude-haiku-4-5-20251001

Aliases automatically point to the latest model snapshot and may update when new versions are released.

### Sources

- [Models Overview - Claude API Docs](https://platform.claude.com/docs/en/about-claude/models)
- [CLI Reference - Claude Code Docs](https://code.claude.com/docs/en/cli-reference)
- [Claude Code Model Configuration - Help Center](https://support.claude.com/en/articles/11940350-claude-code-model-configuration)
- [Context Windows - Claude API Docs](https://platform.claude.com/docs/en/build-with-claude/context-windows)
- [What's New in Claude 4.5](https://platform.claude.com/docs/en/about-claude/models/whats-new-claude-4-5)

---

## Codex CLI Research
**Agent:** Marcus Thompson
**Status:** Complete
**Research Date:** 2026-02-03
**Documentation Version:** Latest (February 2026)

### Models Found

| Model | Model ID | Context Window | Max Output | Notes |
|-------|----------|----------------|------------|-------|
| Codex-1 | codex-1 | 192k tokens | N/A | Version of o3 optimized for software engineering, tested at 192k with medium reasoning effort |
| Codex Mini Latest | codex-mini-latest | 200k tokens | 100k tokens | Fine-tuned version of o4-mini for Codex CLI, **default model**, supports reasoning tokens |
| GPT-5.2-Codex | gpt-5.2-codex | 400k tokens | 128k tokens | Most advanced agentic coding model with context compaction, knowledge cutoff: Aug 31, 2025 |
| GPT-5.1-Codex-Max | gpt-5.1-codex-max | 400k+ tokens | 128k tokens | First model with native context compaction, works across millions of tokens via automatic compaction |
| GPT-5.1-Codex-Mini | gpt-5.1-codex-mini | 400k tokens | 128k tokens | Lighter, more affordable variant of GPT-5.1-Codex with reduced capabilities |
| O3 | o3 | 200k tokens | 100k tokens | Base reasoning model, codex-1 is derived from this |
| O4-Mini | o4-mini | 200k tokens | 100k tokens | Fast reasoning model, codex-mini-latest is derived from this |

### Key Findings

- **Codex CLI Launch**: OpenAI launched Codex CLI on April 15, 2025, as a lightweight coding agent that runs in the terminal
- **Context Compaction**: GPT-5.1-Codex-Max and GPT-5.2-Codex feature revolutionary context compaction technology that automatically summarizes sessions when approaching context limits, enabling work across millions of tokens
- **Model Hierarchy**: Two main families exist:
  - **O-series derivatives**: codex-1 (from o3) and codex-mini-latest (from o4-mini) with 192k-200k windows
  - **GPT-5.x Codex series**: GPT-5.1 and GPT-5.2 variants with 400k windows and advanced agentic capabilities
- **Default Model**: codex-mini-latest is the default model in Codex CLI, optimized for low-latency code Q&A and editing
- **Reasoning Tokens**: All Codex models support reasoning tokens, allowing them to think through problems before responding
- **Open Source**: Codex CLI is fully open-source at github.com/openai/codex
- **Availability**: Rolling out to ChatGPT Pro, Enterprise, and Business users, with Plus and Edu support coming soon
- **Extended Context Testing**: For specialized benchmarks like SWE-bench, models were tested with 256k context length
- **Training Approach**: codex-1 was trained using reinforcement learning on real-world coding tasks to generate human-style code

### Pricing (Per Million Tokens)

| Model | Input Cost | Output Cost | Cache Discount |
|-------|-----------|-------------|----------------|
| codex-mini-latest | $1.50 | $6.00 | 75% prompt caching |

Note: Pricing for other models available through API documentation.

### Sources

- [Codex Models](https://developers.openai.com/codex/models/)
- [Introducing GPT-5.2-Codex | OpenAI](https://openai.com/index/introducing-gpt-5-2-codex/)
- [Building more with GPT-5.1-Codex-Max | OpenAI](https://openai.com/index/gpt-5-1-codex-max/)
- [GPT-5.2-Codex Model | OpenAI API](https://platform.openai.com/docs/models/gpt-5.2-codex)
- [GPT-5.1 Codex Model | OpenAI API](https://platform.openai.com/docs/models/gpt-5.1-codex)
- [codex-mini-latest Model | OpenAI API](https://platform.openai.com/docs/models/codex-mini-latest)
- [o4-mini Model | OpenAI API](https://platform.openai.com/docs/models/o4-mini)
- [o3 Model | OpenAI API](https://platform.openai.com/docs/models/o3)
- [Introducing Codex | OpenAI](https://openai.com/index/introducing-codex/)
- [Introducing OpenAI o3 and o4-mini | OpenAI](https://openai.com/index/introducing-o3-and-o4-mini/)
- [GitHub - openai/codex](https://github.com/openai/codex)
- [Elvis on X about codex-mini-latest](https://x.com/omarsar0/status/1923408662422311203)
- [GPT-5.1 Codex mini Model | OpenAI API](https://platform.openai.com/docs/models/gpt-5.1-codex-mini)

---

## Cursor Research
**Agent:** Elena Rodriguez
**Status:** Complete
**Research Date:** 2026-02-03

### Models Found

| Model | Provider | Context Window | Max Output | Notes |
|-------|----------|----------------|------------|-------|
| Claude Opus 4.5 | Anthropic | 200K tokens | 64K tokens | Premium reasoning model. Released Nov 2025. 80.9% on SWE-bench. Pricing increased in Cursor after initial release. |
| Claude Sonnet 4.5 | Anthropic | 200K / 1M tokens (Max) | 64K tokens | Default Claude model. Released Sept 2025. 1M context requires Max mode with auto `context-1m` flag. |
| Claude Haiku 4.5 | Anthropic | 200K tokens | 64K tokens | Fast Claude model. Released Oct 2025. Knowledge cutoff: Feb 2025. |
| Claude 3.7 Sonnet | Anthropic | 48K / 200K tokens (Max) | 4K / 64K tokens | Legacy model available in Max mode with 200 agent tool call limit. |
| Composer 1 | Cursor (Native) | 150-180K tokens (effective) | N/A | Cursor's native MoE model. 250 tokens/sec output. 4x faster generation. $1.25/M input, $10/M output. |
| GPT-5.2 | OpenAI | 400K tokens | 128K tokens | Latest flagship released Dec 2025. Three modes: Auto, Instant, Thinking. |
| GPT-5.2 Codex | OpenAI | 400K tokens | 128K tokens | Available in Cursor since mid-Jan 2026. Specialized for agentic coding. |
| GPT-5.1 Codex | OpenAI | 400K tokens | 128K tokens | Previous generation, now superseded by GPT-5.2. Still available. |
| GPT-5 | OpenAI | 400K tokens | 128K tokens | Base GPT-5 model. Released Nov 2025. |
| o3 | OpenAI | 200K tokens | 100K tokens | Advanced reasoning model. $2-8/M tokens. Available via "Show additional models" toggle. |
| Gemini 3 Pro | Google | 1M tokens | 65K tokens | Highest context window available. 76.8% SWE-bench. Available in Max mode. Strong for agentic tasks. |
| Gemini 3 Flash | Google | 1M tokens | 65K tokens | 78% SWE-bench (outperforms 3 Pro). 4x lower cost, 3x faster. $0.50/M input, $3/M output. |
| Gemini 2.5 Pro | Google | 1M tokens | 65K tokens | Previous generation. Available in Max mode. State-of-the-art reasoning. |
| Gemini 2.5 Flash | Google | 1M tokens | 65K tokens | Legacy Flash model. Still available. Best price-performance in 2.5 series. |
| Grok Code Fast 1 | xAI | 256K tokens | N/A | 70.8% SWE-bench. Fastest model. $0.20/M input, $1.50/M output. Free trial period. |
| DeepSeek Coder V2 | DeepSeek | 128K tokens | N/A | Cursor-hosted option. Open-source, cost-effective. Native support since v0.44+. |
| DeepSeek V3 | DeepSeek | 64-128K tokens | N/A | Latest version. 64K effective in consumer app, 128K documented. Native Cursor support. |

### Key Findings

- **Model Diversity**: Cursor supports 4 major providers (Anthropic, OpenAI, Google, xAI) plus native Composer model and DeepSeek integration
- **Subscription Tiers**: Pro ($20/month), Pro+ ($60/month - 3x usage), Ultra ($200/month - 20x usage)
- **Usage-Based Credits**: Pro plan provides $20 credit pool (~225 Sonnet 4.5 requests, ~550 Gemini requests, ~500 GPT-5 requests)
- **Max Mode**: Extends context to maximum available per model (1M for Gemini 3, Sonnet 4.5 with auto flag). Slower and more expensive.
- **Normal Mode**: Default 200K token context (~15,000 lines of code) for most models
- **Composer Performance**: Native model outputs at 250 tokens/sec, ~2x faster than similar models, completes turns in <30 seconds
- **Auto Model Selection**: Cursor can automatically select best-performing model based on task and demand
- **Context Window Strategy**: Cursor emphasizes "right context over more context" - quality vs quantity
- **Grok Code**: Free trial period available. Designed for agentic work with tool calling
- **Recent Additions**: GPT-5.2 Codex added mid-Jan 2026, Gemini 3 models added late 2025/early 2026
- **Claude Sonnet 5**: Expected to launch Feb 3, 2026 (this week) - will outperform Opus 4.5 at 50% lower cost
- **Max Mode Features**: 750 lines per file read operation, automatic 1M context flag for Claude models
- **DeepSeek Integration**: Native support for V3 and Coder V2, cost-effective alternative to frontier models

### Context Window Comparison

| Context Size | Models |
|--------------|--------|
| 1M tokens | Gemini 3 Pro, Gemini 3 Flash, Gemini 2.5 Pro, Gemini 2.5 Flash, Claude Sonnet 4.5 (Max mode) |
| 400K tokens | GPT-5, GPT-5.1, GPT-5.2, GPT-5.2 Codex |
| 256K tokens | Grok Code Fast 1 |
| 200K tokens | Claude Opus 4.5, Claude Sonnet 4.5, Claude Haiku 4.5, Claude 3.7 (Max), o3 |
| 150-180K tokens | Composer 1 (effective) |
| 128K tokens | DeepSeek Coder V2 |
| 64-128K tokens | DeepSeek V3 |
| 48K tokens | Claude 3.7 Sonnet (Normal) |

### Pricing Structure

**Anthropic Models (API Pricing):**
- Haiku 4.5: $1/M input, $5/M output
- Sonnet 4.5: $3/M input, $15/M output
- Opus 4.5: $5/M input, $25/M output

**Google Models:**
- Gemini 3 Flash: $0.50/M input, $3/M output
- Gemini 3 Pro: Higher cost than Flash (4x)

**xAI Models:**
- Grok Code Fast 1: $0.20/M input, $1.50/M output

**Cursor Native:**
- Composer 1: $1.25/M input, $10/M output

**OpenAI Models:**
- o3: $2-8/M tokens
- GPT-5 series: Standard OpenAI pricing

### CLI Commands

- `/models` - List all available models and switch between them
- `--list-models` - CLI flag to list models
- `agent models` - Background agent API command

### Model Selection Strategy (Community Recommendations)

Based on Cursor forum discussions, users recommend:
- **Agent**: GPT-5.2 XHigh for complex planning
- **Subagents - DB Tasks**: Opus 4.5 for database work
- **Subagents - Senior Tasks**: GPT-5.2 XHigh for architecture
- **Subagents - Middle+ Tasks**: Codex 5.2 XHigh for implementation
- **Subagents - Middle Tasks**: Gemini 3 Flash for standard coding
- **Subagents - Junior Tasks**: Grok Code Fast for simple tasks
- **Verifier**: Gemini 3 Flash for fast verification

### Sources

- [Models | Cursor Docs](https://cursor.com/docs/models)
- [Cursor Changelog](https://cursor.com/changelog)
- [Cursor CLI (Jan 8, 2026) - Announcements](https://forum.cursor.com/t/cursor-cli-jan-8-2026-new-commands-and-performance-improvement/148372)
- [Choosing the Right Model in Cursor - Frontend Masters Blog](https://frontendmasters.com/blog/choosing-the-right-model-in-cursor/)
- [How To Optimize Your Usage v3.0 - Cursor Forum](https://forum.cursor.com/t/how-to-optimize-your-usage-the-best-ai-models-to-use-version-3-0/145657)
- [GPT 5.2 Codex Available in Cursor - Forum](https://forum.cursor.com/t/gpt-5-2-codex-available-in-cursor/148901)
- [Introducing GPT-5.2 | OpenAI](https://openai.com/index/introducing-gpt-5-2/)
- [Introducing Claude Opus 4.5 | Anthropic](https://www.anthropic.com/news/claude-opus-4-5)
- [Gemini 3 Flash - Release Discussion](https://forum.cursor.com/t/gemini-3-flash-out-now/146648)
- [Grok Code Fast 1 | xAI](https://x.ai/news/grok-code-fast-1)
- [Introducing Composer: Cursor's First Native AI Coding Model](https://skywork.ai/blog/vibecoding/cursor-composer-ai-model/)
- [Cursor Pricing](https://cursor.com/pricing)
- [DeepSeek V3 with Cursor Guide](https://apidog.com/blog/deepseek-v3-cursor-guide/)
- [Claude Opus 4.5 vs GPT-5.2 Comparison](https://www.digitalapplied.com/blog/claude-opus-4-5-vs-gpt-5-2-codex-vs-gemini-3-pro-comparison)
- [Best AI Models 2026 Comparison](https://www.humai.blog/best-ai-models-2026-gpt-5-vs-claude-4-5-opus-vs-gemini-3-pro-complete-comparison/)
- [Cursor vs Claude Code Comparison](https://www.builder.io/blog/cursor-vs-claude-code)
- [Introducing Composer Blog Post](https://cursor.com/blog/2-0)

---

## Gemini CLI Research
**Agent:** Dr. Raj Patel
**Status:** Complete
**Research Date:** 2026-02-03
**Documentation Version:** Latest (February 2026)

### Models Found

| Model | Model ID | Context Window | Max Output | Status |
|-------|----------|----------------|------------|--------|
| Gemini 3 Pro | gemini-3-pro-preview | 1M tokens (1,048,576) | 65,536 tokens | Preview (November 2025) - Available with paid tier |
| Gemini 3 Flash | gemini-3-flash-preview | 1M tokens (1,048,576) | 65,536 tokens | Preview (December 2025) - Available with paid tier |
| Gemini 2.5 Pro | gemini-2.5-pro | 1M tokens (1,048,576) | 65,536 tokens | Stable GA (June 2025) - State-of-the-art reasoning |
| Gemini 2.5 Flash | gemini-2.5-flash | 1M tokens (1,048,576) | 65,536 tokens | Stable GA (June 2025) - Best price-performance |
| Gemini 2.5 Flash-Lite | gemini-2.5-flash-lite | 1M tokens (1,048,576) | 65,536 tokens | Stable GA (July 2025) - Fastest, cost-optimized |
| Gemini 1.5 Pro | gemini-1.5-pro-002 | 1M tokens / 2M tokens | 8,192 tokens | **DEPRECATED** - Shut down September 2025 |
| Gemini 1.5 Flash | gemini-1.5-flash-002 | 1M tokens | 8,192 tokens | **DEPRECATED** - Shut down September 2025 |
| Gemini 2.0 Flash | gemini-2.0-flash | 1M tokens | 8,192 tokens | **SHUTTING DOWN** - March 31, 2026 |
| Gemini 2.0 Flash-Lite | gemini-2.0-flash-lite | 1M tokens | 8,192 tokens | **SHUTTING DOWN** - March 31, 2026 |

### Key Findings

- **Current Generation**: Gemini 3 series (Pro and Flash) are the latest preview models available in CLI, offering frontier-class multimodal capabilities
- **Production Stable**: Gemini 2.5 series (Pro, Flash, Flash-Lite) are stable GA models recommended for production use
- **Consistent Context**: All current-generation models (Gemini 2.5 and 3.x) support 1M token context windows as standard
- **Increased Output**: Current models support 65,536 tokens output (8x more than previous generations' 8K limit)
- **2M Context Deprecated**: Gemini 1.5 Pro's 2M token context window capability was available but the model has been deprecated (shutdown September 2025)
- **Migration Required**: Gemini 2.0 models shutting down March 31, 2026 - users must migrate to 2.5 or 3.x series
- **Multimodal Support**: All current models support text, image, video, audio, and PDF inputs
- **Auto Selection**: CLI offers "Auto" mode that intelligently selects between Gemini 3 or 2.5 models based on task complexity
- **Access Control**: Gemini 3 models require paid tier (Google AI Pro/Ultra, paid API key, or Gemini Code Assist with admin preview access)
- **Alias Tracking**: `gemini-pro-latest` and `gemini-flash-latest` now point to Gemini 3 models (as of January 2026)

### Context Window Capabilities

**All Current Models (2.5 and 3.x):**
- 1,048,576 tokens (1M) input context window
- Equivalent to:
  - 50,000 lines of code
  - 8 average-length English novels
  - 1 hour of video content
  - 11 hours of audio
  - 700,000+ words

**Output Tokens:**
- Current generation: 65,536 tokens (65K)
- Legacy models: 8,192 tokens (8K)

**Historical Note:**
- Gemini 1.5 Pro supported up to 2M tokens but has been shut down
- No current models offer 2M context windows

### Model Selection in CLI

**Auto Mode (Recommended):**
- `Auto (Gemini 3)`: Automatically selects between gemini-3-pro-preview and gemini-3-flash-preview
- `Auto (Gemini 2.5)`: Automatically selects between gemini-2.5-pro and gemini-2.5-flash

**Manual Selection:**
Users can manually select specific models via the `/model` command or `-m` flag:
```bash
gemini -m gemini-2.5-flash
gemini -m gemini-3-pro-preview
```

**Requirements for Gemini 3 Access:**
1. Upgrade CLI to version 0.21.1 or later
2. Run `/settings` and enable "Preview features"
3. Use `/model` to select Gemini 3 models

### Version and Release Timeline

- **January 2026**: Gemini 3 models support Computer Use tool; gemini-3-pro-image-preview released
- **December 2025**: Gemini 3 Flash preview released
- **November 2025**: Gemini 3 Pro preview released
- **July 2025**: Gemini 2.5 Flash-Lite stable release
- **June 2025**: Gemini 2.5 Pro and Flash stable releases
- **September 2025**: Gemini 1.5 models shut down
- **March 31, 2026**: Gemini 2.0 models scheduled shutdown

### Performance Highlights

**Gemini 3 Flash:**
- 78% score on SWE-bench Verified for agentic coding
- Outperforms both Gemini 2.5 series and Gemini 3 Pro on coding tasks
- Optimized for high-frequency terminal-based workflows

**Gemini 2.5 Flash:**
- Best price-performance ratio in the lineup
- Upgraded reasoning and hybrid thinking control
- Production-ready stability

**Gemini 2.5 Pro:**
- State-of-the-art thinking model for complex reasoning
- Handles challenging problems across multiple information sources

### Sources

- [Gemini Models Documentation - Google AI for Developers](https://ai.google.dev/gemini-api/docs/models)
- [Long Context Support - Gemini API Docs](https://ai.google.dev/gemini-api/docs/long-context)
- [Gemini CLI GitHub Repository](https://github.com/google-gemini/gemini-cli)
- [Gemini 3 Flash Announcement - Google Developers Blog](https://developers.googleblog.com/gemini-3-flash-is-now-available-in-gemini-cli/)
- [Gemini CLI Model Selection Documentation](https://geminicli.com/docs/cli/model/)
- [Release Notes - Gemini API Changelog](https://ai.google.dev/gemini-api/docs/changelog)
- [Google Gemini Context Window Guide - DataStudios](https://www.datastudios.org/post/google-gemini-context-window-token-limits-model-comparison-and-workflow-strategies-for-late-2025)
- [Gemini 3 Context Window Analysis - Thinkpeak AI](https://thinkpeak.ai/gemini-3-context-window-size-1-2m-tokens/)
- [Gemini 1.5 Pro 2M Context Window Announcement - Google Developers Blog](https://developers.googleblog.com/en/new-features-for-the-gemini-api-and-google-ai-studio/)
- [Gemini 3 Overview - Google Blog](https://blog.google/products/gemini/gemini-3/)
- [Gemini 3 Flash Benchmarks - Google Blog](https://blog.google/products/gemini/gemini-3-flash/)

---
