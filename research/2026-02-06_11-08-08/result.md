# Research Results

**Completed:** 2026-02-06 11:08
**Research Folder:** research/2026-02-06_11-08-08/

## Summary

| Tool | Context Window Changes | Feature Changes |
|------|------------------------|-----------------|
| Claude Code | YES - Opus 4.6 (1M beta, 128k output) | YES - Sandbox ✅, Memory ✅, Image ✅, Agent Teams |
| Codex CLI | YES - GPT-5.3-Codex (400k, Perfect Recall) | YES - Custom System Prompts ✅ |
| Cursor | YES - Claude 4.6 Opus, DeepSeek V3.1, Grok Code added | NO - Minor refinements only |
| Gemini CLI | YES - Gemini 3 Flash Preview added (Feb 4) | YES - Sub-agents ✅ (was ⚠️) |

---

## Proposed Context Window Table (README.md)

| Tool | Largest Context | Best Model | Source |
|------|-----------------|------------|--------|
| Claude Code | 1M (beta) | Opus 4.6 with `--betas context-1m-2025-08-07` | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
| Codex CLI | 400k+ | GPT-5.3-Codex (context compaction) | [OpenAI Models](https://platform.openai.com/docs/models) |
| Cursor | 2M (Max mode) | Grok 4 | [Cursor Models](https://cursor.com/docs/models) |
| Gemini CLI | 1M | Gemini 3 Pro Preview | [Gemini API](https://ai.google.dev/gemini-api/docs/models) |

---

## Proposed Feature Table (README.md)

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

---

## Diff: Current vs New

### README.md - Context Window Changes

```diff
 | Tool | Largest Context | Best Model | Source |
 |------|-----------------|------------|--------|
-| Claude Code | 1M (beta) | Sonnet 4.5 with `--betas context-1m-2025-08-07` | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
+| Claude Code | 1M (beta) | Opus 4.6 with `--betas context-1m-2025-08-07` | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
-| Codex CLI | 400k+ | GPT-5.2-Codex (context compaction) | [OpenAI Models](https://platform.openai.com/docs/models) |
+| Codex CLI | 400k+ | GPT-5.3-Codex (context compaction) | [OpenAI Models](https://platform.openai.com/docs/models) |
-| Cursor | 1M (Max mode) | Gemini 3 Pro/Flash | [Cursor Models](https://cursor.com/docs/models) |
+| Cursor | 2M (Max mode) | Grok 4 | [Cursor Models](https://cursor.com/docs/models) |
 | Gemini CLI | 1M | Gemini 3 Pro Preview | [Gemini API](https://ai.google.dev/gemini-api/docs/models) |
```

### README.md - Feature Changes

```diff
 | Feature | Claude Code | Codex CLI | Gemini CLI | Cursor |
 |---------|:-----------:|:---------:|:----------:|:------:|
 | **Hooks** | ✅ | ⚠️ | ✅ | ✅ |
 | **Plugins/MCP** | ✅ | ✅ | ✅ | ✅ |
-| **Sub-agents** | ✅ | ✅ | ⚠️ | ✅ |
+| **Sub-agents** | ✅ | ✅ | ✅ | ✅ |
 | **Slash Commands** | ✅ | ✅ | ✅ | ✅ |
 | **Custom Commands** | ✅ | ✅ | ✅ | ✅ |
 | **IDE Integration** | ✅ | ✅ | ✅ | ✅ |
-| **Git Integration** | ✅ | ✅ | ⚠️ | ✅ |
+| **Git Integration** | ✅ | ✅ | ✅ | ✅ |
 | **Web Search** | ✅ | ✅ | ✅ | ✅ |
-| **Image Support** | ⚠️ | ✅ | ✅ | ⚠️ |
+| **Image Support** | ✅ | ✅ | ✅ | ⚠️ |
-| **Memory/Persistence** | ⚠️ | ✅ | ✅ | ⚠️ |
+| **Memory/Persistence** | ✅ | ✅ | ✅ | ⚠️ |
 | **Multi-file Editing** | ✅ | ✅ | ✅ | ✅ |
 | **Auto-commit** | ⚠️ | ⚠️ | ✅ | ✅ |
-| **Custom System Prompts** | ✅ | ⚠️ | ✅ | ✅ |
+| **Custom System Prompts** | ✅ | ✅ | ✅ | ✅ |
 | **Cost Tracking** | ✅ | ❌ | ✅ | ⚠️ |
-| **Sandbox Mode** | ❌ | ✅ | ✅ | ⚠️ |
+| **Sandbox Mode** | ✅ | ✅ | ✅ | ⚠️ |
```

### reports/context-comparison.md - Claude Code Changes

```diff
 ## Claude Code

 | Model | Context Window | Max Output | Notes |
 |-------|----------------|------------|-------|
+| Opus 4.6 | 200k (1M beta) | 128k | Latest model, adaptive thinking, first Opus with 1M context |
 | Opus 4.5 | 200k | 64k | Premium model, complex reasoning, 67% lower cost than predecessor |
 | Sonnet 4.5 | 200k (1M beta) | 64k | Recommended default, context awareness feature, best coding model |
 | Haiku 4.5 | 200k | 64k | Fastest, context awareness feature, unbeatable for UI work |

 **Legacy Models (Still Available):**
+- Opus 4.5: 200k tokens, 64k max output
 - Opus 4.1: 200k tokens, 32k max output
 - Sonnet 4: 200k / 1M beta, 64k max output
```

### reports/context-comparison.md - Codex CLI Changes

```diff
 ## Codex CLI

 | Model | Context Window | Max Output | Notes |
 |-------|----------------|------------|-------|
+| GPT-5.3-Codex | 400k | 128k | Latest model (Feb 5, 2026), Perfect Recall attention, 25% faster |
 | GPT-5.2-Codex | 400k | 128k | Latest model (Jan 14, 2026), native compaction, reliable tool calling |
 | GPT-5.1-Codex-Max | Multi-window (millions) | N/A | First model natively trained for compaction |
```

### reports/context-comparison.md - Cursor Changes

```diff
 ### Anthropic Models

 | Model | Context Window | Max Output | Notes |
 |-------|----------------|------------|-------|
+| Claude 4.6 Opus | 200k (1M max) | 64k | NEW - Latest Opus model |
 | Claude 4.5 Sonnet | 200k (1M max) | 64k | Premium, Agent/Thinking modes |
-| Claude 4.1 Opus | 200k | 64k | Max mode only, deep reasoning |
+| Claude 4.5 Opus | 200k | 64k | Deep reasoning |

 ### xAI Models

 | Model | Context Window | Max Output | Notes |
 |-------|----------------|------------|-------|
 | Grok 4 | 200k (2M max) | - | Real-time web search integration |
+| Grok Code | 256k | - | Code-optimized |
 | Grok Code Fast | 200k | - | Optimized for speed |

 ### DeepSeek Models

 | Model | Context Window | Max Output | Notes |
 |-------|----------------|------------|-------|
-| DeepSeek V3 | 200k | - | Native support since v0.44+, hosted on US servers |
+| DeepSeek V3 | 64k-128k | - | Native support, hosted on US servers |
+| DeepSeek V3.1 | 128k | - | NEW - Upgraded context from V3 |
 | DeepSeek R1 | 200k | - | Native support since v0.45+, free within Pro plan |
```

### reports/context-comparison.md - Gemini CLI Changes

```diff
 ## Gemini CLI

 | Model | Context Window | Max Output | Status |
 |-------|----------------|------------|--------|
 | Gemini 3 Pro Preview | 1M | 65k | Current flagship |
-| Gemini 3 Flash Preview | 1M | 65k | Balanced speed/intelligence |
+| Gemini 3 Flash Preview | 1M | 65k | Balanced speed/intelligence - Launched Feb 4, 2026 |
 | Gemini 3 Pro Image Preview | 65k | 32k | Image generation |
+| Gemini 2.5 Flash TTS | 8k | 16k | Text-to-speech (Preview) |
+| Gemini 2.5 Flash Preview | 1M | 65k | Experimental features (Preview) |
```

---

## Detailed Change Summary

### Context Window Changes

1. **Claude Code**: Opus 4.6 released Feb 5, 2026 - first Opus model with 1M context (beta) and 128k max output (doubled from 64k). Best model changes from Sonnet 4.5 to Opus 4.6.
2. **Codex CLI**: GPT-5.3-Codex released Feb 5, 2026 - 400k context with "Perfect Recall" attention mechanism, 25% faster than predecessor.
3. **Cursor**: New models added - Claude 4.6 Opus (1M max), DeepSeek V3.1 (128k), Grok Code (256k). Largest context now 2M via Grok 4 Max mode.
4. **Gemini CLI**: Gemini 3 Flash Preview launched Feb 4, 2026. Added Gemini 2.5 Flash TTS and Flash Preview models. Core context windows unchanged at 1M.

### Feature Changes

1. **Claude Code**: Sandbox Mode upgraded from ❌ to ✅ (macOS/Linux sandboxing). Memory/Persistence upgraded from ⚠️ to ✅ (automatic memory, CLAUDE.md, .claude/rules/). Image Support upgraded from ⚠️ to ✅ (all Claude 4 models). New: Agent Teams, unified Skills system, LSP tool, PDF reading, keybindings.
2. **Codex CLI**: Custom System Prompts upgraded from ⚠️ to ✅ (Markdown-based custom prompts). New: GPT-5.3-Codex, JetBrains/Visual Studio/Xcode/Eclipse IDE support, live skill update detection.
3. **Gemini CLI**: Sub-agents upgraded from ⚠️ to ✅ (AgentRegistry, JSON schema validation). Git Integration upgraded from ⚠️ to ✅ (GitHub Actions integration, AI commit messages). New: v0.27.0 event-driven architecture, Agent Skills stable, /rewind command.
4. **Cursor**: Minor refinements. New: Cursor Blame (Enterprise), Agent Q&A, Cloud agents, image generation. Feature statuses largely confirmed as-is.

---

## Date Updates

README.md and reports/context-comparison.md "Last Updated" date should change from `2026-02-04` to `2026-02-06`.
