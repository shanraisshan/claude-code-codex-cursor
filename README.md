# claude-code-codex-cursor-gemini

![AI Coding Tools](!/banner-pills.svg)

![Battle of the AI Agents](!/claude-mascot.svg)
![Battle of the AI Agents](!/codex-mascot.svg)
![Battle of the AI Agents](!/cursor-mascot.svg)
![Battle of the AI Agents](!/gemini-mascot.svg)

![AI Models](!/banner-models.svg)

> **Last Updated:** 2026-02-06

## Context Window Comparison

| Tool | Largest Context | Best Model | Input $/M | Output $/M | Source |
|------|-----------------|------------|-----------|------------|--------|
| Claude Code | 1M (beta) | Opus 4.6 with `--betas context-1m-2025-08-07` | $5.00 | $25.00 | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
| Codex CLI | 400k+ | GPT-5.3-Codex (context compaction) | TBD* | TBD* | [OpenAI Models](https://platform.openai.com/docs/models) |
| Cursor | 2M (Max mode) | Grok 4 | $3.00** | $15.00** | [Cursor Models](https://cursor.com/docs/models) |
| Gemini CLI | 1M | Gemini 3 Pro Preview | $2.00 | $12.00 | [Gemini API](https://ai.google.dev/gemini-api/docs/models) |

> \* GPT-5.3-Codex pricing not yet published by OpenAI (predecessor GPT-5.2-Codex: $1.75/$14.00)
> \*\* Cursor uses subscription pricing ($20/mo Pro); API prices shown are for the underlying Grok 4 model via xAI

[View Full Report](reports/context-comparison.md)

---

## Feature Comparison

| Feature | Claude Code | Codex CLI | Gemini CLI | Cursor |
|---------|:-----------:|:---------:|:----------:|:------:|
| **Hooks** | ✅ | ⚠️ | ✅ | ✅ |
| **Plugins/MCP** | ✅ | ✅ | ✅ | ✅ |
| **Sub-agents** | ✅ | ✅ | ✅ | ✅ |
| **Slash Commands** | ✅ | ✅ | ✅ | ✅ |
| **Custom Commands** | ✅ | ✅ | ✅ | ✅ |
| **IDE Integration** | ✅ | ✅ | ✅ | ✅ |
| **Git Integration** | ✅ | ✅ | ✅ | ✅ |
| **Web Search** | ✅ | ✅ | ✅ | ✅ |
| **Image Support** | ✅ | ✅ | ✅ | ⚠️ |
| **Memory/Persistence** | ✅ | ✅ | ✅ | ⚠️ |
| **Multi-file Editing** | ✅ | ✅ | ✅ | ✅ |
| **Auto-commit** | ⚠️ | ⚠️ | ✅ | ✅ |
| **Custom System Prompts** | ✅ | ✅ | ✅ | ✅ |
| **Cost Tracking** | ✅ | ❌ | ✅ | ⚠️ |
| **Sandbox Mode** | ✅ | ✅ | ✅ | ⚠️ |

[View Full Report](reports/feature-comparison.md)
