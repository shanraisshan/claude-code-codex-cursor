# Research Results

**Completed:** 2026-02-04 12:45:00

## Summary

| Tool | Context Window Changes | Feature Changes |
|------|------------------------|-----------------|
| Claude Code | Yes | Yes |
| Codex CLI | Yes | Yes |
| Cursor | Yes | Yes |
| Gemini CLI | Yes | Yes |

---

## Key Changes Found

### Context Windows

1. **Claude Code**: Added legacy model details (Opus 4.1, Sonnet 4, Sonnet 3.7, Opus 4, Haiku 3). Added context awareness feature for Sonnet 4.5 and Haiku 4.5.

2. **Codex CLI**: `codex-mini-latest` deprecated (removed Jan 16, 2026). GPT-5.2-Codex confirmed as latest with 400K context. Context compaction is now a core feature.

3. **Cursor**: Added GPT-5.1 Codex Max (400K Max mode), Gemini 3 Pro Preview (1M Max mode), Grok 4 (2M Max mode), DeepSeek V3/R1 native support. Added dynamic context discovery (46.9% token reduction).

4. **Gemini CLI**: Confirmed Gemini 2.5 Flash Image (65k context, 32k output) and Gemini 2.5 Flash Live (131k context). Added Gemini 3 Pro Image Preview.

### Features

1. **Claude Code Hooks**: Expanded from 8 to 12 event types (added PermissionRequest, PostToolUseFailure, SubagentStart, SessionEnd). Added 3 hook types (command, prompt, agent) and async support.

2. **Codex CLI MCP**: Now has Agent Skills system that is production-ready.

3. **Cursor Hooks**: Now enterprise-grade with partner integrations (MintMCP, Oasis Security, Runlayer, Semgrep). 10-20x performance improvement.

4. **Gemini CLI Hooks**: Now full support (was experimental), enabled by default since v0.26.0+.

5. **Gemini CLI Git Integration**: Should be updated to ⚠️ Partial (native git operations not yet available, only git-aware filtering).

---

## Proposed Context Window Updates (README.md)

No changes to the summary table required. Current values are accurate:

| Tool | Largest Context | Best Model | Source |
|------|-----------------|------------|--------|
| Claude Code | 1M (beta) | Sonnet 4.5 with `--betas context-1m-2025-08-07` | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
| Codex CLI | 400k+ | GPT-5.2-Codex (context compaction) | [OpenAI Models](https://platform.openai.com/docs/models) |
| Cursor | 1M (Max mode) | Gemini 3 Pro/Flash | [Cursor Models](https://cursor.com/docs/models) |
| Gemini CLI | 1M | Gemini 3 Pro Preview | [Gemini API](https://ai.google.dev/gemini-api/docs/models) |

---

## Proposed Feature Updates (README.md)

| Feature | Claude Code | Codex CLI | Gemini CLI | Cursor |
|---------|:-----------:|:---------:|:----------:|:------:|
| **Hooks** | ✅ | ⚠️ | ✅ | ✅ |
| **Plugins/MCP** | ✅ | ✅ | ✅ | ✅ |
| **Sub-agents** | ✅ | ✅ | ⚠️ | ✅ |
| **Slash Commands** | ✅ | ✅ | ✅ | ✅ |
| **Custom Commands** | ✅ | ✅ | ✅ | ✅ |
| **IDE Integration** | ✅ | ✅ | ✅ | ✅ |
| **Git Integration** | ✅ | ✅ | ⚠️ | ✅ |
| **Web Search** | ✅ | ✅ | ✅ | ✅ |
| **Image Support** | ⚠️ | ✅ | ✅ | ⚠️ |
| **Memory/Persistence** | ⚠️ | ✅ | ✅ | ⚠️ |
| **Multi-file Editing** | ✅ | ✅ | ✅ | ✅ |
| **Auto-commit** | ⚠️ | ⚠️ | ✅ | ✅ |
| **Custom System Prompts** | ✅ | ⚠️ | ✅ | ✅ |
| **Cost Tracking** | ✅ | ❌ | ✅ | ⚠️ |
| **Sandbox Mode** | ❌ | ✅ | ✅ | ⚠️ |

---

## Diff: Current vs New

### README.md - Feature Changes

```diff
 | Feature | Claude Code | Codex CLI | Gemini CLI | Cursor |
 |---------|:-----------:|:---------:|:----------:|:------:|
-| **Hooks** | ✅ | ⚠️ | ⚠️ | ✅ |
+| **Hooks** | ✅ | ⚠️ | ✅ | ✅ |
-| **Plugins/MCP** | ✅ | ⚠️ | ✅ | ✅ |
+| **Plugins/MCP** | ✅ | ✅ | ✅ | ✅ |
-| **Git Integration** | ✅ | ✅ | ✅ | ✅ |
+| **Git Integration** | ✅ | ✅ | ⚠️ | ✅ |
-| **Cost Tracking** | ✅ | ⚠️ | ✅ | ⚠️ |
+| **Cost Tracking** | ✅ | ❌ | ✅ | ⚠️ |
```

### Changes Summary

1. **Gemini CLI Hooks**: ⚠️ → ✅ (now full support, enabled by default since v0.26.0+)
2. **Codex CLI Plugins/MCP**: ⚠️ → ✅ (Agent Skills system is now production-ready)
3. **Gemini CLI Git Integration**: ✅ → ⚠️ (only git-aware filtering, no native git operations)
4. **Codex CLI Cost Tracking**: ⚠️ → ❌ (no built-in cost tracking at all, only community-requested)

---

## reports/context-comparison.md Changes

### Claude Code Section
- Add legacy models list
- Add context awareness feature note
- Update key features

### Codex CLI Section
- Mark `codex-mini-latest` as DEPRECATED
- Add context compaction as core feature
- Update model list

### Cursor Section
- Add GPT-5.1 Codex Max model
- Add Grok 4 with 2M Max mode
- Add DeepSeek V3/R1 with native support
- Add dynamic context discovery feature

### Gemini CLI Section
- Add Gemini 2.5 Flash Image (65k context)
- Add Gemini 2.5 Flash Live (131k context)
- Add Gemini 3 Pro Image Preview

---

## reports/feature-comparison.md Changes

### Hooks Section
- Claude Code: Update to 12 event types, add hook types (command, prompt, agent), async support
- Gemini CLI: Change status from "⚠️ Experimental" to "✅ Full Support"

### Plugins/MCP Section
- Codex CLI: Change status from "⚠️ MCP Only" to "✅ Full Support" (Agent Skills production-ready)

### Git Integration Section
- Gemini CLI: Change status from "✅ Full" to "⚠️ Partial" (git-aware filtering only)

### Cost Tracking Section
- Codex CLI: Change status from "⚠️ Third-party" to "❌ None" (no built-in tracking)

---

## Action Required

**User approval needed to:**

1. Update README.md Feature Comparison table (4 cell changes)
2. Update reports/context-comparison.md with new model details
3. Update reports/feature-comparison.md with revised feature statuses
