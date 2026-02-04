# Feature Comparison Report

> **Last Updated:** 2026-02-04 (Research Session)

## Overview

A comprehensive comparison of features across the four major AI coding assistants: Claude Code, Codex CLI, Gemini CLI, and Cursor.

### Legend
- ✅ Full Support
- ⚠️ Partial/Limited Support
- ❌ Not Available

---

## Hooks

Shell commands triggered by events during AI operation.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | 12 event types, 3 hook types (command, prompt, agent), async support |
| Codex CLI | ⚠️ Limited | Only notification hook officially supported; comprehensive hooks proposed but not accepted |
| Gemini CLI | ✅ Full | Enabled by default since v0.26.0+, scripts at lifecycle events |
| Cursor | ✅ Full | Enterprise-grade with partner integrations, 10-20x performance improvement |

### Claude Code Hooks

Claude Code provides the most comprehensive hooks system with 12 event types:

| Event | Trigger |
|-------|---------|
| SessionStart | When session begins/resumes |
| UserPromptSubmit | Before Claude processes user prompt |
| PreToolUse | Before tool execution (can block) |
| PermissionRequest | When permission dialog appears |
| PostToolUse | After successful tool execution |
| PostToolUseFailure | After tool execution fails |
| Notification | When Claude Code sends notifications |
| SubagentStart | When subagent spawns |
| SubagentStop | When subagent finishes |
| Stop | When Claude finishes responding |
| PreCompact | Before context compaction |
| SessionEnd | When session terminates |

**Hook Types:**
- Command hooks (`type: "command"`) - Execute shell scripts
- Prompt hooks (`type: "prompt"`) - Single-turn LLM evaluation
- Agent hooks (`type: "agent"`) - Multi-turn subagent with tool access
- Async hooks support with `"async": true` for non-blocking execution

### Codex CLI Hooks

Limited official support:
- **Notification hook**: Built-in, triggers when Codex completes a task
- Comprehensive hooks system proposed (PR #9796) but not yet accepted

### Gemini CLI Hooks

Full support (enabled by default since v0.26.0+):
- Scripts execute at specific points in the agentic loop
- Extensions can bundle hooks directly
- Supports variable substitution in hooks/hooks.json
- Controls and customizes the agent loop at lifecycle events

### Cursor Hooks

Enterprise-grade hooks system (January 2026):
- Observe, block, and extend agent loop operations
- Auto-formatting after edits, gating dangerous commands
- **Performance:** 10-20x faster following January 8, 2026 CLI update
- **Enterprise Partners:** MintMCP, Oasis Security, Runlayer, Semgrep

---

## Plugins/MCP

Extension system via Model Context Protocol and plugin architecture.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | Full MCP support with dynamic tool loading, OAuth support |
| Codex CLI | ✅ Full | MCP + Agent Skills system (production-ready) |
| Gemini CLI | ✅ Full | Robust extension ecosystem, browse at geminicli.com/extensions |
| Cursor | ✅ Full | MCP + VS Code extensions (some Microsoft restrictions) |

### Claude Code MCP

- Full Model Context Protocol implementation
- Dynamic tool loading at runtime
- OAuth support for authenticated services
- Configure in `~/.claude/mcp_servers.json`
- Auto-enable threshold with `auto:N` syntax

### Codex CLI MCP + Agent Skills

- **MCP servers** officially supported for third-party tools
- **Agent Skills** (production-ready): Reusable bundles of instructions
  - Invoke with `$skill-name` (e.g., `$skill-installer`)
  - Auto-selected by Codex based on prompt context
  - Install in `~/.codex/skills` (user) or `.codex/skills` (project)

### Gemini CLI Extensions

- Robust extension ecosystem at geminicli.com/extensions
- Package prompts, MCP servers, Agent Skills, and custom commands
- Easy one-command installation
- Configure via `/extensions` command

### Cursor MCP + Extensions

- Full MCP support with `/mcp enable` and `/mcp disable` commands
- Dynamic context discovery (46.9% token reduction)
- VS Code extension compatibility (some Microsoft-specific restrictions)
- MCP governance via partner integrations

---

## Sub-agents

Ability to spawn parallel worker processes for complex tasks.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | Task tool (7 parallel) + custom persistent subagents |
| Codex CLI | ✅ Via MCP | codex-as-mcp, codex-subagents-mcp, manual orchestration |
| Gemini CLI | ⚠️ Limited | No native support; shell spawning workarounds |
| Cursor | ✅ Full | Up to 8 parallel agents via git worktrees, background agents |

### Claude Code Sub-agents

- **Task Tool**: Up to 7 parallel agents
- **Custom Subagents**: Define in `.claude/agents/` directory
- **Agent Types**: Explore, Plan, Bash, general-purpose, and custom

### Codex CLI Sub-agents

- Via MCP packages:
  - `codex-as-mcp`: Use Codex as an MCP server
  - `codex-subagents-mcp`: Full multi-agent orchestration
- Manual orchestration also possible

### Gemini CLI Sub-agents

- No native sub-agent support
- Workarounds via shell spawning multiple instances

### Cursor Sub-agents

- Up to 8 parallel agents via git worktrees
- Background agents for long-running tasks
- Isolated Ubuntu VMs for background execution

---

## Slash Commands

Built-in commands for common operations.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | /help, /clear, /context, /init, /commit, /pr-comments, /model, /cost, /stats |
| Codex CLI | ✅ Full | /quit, /mention, /new, /resume, /fork, /review, /model, /approvals, /compact |
| Gemini CLI | ✅ Full | /help, /model, /chat, /memory, /extensions, /settings, /stats |
| Cursor | ✅ Full | /summarize, custom commands via .cursor/commands/ |

### Claude Code Commands

| Command | Description |
|---------|-------------|
| `/help` | Show help information |
| `/clear` | Clear conversation |
| `/context` | Show context usage |
| `/init` | Initialize CLAUDE.md |
| `/commit` | Create git commit |
| `/pr-comments` | Review PR comments |
| `/model` | Switch model |
| `/cost` | Show cost information |
| `/stats` | Show session statistics |

### Codex CLI Commands

| Command | Description |
|---------|-------------|
| `/quit` | Exit the CLI |
| `/mention` | Mention files/context |
| `/new` | Start new session |
| `/resume` | Resume previous session |
| `/fork` | Fork current session |
| `/review` | Review code |
| `/model` | Switch model |
| `/approvals` | Manage approval settings |
| `/compact` | Compact context |

### Gemini CLI Commands

| Command | Description |
|---------|-------------|
| `/help` | Show help |
| `/model` | Switch model |
| `/chat` | Manage chat sessions |
| `/memory` | Memory commands |
| `/extensions` | Manage extensions |
| `/settings` | View/edit settings |
| `/stats` | Show usage statistics |

### Cursor Commands

| Command | Description |
|---------|-------------|
| `/summarize` | Summarize content |
| Custom | Via `.cursor/commands/` directory |

---

## Custom Commands

User-defined commands and prompts.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | Skills in ~/.claude/skills/, commands in ~/.claude/commands/ |
| Codex CLI | ✅ Full | Custom prompts in ~/.codex/, invoked as /prompts:name |
| Gemini CLI | ✅ Full | TOML files in ~/.gemini/commands/, supports {{args}} placeholders |
| Cursor | ✅ Full | .cursorrules, Project Rules in .cursor/rules/, Global Rules |

### Claude Code Custom Commands

- **Skills**: `~/.claude/skills/` - Full skill definitions
- **Commands**: `~/.claude/commands/` - Markdown command templates
- Invoked with `/command-name`

### Codex CLI Custom Commands

- Location: `~/.codex/prompts/`
- Invoked as `/prompts:name`
- Supports variable substitution

### Gemini CLI Custom Commands

- Location: `~/.gemini/commands/`
- Format: TOML configuration files
- Supports `{{args}}` placeholders for arguments

### Cursor Custom Commands

- **Project Rules**: `.cursor/rules/` directory
- **Global Rules**: In Cursor settings
- **.cursorrules**: Project-level AI behavior customization

---

## IDE Integration

Editor and development environment support.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | VS Code extension + JetBrains plugin |
| Codex CLI | ✅ Full | VS Code extension + native JetBrains (Jan 2026) |
| Gemini CLI | ✅ Full | VS Code (official) + JetBrains (3rd party plugin) |
| Cursor | ✅ Standalone | VS Code fork - standalone IDE, not a plugin |

### Claude Code IDE Support

- **VS Code**: Official extension
- **JetBrains**: Official plugin for IntelliJ, PyCharm, etc.

### Codex CLI IDE Support

- **VS Code**: Official extension
- **JetBrains**: Native integration (January 2026)

### Gemini CLI IDE Support

- **VS Code**: Official extension
- **JetBrains**: Third-party plugin available

### Cursor IDE

- Standalone IDE based on VS Code fork
- Not available as a plugin for other editors
- Full VS Code extension compatibility

---

## Git Integration

Version control features and automation.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | GitHub + GitLab, PR/MR creation, commit generation |
| Codex CLI | ✅ Full | Deep git integration, GitHub Actions, review workflows |
| Gemini CLI | ⚠️ Partial | Git-aware filtering only; native git operations requested |
| Cursor | ✅ Full | Native git + PR creation via GitHub MCP |

### Claude Code Git Features

- GitHub and GitLab support
- PR/MR creation and management
- Automatic commit message generation
- `/commit` and `/pr-comments` commands
- GitHub Actions integration with `@claude` mentions
- GitLab CI/CD event-driven automation

### Codex CLI Git Features

- Deep git integration
- Built-in `/diff` command for reviewing changes
- GitHub Actions support
- Code review workflows with `/review` command
- Session-based change tracking

### Gemini CLI Git Features

**Currently Available:**
- Git-aware filtering: @ commands exclude git-ignored files by default
- Automatic exclusion of .git/, node_modules/, dist/, .env
- Can execute git operations through shell commands

**Requested Features (Not Yet Available):**
- Native git operations (create commits, branches, PRs)
- Direct git integration tools

### Cursor Git Features

- Git history indexing with commit SHAs and parent info
- Automatic PR indexing for all merged PRs
- Merkle tree-based efficient updates (10-minute intervals)
- GitButler integration for auto-commits

---

## Web Search

Internet search capability for real-time information.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | WebSearch + WebFetch tools (API only, not Bedrock/Vertex) |
| Codex CLI | ✅ Full | Built-in, --search flag for live results |
| Gemini CLI | ✅ Full | Google Search grounding via google_web_search tool |
| Cursor | ✅ Full | @Web command powered by Exa/SerpApi |

### Claude Code Web Search

- **WebSearch**: Search the web for information
- **WebFetch**: Fetch and analyze web pages
- Availability: API only (not on Bedrock/Vertex)

### Codex CLI Web Search

- Built-in web search capability
- `--search` flag for live results
- Integrated into conversation flow

### Gemini CLI Web Search

- Google Search grounding via `google_web_search` tool
- Native Google integration
- Real-time search results

### Cursor Web Search

- `@Web` command
- Powered by Exa/SerpApi
- Context-aware search results

---

## Image Support

Visual input analysis and multimodal capabilities.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ⚠️ Limited | JPEG/PNG/GIF/WebP; some CLI limitations |
| Codex CLI | ✅ Full | --image flag, paste in TUI, multiple images |
| Gemini CLI | ✅ Full | Multimodal input, Windows clipboard paste (Alt+V) |
| Cursor | ⚠️ Partial | Multimodal AI yes; terminal image output limited |

### Claude Code Image Support

- Formats: JPEG, PNG, GIF, WebP
- Some CLI limitations for image display
- Read tool can analyze images

### Codex CLI Image Support

- `--image` flag for image input
- Paste directly in TUI
- Multiple images supported per prompt

### Gemini CLI Image Support

- Full multimodal input support
- Windows clipboard paste with Alt+V
- Image analysis and generation (with appropriate model)

### Cursor Image Support

- Multimodal AI capabilities
- Terminal image output limited
- Works well in IDE context

---

## Memory/Persistence

Cross-session context retention.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ⚠️ Partial | CLAUDE.md files; no native cross-session memory |
| Codex CLI | ✅ Full | JSONL sessions, resume/fork, excellent persistence |
| Gemini CLI | ✅ Full | GEMINI.md files, /memory commands, chat save/resume |
| Cursor | ⚠️ MCP Only | No native memory; requires MCP solutions (knowledge-graph, etc.) |

### Claude Code Memory

- **CLAUDE.md**: Project-level context files
- No native cross-session memory
- Context automatically summarized at compaction

### Codex CLI Memory

- JSONL session files
- `/resume` to continue sessions
- `/fork` to branch sessions
- Excellent persistence support

### Gemini CLI Memory

- **GEMINI.md**: Project-level context
- `/memory` commands for explicit memory management
- Chat save and resume functionality

### Cursor Memory

- No native memory system
- Requires MCP solutions:
  - knowledge-graph MCP
  - Custom memory MCP servers

---

## Multi-file Editing

Coordinated changes across multiple files.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | Coordinated edits, git worktrees for parallel sessions |
| Codex CLI | ✅ Full | Batch operations, parallel tool calling |
| Gemini CLI | ✅ Full | Edit multiple files in one session |
| Cursor | ✅ Full | Composer handles 22,000+ lines, 151+ files |

### Claude Code Multi-file

- Coordinated edits across files
- Git worktrees for parallel editing sessions
- Edit tool with file path specification

### Codex CLI Multi-file

- Batch file operations
- Parallel tool calling
- Atomic multi-file changes

### Gemini CLI Multi-file

- Edit multiple files in single session
- Coordinated changes

### Cursor Multi-file (Composer)

- Industry-leading: 22,000+ lines across 151+ files
- Composer mode for large-scale changes
- Agent mode for autonomous refactoring

---

## Auto-commit

Automatic git commit creation.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ⚠️ Partial | Via custom /commit command and third-party tools |
| Codex CLI | ⚠️ Partial | Can commit but requires approval (by design) |
| Gemini CLI | ✅ Full | Built-in tool + geminicommit CLI |
| Cursor | ✅ Full | Via hooks system and GitButler integration |

### Claude Code Auto-commit

- Custom `/commit` command
- Third-party tools available
- Not fully automatic (by design for safety)

### Codex CLI Auto-commit

- Can create commits
- Requires approval (safety by design)
- Part of approval tier system

### Gemini CLI Auto-commit

- Built-in commit tool
- `geminicommit` CLI for standalone use
- Automatic commit message generation

### Cursor Auto-commit

- Via hooks system (`afterFileEdit`)
- GitButler integration
- Can be fully automated

---

## Custom System Prompts

Customizing AI behavior with system-level instructions.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | CLAUDE.md, --append-system-prompt, Agent SDK, subagents |
| Codex CLI | ⚠️ Experimental | experimental_instructions_file; may break between versions |
| Gemini CLI | ✅ Full | GEMINI_SYSTEM_MD env var for complete override |
| Cursor | ✅ Full | .cursorrules, project rules, global rules |

### Claude Code System Prompts

- **CLAUDE.md**: Project-level instructions
- `--append-system-prompt`: CLI flag for additional instructions
- **Agent SDK**: Full system prompt control
- **Subagents**: Custom system prompts per agent

### Codex CLI System Prompts

- `experimental_instructions_file` option
- May break between versions (experimental)
- Limited official support

### Gemini CLI System Prompts

- `GEMINI_SYSTEM_MD` environment variable
- Complete system prompt override
- GEMINI.md for project context

### Cursor System Prompts

- **.cursorrules**: Project-level AI behavior
- **Project Rules**: `.cursor/rules/` directory
- **Global Rules**: Application-wide settings

---

## Cost Tracking

Token usage and cost monitoring.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ✅ Full | /cost, /stats, workspace-based centralized tracking |
| Codex CLI | ❌ None | No built-in cost tracking; community-requested feature |
| Gemini CLI | ✅ Full | /stats, OpenTelemetry, Google Cloud Monitoring dashboards |
| Cursor | ⚠️ Limited | Basic usage display; no detailed cost breakdown |

### Claude Code Cost Tracking

- `/cost`: Detailed token usage statistics per session
- `/stats`: Usage patterns (subscribers)
- Workspace-based centralized cost tracking via Claude Console
- Auto-created "Claude Code" workspace for organization cost management
- Context awareness feature tracks remaining context window

### Codex CLI Cost Tracking

**Current State:** No built-in cost tracking or usage analytics
- GitHub Issue #5085 proposes cost/usage analytics module
- Users face unpredictable bills without visibility into session costs
- Workaround: Manual tracking based on API pricing

### Gemini CLI Cost Tracking

- `/stats`: Token usage, cached token savings, session duration
- Summary presented on exit
- OpenTelemetry integration
- Google Cloud Monitoring dashboards

### Cursor Cost Tracking

- Basic usage display in UI
- No detailed cost breakdown
- Limited compared to CLI tools

---

## Sandbox Mode

Isolated execution environment for safety.

| Tool | Status | Details |
|------|--------|---------|
| Claude Code | ❌ None | No built-in sandbox |
| Codex CLI | ✅ Full | Landlock (Linux), Seatbelt (macOS), 3 modes (read-only, workspace-write, full-access) |
| Gemini CLI | ✅ Full | Docker/Podman containers, macOS Seatbelt |
| Cursor | ⚠️ Limited | Background agents run in isolated Ubuntu VMs |

### Claude Code Sandbox

- No built-in sandbox
- Relies on user environment isolation

### Codex CLI Sandbox

Three-tier sandbox system:
- **Read-only**: Cannot modify files
- **Workspace-write**: Write only to workspace
- **Full-access**: No restrictions

Technologies:
- **Linux**: Landlock LSM
- **macOS**: Seatbelt sandbox

### Gemini CLI Sandbox

- Docker/Podman container isolation
- macOS Seatbelt for native sandboxing
- Configure via settings

### Cursor Sandbox

- Background agents run in isolated Ubuntu VMs
- Limited sandbox for regular operations

---

## Key Differentiators

| Tool | Strongest Features |
|------|-------------------|
| **Claude Code** | Best hooks system, powerful sub-agents (Task tool), comprehensive MCP support, strong IDE integrations |
| **Codex CLI** | Excellent sandbox security, best session persistence, strong CI/CD support, three-tier approval system |
| **Gemini CLI** | Best extension ecosystem, native Google Cloud integration, 1M token context on all models, built-in cost tracking |
| **Cursor** | Best multi-file editing (Composer), parallel background agents, seamless VS Code experience, codebase indexing |

---

## Research Sources

### Claude Code
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Anthropic Models](https://docs.anthropic.com/en/docs/about-claude/models)

### Codex CLI
- [Codex CLI GitHub](https://github.com/openai/codex)
- [OpenAI Platform](https://platform.openai.com/docs)

### Gemini CLI
- [Gemini CLI GitHub](https://github.com/google-gemini/gemini-cli)
- [Gemini Extensions](https://geminicli.com/extensions)

### Cursor
- [Cursor Documentation](https://cursor.com/docs)
- [Cursor Changelog](https://cursor.com/changelog)
