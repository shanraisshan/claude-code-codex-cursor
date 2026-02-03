# Research Results

**Completed:** 2026-02-03 21:13:09
**Status:** Complete - README Updated

---

## Summary

| Tool | Models Found | Changes Detected |
|------|--------------|------------------|
| Claude Code | 5 (3 current + 2 legacy) | Minor - Legacy models added |
| Codex CLI | 7 | Yes - codex-mini renamed to codex-mini-latest |
| Cursor | 17 | Yes - New models: Composer 1, Grok Code Fast 1, DeepSeek |
| Gemini CLI | 9 (5 current + 4 deprecated) | Minor - Deprecation dates confirmed |

---

## Proposed README Updates

```markdown
## Context Window Comparison

| Tool | Largest Context | Best Model | Source |
|------|-----------------|------------|--------|
| Claude Code | 1M (beta) | Sonnet 4.5 with `--betas context-1m-2025-08-07` | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
| Codex CLI | 400k+ | GPT-5.2-Codex (with context compaction) | [OpenAI Models](https://platform.openai.com/docs/models) |
| Cursor | 1M (Max mode) | Gemini 3 Pro/Flash | [Cursor Models](https://cursor.com/docs/models) |
| Gemini CLI | 1M | Gemini 3 Pro Preview | [Gemini API](https://ai.google.dev/gemini-api/docs/models) |
```

---

## Diff: Current vs New

### README.md Changes

```diff
 | Tool | Largest Context | Best Model | Source |
 |------|-----------------|------------|--------|
-| Claude Code | 1M (beta) | Sonnet 4.5 with `[1m]` suffix | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
+| Claude Code | 1M (beta) | Sonnet 4.5 with `--betas context-1m-2025-08-07` | [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models) |
 | Codex CLI | 400k | GPT-5.2-Codex | [OpenAI Models](https://platform.openai.com/docs/models) |
-| Cursor | 2M (Max mode) | Grok 4 Fast | [Cursor Models](https://cursor.com/docs/models) |
+| Cursor | 1M (Max mode) | Gemini 3 Pro/Flash | [Cursor Models](https://cursor.com/docs/models) |
 | Gemini CLI | 1M | Gemini 3 Pro Preview | [Gemini API](https://ai.google.dev/gemini-api/docs/models) |
```

### Key Differences Found

#### Claude Code
- **Current README**: Shows `[1m]` suffix for extended context
- **New Research**: Requires `--betas context-1m-2025-08-07` flag (more accurate)
- **Added**: Legacy models (Sonnet 4, Haiku 3.5) still available

#### Codex CLI
- **Current README**: Lists `codex-mini`
- **New Research**: Model renamed to `codex-mini-latest` (default model)
- **Confirmed**: GPT-5.2-Codex with 400k context is latest

#### Cursor
- **Current README**: Claims 2M context with Grok 4 Fast
- **New Research**: No 2M context found - Grok Code Fast 1 has 256k, max is 1M with Gemini models
- **Added**: Composer 1 (Cursor native), DeepSeek V3, Grok Code Fast 1
- **Correction**: Best large-context model is Gemini 3 Pro/Flash at 1M

#### Gemini CLI
- **Current README**: Accurate - 1M context, Gemini 3 Pro Preview
- **New Research**: Confirms data, adds deprecation timeline for 2.0/2.5 models
- **Note**: 2M context (Gemini 1.5 Pro) is retired

---

## Proposed Report Updates (reports/context-comparison.md)

### Claude Code Section
```diff
 ### Model Selection

 - During session: `/model <alias>`
 - At startup: `claude --model <alias>`
 - Environment: `ANTHROPIC_MODEL=<alias>`
-- Aliases: `opus`, `sonnet`, `haiku`, `sonnet[1m]`, `opusplan`
+- Aliases: `opus`, `sonnet`, `haiku`, `opusplan`
+- Extended context: `claude --betas context-1m-2025-08-07`
```

### Codex CLI Section
```diff
 | Model | Context Window | Max Output | Notes |
 |-------|----------------|------------|-------|
 | GPT-5.2-Codex | 400k | 128k | Default since Jan 2026, context compaction support |
-| GPT-5.1-Codex-Max | 400k | 128k | Long-horizon agentic tasks |
-| GPT-5.1-Codex | 400k | 128k | Agentic coding optimized |
-| GPT-5.1-Codex-Mini | 400k | 128k | Cost-effective |
-| GPT-5-Codex | 400k | 128k | Context compaction support |
-| GPT-5 | 400k | 128k | General purpose |
+| GPT-5.1-Codex-Max | 400k+ | 128k | Native context compaction, works across millions of tokens |
+| GPT-5.1-Codex-Mini | 400k | 128k | Lighter, more affordable variant |
 | codex-1 | 192k | - | Specialized o3 variant for coding |
-| codex-mini | 200k | 100k | Fine-tuned o4-mini, low-latency |
+| codex-mini-latest | 200k | 100k | **Default model**, fine-tuned o4-mini, low-latency |
 | o3 | 200k | 100k | Latest reasoning model |
 | o4-mini | 200k | 100k | Fast, efficient reasoning |
```

### Cursor Section
```diff
+### Cursor Native Models
+
+| Model | Context Window | Max Output | Notes |
+|-------|----------------|------------|-------|
+| Composer 1 | 150-180k | N/A | Native MoE model, 250 tokens/sec, $1.25/M input |
+
 ### xAI Models

 | Model | Context Window | Max Output | Notes |
 |-------|----------------|------------|-------|
-| Grok 4 | 256k | 8k | Agent/Thinking modes |
-| Grok 4 Fast | 200k (2M max) | 8k | **Largest context available** |
-| Grok Code | 256k | 8k | Code-specialized |
+| Grok Code Fast 1 | 256k | N/A | 70.8% SWE-bench, fastest, $0.20/M input |
+
+### DeepSeek Models
+
+| Model | Context Window | Max Output | Notes |
+|-------|----------------|------------|-------|
+| DeepSeek Coder V2 | 128k | N/A | Open-source, cost-effective |
+| DeepSeek V3 | 64-128k | N/A | Native Cursor support, free |
```

### Gemini CLI Section
```diff
+### Deprecation Timeline
+
+| Model | Shutdown Date |
+|-------|---------------|
+| Gemini 2.0 Flash | March 31, 2026 |
+| Gemini 2.0 Flash-Lite | March 31, 2026 |
+| Gemini 2.5 Pro | June 17, 2026 |
+| Gemini 2.5 Flash | June 17, 2026 |
+| Gemini 2.5 Flash-Lite | July 22, 2026 |
```

---

## Corrections Required

1. **Cursor 2M Context**: The current README claims Cursor has 2M context with Grok 4 Fast. Research found no evidence of this - maximum is 1M with Gemini models. The "Grok 4 Fast" model appears to be "Grok Code Fast 1" with 256k context.

2. **Claude Code Extended Context**: The `[1m]` suffix notation should be replaced with the actual beta flag: `--betas context-1m-2025-08-07`

3. **Codex CLI Default Model**: `codex-mini` should be `codex-mini-latest` as this is the official model ID.

---

## Research Session Complete

All 4 agents completed their research successfully. The research.md file contains detailed findings from each agent with sources.

---

## Update Applied

**User Approved:** Yes
**Updated Files:**
- `README.md` - Quick comparison table corrected
- `reports/context-comparison.md` - Full report updated with:
  - Claude Code: Fixed extended context syntax
  - Codex CLI: Renamed codex-mini to codex-mini-latest, streamlined model list
  - Cursor: Removed incorrect 2M claim, added Composer 1, DeepSeek models, Grok Code Fast 1
  - Gemini CLI: Added deprecation timeline
