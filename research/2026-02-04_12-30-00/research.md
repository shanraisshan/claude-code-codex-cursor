# Context Window & Features Research Session

**Started:** 2026-02-04 12:30:00
**Completed:** 2026-02-04
**Status:** Complete

---

## Claude Code Research
**Agent:** Dr. Sarah Chen
**Status:** Complete

### Context Windows

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| Claude Opus 4.5 | 200K tokens | 64K tokens | Released Nov 24, 2025; flagship model at 67% lower cost than predecessor |
| Claude Sonnet 4.5 | 200K tokens / 1M tokens (beta) | 64K tokens | 1M beta requires `context-1m-2025-08-07` header; best coding model; context awareness feature |
| Claude Haiku 4.5 | 200K tokens | 64K tokens | Fastest model; unbeatable for UI work; context awareness feature |

**Legacy Models (Still Available):**
- Claude Opus 4.1: 200K tokens, 32K max output ($15/$75 per MTok)
- Claude Sonnet 4: 200K / 1M beta, 64K max output
- Claude Sonnet 3.7: 200K tokens, 64K / 128K beta max output
- Claude Opus 4: 200K tokens, 32K max output
- Claude Haiku 3: 200K tokens, 4K max output

**Key Details:**
- Context window budget set to 200K (standard), 500K (Enterprise), or 1M (beta for tier 4 orgs)
- Sonnet 4.5 and Haiku 4.5 feature **context awareness**: models track remaining context window throughout conversation
- Long context pricing applies to requests exceeding 200K tokens
- Model aliases (e.g., `claude-sonnet-4-5`) auto-point to latest snapshot; use specific versions in production
- Extended thinking enabled by default with 31,999 token budget

### Features

#### Hooks Support
**Status:** Full support with comprehensive event system

**Event Types:**
- `SessionStart` - When session begins/resumes (matcher: startup/resume/clear/compact)
- `UserPromptSubmit` - Before Claude processes user prompt
- `PreToolUse` - Before tool execution; can block (matcher: tool name)
- `PermissionRequest` - When permission dialog appears (matcher: tool name)
- `PostToolUse` - After successful tool execution (matcher: tool name)
- `PostToolUseFailure` - After tool execution fails (matcher: tool name)
- `Notification` - When Claude Code sends notifications (matcher: permission_prompt/idle_prompt/auth_success/elicitation_dialog)
- `SubagentStart` - When subagent spawns (matcher: agent type)
- `SubagentStop` - When subagent finishes (matcher: agent type)
- `Stop` - When Claude finishes responding
- `PreCompact` - Before context compaction (matcher: manual/auto)
- `SessionEnd` - When session terminates (matcher: reason codes)

**Hook Types:**
- Command hooks (`type: "command"`) - Execute shell scripts
- Prompt hooks (`type: "prompt"`) - Single-turn LLM evaluation
- Agent hooks (`type: "agent"`) - Multi-turn subagent with tool access
- Async hooks support with `"async": true` for non-blocking execution

**Hook Locations:**
- `~/.claude/settings.json` (global)
- `.claude/settings.json` (project, shareable)
- `.claude/settings.local.json` (project, gitignored)
- Managed policy settings (organization-wide)
- Plugin `hooks/hooks.json`
- Skill/agent frontmatter

**Management:**
- `/hooks` interactive menu for viewing, adding, deleting hooks
- Environment variables: `$CLAUDE_PROJECT_DIR`, `${CLAUDE_PLUGIN_ROOT}`, `$CLAUDE_ENV_FILE`
- Decision control: allow/deny/ask with reason, updatedInput, additionalContext
- JSON input/output on stdin/stdout, exit codes for control

#### MCP (Model Context Protocol) Support
**Status:** Full support with plugin integration

- MCP server tools appear as regular tools in hook events
- Naming pattern: `mcp__<server>__<tool>` (e.g., `mcp__memory__create_entities`)
- Configurable via `.mcp.json` in plugins
- Auto-enable threshold with `auto:N` syntax (N = context window percentage 0-100)
- MCP tools can be matched in hooks using regex patterns
- Supports external tool configuration with MCP servers

#### Sub-agents/Task Tool
**Status:** Full support with recent v2.1.16+ major improvements

**Built-in Sub-agents:**
- Fast, read-only agent for searching/analyzing codebases
- Specialized agents: Bash, Explore, Plan
- Up to 7 agents running simultaneously

**Recent Updates (v2.1.16, January 2026):**
- Moved from ephemeral "To-dos" to persistent "Tasks"
- Support for directed acyclic graphs (DAGs) where tasks can block others
- Coordinating work across sessions, subagents, and context windows
- v2.1.17 patch fixed out-of-memory crashes with heavy subagent usage

**Custom Sub-agents:**
- Define in Markdown files with YAML frontmatter
- Located in `.claude/agents/`
- Custom prompts, tool restrictions, permission modes, hooks, and skills
- Created manually or via `/agents` command
- Can be invoked via Task tool with `subagent_type` parameter

#### Slash Commands
**Status:** Full support, merged with skills system (v2.1.3+)

**Built-in Commands:**
- `/help` - Show all commands
- `/clear` - Clear history
- `/init` - Create CLAUDE.md
- `/doctor` - Diagnose issues
- `/compact` - Compact context
- `/resume` - Resume session
- `/config` - Configuration management
- `/cost` - Display token usage and costs
- `/stats` - View usage patterns (subscribers)
- `/hooks` - Interactive hooks manager
- `/agents` - Manage custom agents

**Custom Commands:**
- Store in `~/.claude/commands/` (global) or `.claude/commands/` (project)
- Markdown files with `.md` extension
- Use `$ARGUMENTS` placeholder for parameters
- Written in natural language
- Unified with skills system: commands and skills create same `/command` interface

#### Custom Commands/Skills
**Status:** Full support with unified system

- Skills stored in `.claude/skills/<name>/SKILL.md`
- Commands and skills merged in v2.1.3 - both work identically
- YAML frontmatter for configuration
- Supports hooks, custom prompts, tool restrictions
- Can include `once: true` for single-run hooks
- Agent Skills available for specialized tasks
- MCP server tools can be integrated into skills

#### IDE Integrations
**Status:** Full support across multiple platforms

**Available Platforms:**
- **Terminal (CLI)** - Core experience, run `claude` in any terminal
- **VS Code** - Native extension with inline diffs, @-mentions, plan review
- **JetBrains IDEs** - Plugin for IntelliJ IDEA, PyCharm, WebStorm with IDE diff viewing, context sharing
- **Desktop app** - Standalone with diff review, parallel sessions via git worktrees, cloud sessions
- **Web** - Browser at claude.ai/code, iOS app, no local setup required, parallel tasks, built-in diff view
- **Chrome** - Browser extension for live debugging, design verification, web app testing

#### Git Integration
**Status:** Full support with automation capabilities

- Handle git workflows through natural language
- Resolve merge conflicts
- Create commits and PRs
- Write release notes automatically
- GitHub Actions integration with `@claude` mentions
- GitLab CI/CD event-driven automation
- Works in CI for automated code review and issue triage
- Desktop app supports parallel sessions via git worktrees

#### Web Search Capability
**Status:** Full support via WebSearch tool

- WebSearch tool available as built-in tool
- Supports query parameters, allowed_domains, blocked_domains
- Can be matched in hooks with tool name "WebSearch"
- Maintains awareness to find up-to-date information from the web
- Integrated into agentic loop for information retrieval

#### Sandbox/Security Features
**Status:** Enterprise-grade security with permission system

**Permission System:**
- Multiple permission modes: default, plan, acceptEdits, dontAsk, bypassPermissions
- Permission dialogs for tool execution
- Permission rules for "always allow" patterns
- Hooks can intercept and control permissions (PermissionRequest event)
- Managed policy settings for organization-wide control
- Enterprise admins can use `allowManagedHooksOnly` to block user/project/plugin hooks

**Security Features:**
- Enterprise-grade security, privacy, and compliance built-in
- Use Claude API, or host on AWS Bedrock or GCP Vertex AI
- Hooks run with user permissions (security considerations required)
- Sessions capture hooks snapshot at startup (prevents mid-session modifications)
- External hook modifications require review in `/hooks` menu
- Environment isolation with `$CLAUDE_CODE_REMOTE` variable for remote sessions

**Best Practices:**
- Validate and sanitize inputs
- Quote shell variables
- Block path traversal
- Use absolute paths
- Skip sensitive files

#### Cost Tracking Options
**Status:** Full support with detailed tracking

**Cost Tracking Features:**
- `/cost` command displays detailed token usage statistics per session
- Shows total cost, API duration, wall duration, code changes
- `/stats` command for usage patterns (subscribers)
- Workspace-based centralized cost tracking via Claude Console
- Auto-created "Claude Code" workspace for organization cost management

**Token Budget Management:**
- Extended thinking enabled by default with 31,999 token budget
- Configurable via `/config` or `MAX_THINKING_TOKENS` setting
- Context awareness feature tracks remaining context window
- Long context pricing for requests exceeding 200K tokens

**Average Costs (2026):**
- Average: $100-200/developer per month with Sonnet 4.5
- Average $6/day, 90% of developers under $12/day
- Variance based on automation usage and instance count

**Pricing Plans:**
- Pro: $20/month
- Max 5x: $100/month (5x token capacity)
- Max 20x: $200/month (20x token capacity)
- Teams: $150/month per developer (minimum 5 seats)

**Additional Features:**
- Composable and scriptable (Unix philosophy)
- CLAUDE.md for static context and instructions
- Slack integration with Claude mentions
- Reference implementation in development containers
- Auto-updates for native installations
- Debug mode with `claude --debug`
- Verbose mode toggle with `Ctrl+O`

---

## Codex CLI Research
**Agent:** Marcus Thompson
**Status:** Complete

### Context Windows

OpenAI Codex CLI in 2026 uses a fundamentally different approach to context windows compared to traditional fixed-size models. The latest models employ **context compaction technology** that allows them to work across multiple context windows.

| Model | Context Window | Max Output | Notes |
|-------|----------------|------------|-------|
| GPT-5.2-Codex | 400K tokens | 128K tokens | Latest model released Jan 14, 2026. Fixed large context window with improved long-context understanding, reliable tool calling, and native compaction |
| GPT-5.1-Codex-Max | Multi-window (millions of tokens) | N/A | First model natively trained for compaction. Automatically summarizes and compacts when approaching limits, enabling coherent work over millions of tokens in a single task |
| GPT-5-Codex | 200K tokens | N/A | Standard model with 200K context window |
| codex-mini-latest | ~200K tokens | N/A | **DEPRECATED** - Removal from API on January 16, 2026 |

**Key Innovation - Context Compaction:**
- GPT-5.1-Codex-Max and GPT-5.2-Codex feature native compaction technology
- Automatically summarizes conversation history when approaching context limits
- Provides a "fresh" context window and repeats the process as needed
- Enables long-running coding tasks spanning millions of tokens
- More token-efficient reasoning for extended sessions

**Model Evolution:**
- Original Codex models (code-davinci-002) were deprecated in March 2023
- Codex functionality now integrated into GPT-5 series models
- Modern Codex is a complete coding agent rather than just a model

### Features

#### Hooks Support
**Status:** Limited/Community-Requested

- **Notification Hook:** Built-in hook that triggers when Codex completes a task (officially supported)
- **Comprehensive Hooks System:** Community PR #9796 proposed extensive hooks (tool, file, event lifecycle) but OpenAI is **not accepting feature contributions** at this time
- **Proposed Hook Types:** before/after tool execution, before/after file write operations, prompt gating, stop hooks, compact mode notifications
- **Current Limitation:** OpenAI needs to ensure features are well-designed and consistent across all Codex surfaces (CLI, IDE, web) before accepting

#### MCP/Plugin Support
**Status:** Full Support

- **Model Context Protocol (MCP):** Officially supported for third-party tools and context integration
- **Agent Skills:** Reusable bundles of instructions to automate tasks
  - Invoke explicitly with `$skill-name` (e.g., `$skill-installer`, `$create-plan`)
  - Can be auto-selected by Codex based on prompt context
  - Install user-specific skills in `~/.codex/skills`
  - Check project-specific skills into `.codex/skills` for team sharing

#### Sub-agents Capability
**Status:** Native Agent Architecture

- Codex operates as a "Software Engineer teammate" connecting models, local tooling, and cloud
- Multi-surface architecture (CLI, IDE extension, macOS app, web at chatgpt.com/codex)
- Agent loop unrolls tasks into planning, execution, and review phases
- Dedicated reviewer mode with `/review` command

#### Slash Commands
**Status:** Full Support

- **`/diff`** - Inspect Git diff (staged, unstaged, untracked files)
- **`/mention`** - Add files to conversation by path
- **`/new`** - Start fresh conversation in same session
- **`/resume`** - Reload and continue previous conversation
- **`/model`** - Switch between GPT-5-Codex, GPT-5, or adjust reasoning levels
- **`/review`** - Launch dedicated code reviewer for diff analysis
- **Custom Commands:** Create custom prompts that behave like slash commands with arguments and metadata

#### Custom Commands
**Status:** Full Support

- Users can create custom prompts functioning as new slash commands
- Support for arguments and metadata
- Custom skills can be installed globally or per-project

#### IDE Integrations
**Status:** Full Support

- **Supported IDEs:** VS Code, Cursor, Windsurf
- IDE extension provides same slash commands as CLI
- Seamless context switching between terminal CLI, IDE extension, and web interface
- Local and cloud mode switching available

#### Git Integration
**Status:** Full Support

- Built-in `/diff` command for reviewing changes
- Automatic transcript of all actions for audit trail
- Recommended workflow: create Git checkpoints before/after tasks
- Easy rollback with standard Git commands
- Codex surfaces changes for review before committing

#### Web Search Capability
**Status:** Full Support

- Built-in web search to get up-to-date information during tasks
- Integrated into the agent's tooling capabilities
- Available across all Codex surfaces (CLI, IDE, web)

#### Sandbox/Approval Modes
**Status:** Full Support

Multiple sandbox policies available via `--sandbox` flag:

- **`read-only`** - Commands can read files but cannot write anywhere (including /tmp)
- **`workspace-write`** - Default mode with:
  - Write permissions limited to active workspace
  - No network access by default (configurable)
  - Reads work broadly across filesystem
  - Recommended for most development work
- **`danger-full-access`** - Full write access to filesystem, removes all sandbox restrictions

**Approval Modes:**
- `--ask-for-approval on-request` - Approve on request
- `--full-auto` - Shortcut combining `on-request` approvals with `workspace-write` sandbox
- `--dangerously-bypass-approvals-and-sandbox` - Disables all protections (dangerous)

**Implementation:**
- macOS 12+: Apple Seatbelt with `sandbox-exec`
- Linux: Landlock/seccomp APIs

#### Cost Tracking Options
**Status:** None (Community-Requested)

- **Current State:** No built-in cost tracking or usage analytics
- **Community Request:** GitHub Issue #5085 proposes cost/usage analytics module
- **Problem:** Users face unpredictable bills without visibility into session costs or token consumption
- **Workaround:** Manual tracking based on API pricing

**2026 Pricing Context:**
- GPT-5-Codex: $1.25/M input tokens, $10.00/M output tokens
- GPT-5.1-Codex-Mini: $0.25/M input tokens, $2.00/M output tokens
- Codex-mini-latest: $1.50/M input tokens, $6.00/M output tokens
- Typical medium-sized code changes: $3-4 with o3 model
- ChatGPT Plus ($20/month): 30-150 local tasks every 5 hours
- ChatGPT Pro ($200/month): Unlimited o1 reasoning models for power users

**Notable Changes from Previous Research:**
1. New GPT-5.2-Codex model released (Jan 14, 2026) with 400K context window
2. codex-mini-latest deprecated (removed Jan 16, 2026)
3. Context compaction is now a core feature, not just experimental
4. Agent skills system is production-ready
5. Comprehensive hooks system exists as community PR but not yet merged
6. Cost tracking remains a requested feature, not implemented

---

## Cursor Research
**Agent:** Elena Rodriguez
**Status:** Complete

### Context Windows

Cursor IDE supports multiple AI model providers with varying context window configurations. As of February 2026, Cursor operates with a standard 200k token context window (~15,000 lines of code) in normal mode, with "Max Mode" extending the context window to the maximum available for supported models.

#### Anthropic Models

| Model | Context Window (Normal) | Max Mode | Notes |
|-------|------------------------|----------|-------|
| Claude Opus 4.5 | 200k tokens | 200k tokens | Released Nov 24, 2025; supports Infinite Chats feature |
| Claude Sonnet 4.5 | 200k tokens | 200k-1M tokens | Community reports varying limits; officially ~200k |

#### OpenAI Models

| Model | Context Window (Normal) | Max Mode | Notes |
|-------|------------------------|----------|-------|
| GPT-5.1 Codex Max | 200k tokens | 400k tokens | Added January 2026; improved tool calls |
| GPT-5.1 High | 200k tokens | 400k tokens | Frontier coding model |
| GPT-5 Mini | 200k tokens | N/A | Fast, lightweight option |
| GPT-5 Nano | 200k tokens | N/A | Ultra-fast for simple tasks |
| GPT-4.1 | 200k tokens | Supported | Legacy model, still available |

#### Google Models

| Model | Context Window (Normal) | Max Mode | Notes |
|-------|------------------------|----------|-------|
| Gemini 3 Pro Preview | 200k tokens | 1M tokens | Top performer on SWE-bench (76.2-78%) |
| Gemini 2.5 Flash | 200k tokens | 1M tokens | Fast inference, extended context available |

#### xAI Models

| Model | Context Window (Normal) | Max Mode | Notes |
|-------|------------------------|----------|-------|
| Grok 4 | 200k tokens | 2M tokens | Real-time web search integration |
| Grok Code Fast | 200k tokens | N/A | Optimized for speed |

#### DeepSeek Models

| Model | Context Window (Normal) | Max Mode | Notes |
|-------|------------------------|----------|-------|
| DeepSeek V3 | 200k tokens | N/A | Native support since v0.44+; hosted on US servers |
| DeepSeek R1 | 200k tokens | N/A | Native support since v0.45+; free within Pro plan |

#### Cursor Native Models

| Model | Context Window (Normal) | Max Mode | Notes |
|-------|------------------------|----------|-------|
| Composer 1 | ~200k tokens | N/A | 4x faster than comparable models; <30s response time |

**Key Context Management Features:**
- Dynamic context discovery reduces token usage by 46.9% for MCP tool calls
- Automatic summarization when context window fills
- Chat history preserved as files for context recovery
- Efficient updates via Merkle tree-based change detection

### Features

#### Hooks System (Enterprise-Grade)
**Status:** Full Support (January 2026)

- Observe, block, and extend agent loop operations
- Auto-formatting after edits
- Gating dangerous commands
- Adding commit checkpoints
- Redacting environment secrets
- **Performance:** 10-20x faster following January 8, 2026 CLI update
- **Enterprise Partners:** MintMCP (MCP governance), Oasis Security (access management), Runlayer (MCP broker), Semgrep (security scanning)

#### Model Context Protocol (MCP)
**Status:** Full Support (First-class integration)

- `/mcp enable` and `/mcp disable` commands for on-the-fly server management
- Dynamic context discovery for external tools and data sources
- 46.9% token reduction in agent runs using MCP tools
- MCP governance via partner integrations

#### VS Code Extension Compatibility
**Status:** Full Support

- Cursor is built on VS Code, maintaining full compatibility with VS Code extensions and marketplace

#### Parallel Agents / Sub-agents
**Status:** Full Support

- Multiple agents can run in parallel via Cursor 2.0
- Agent-centric interface for managing concurrent agents
- Background Agents for asynchronous tasks (auto-testing, dependency monitoring)
- Background agents run in isolated AWS VMs
- Trigger via Ctrl+E for background mode

#### Slash Commands
**Status:** Full Support

**Built-in Commands:**
- `/models` - List and switch between available models
- `/rules` - Create and edit rules from terminal
- `/mcp enable` / `/mcp disable` - Manage MCP servers

**Custom Commands:**
- Stored as Markdown files in `.cursor/commands/`
- Project-specific and global libraries
- Higher priority than rules (agent treats them as direct prompts)

#### Custom Rules (.cursorrules)
**Status:** Full Support

- Project-specific AI instructions for code generation
- Defined in `.cursorrules` files
- Automatically appended to agent context
- Community repository available (awesome-cursorrules)
- Lower priority than slash commands

#### Composer / Agent Mode
**Status:** Full Support (Cursor 2.0)

- **Composer 1:** Native ultra-fast coding model
- **Composer 2.0:** Added "Plan Mode" for step outlining before execution
- Multi-file editing with project-wide context
- Auto-runs terminal commands (foreground requires approval)
- Intelligent context retrieval from project index
- ~200k effective context window with augmentation

#### Git Integration
**Status:** Full Support

- Git history indexing with commit SHAs and parent info
- Automatic PR indexing for all merged PRs
- PR search and retrieval into agent context
- Merkle tree-based efficient updates (10-minute intervals)
- Clone via "Cursor: Clone" command for immediate indexing
- Privacy: obfuscated filenames, encrypted code chunks

#### Web Search (@Web)
**Status:** Full Support

- Integrated web search capability via @ mentions in chat interface

#### Background Agents
**Status:** Full Support (2026)

- Asynchronous task execution (testing, monitoring)
- Runs in isolated AWS infrastructure (VM-based)
- Auto-runs terminal commands without approval (unlike foreground)
- Trigger via Ctrl+E
- View status and enter machine from agent list

#### Codebase Indexing
**Status:** Full Support

**Technology:**
- Embedding-based indexing for all files
- Automatic indexing on project open
- Incremental indexing for new files
- Understands file relationships and components
- Git history indexing when enabled
- Merkle tree for efficient change detection (10-min intervals)

**Privacy:**
- Filenames obfuscated
- Code chunks encrypted
- Decryption on retrieval

#### CLI Support
**Status:** Full Support (January 2026)

- Model management commands
- MCP server controls
- Rules and commands management
- Performance improvements in v0.44-0.45+

---

## Gemini CLI Research
**Agent:** Dr. Raj Patel
**Status:** Complete

### Context Windows

**Current Stable Models (February 2026)**

| Model | Context Window | Max Output | Status |
|-------|----------------|------------|--------|
| Gemini 2.5 Pro | 1,048,576 (1M) | 65,536 | Stable |
| Gemini 2.5 Flash | 1,048,576 (1M) | 65,536 | Stable |
| Gemini 2.5 Flash-Lite | 1,048,576 (1M) | 65,536 | Stable |
| Gemini 2.5 Flash Image | 65,536 | 32,768 | Stable |
| Gemini 2.5 Flash Live | 131,072 | 8,192 | Preview |

**Preview Models (Gemini 3 Series)**

| Model | Context Window | Max Output | Status |
|-------|----------------|------------|--------|
| Gemini 3 Pro Preview | 1,048,576 (1M) | 65,536 | Preview |
| Gemini 3 Flash Preview | 1,048,576 (1M) | 65,536 | Preview |
| Gemini 3 Pro Image Preview | 65,536 | 32,768 | Preview |

**Deprecation Timeline**

| Model | Shutdown Date | Migration Path |
|-------|---------------|----------------|
| Gemini 2.0 Flash | March 31, 2026 | Gemini 2.5 Flash or Flash-Lite |
| Gemini 2.0 Flash-Lite | March 31, 2026 | Gemini 2.5 Flash-Lite |
| gemini-2.5-flash-image-preview | January 15, 2026 | Gemini 2.5 Flash Image (stable) |
| text-embedding-004 | January 14, 2026 | N/A |

**Key Insights:**
- All mainstream Gemini models support 1M+ token context windows (1,048,576 tokens)
- The 1M token window translates to approximately 1,500 pages of text or 30,000 lines of code
- Max output consistently at 65,536 tokens for Pro/Flash models, 32,768 for image-optimized variants
- Gemini 1.5 Pro can be upgraded to 2M tokens in certain configurations
- Free tier via Google AI API: 60 requests/minute, 1,000 requests/day

### Features

#### Hooks Support
**Status:** Full Support

- Enabled by default since v0.26.0+
- Scripts execute at specific points in the agentic loop
- Extensions can bundle hooks directly
- Supports variable substitution in hooks/hooks.json
- Allows customization without touching source code
- Controls and customizes the agent loop at lifecycle events

#### MCP/Extensions Support
**Status:** Full Support

**MCP (Model Context Protocol):**
- Configure connections to one or more MCP servers
- Discover and use custom tools
- Managed via `/mcp` command
- Extensions can package MCP servers with variable substitution

**Extensions System:**
- Package prompts, MCP servers, Agent Skills, and custom commands
- Easy one-command installation
- Browse extensions at geminicli.com/extensions
- Simple "playbook" architecture - set of tools extensions know how to use
- Can include context files (GEMINI.md), excluded tools, and custom commands
- Documentation updated as recently as January 28, 2026

#### Sub-agents Capability
**Status:** Preview

- Agent Skills provide on-demand expertise and specialized workflows
- Managed via `/skills` command
- Currently in preview status

#### Slash Commands
**Status:** Full Support

**30+ slash commands available across categories:**

**Session Management:**
- `/chat` - Save and resume conversation history for branching
- `/resume` - Browse and restore previous sessions interactively
- `/rewind` - Navigate backward through conversation history
- `/clear` - Wipe terminal display (Ctrl+L)
- `/quit` or `/exit` - Close application

**Information & Help:**
- `/help` or `/?` - Display available commands
- `/about` - Show version information
- `/stats` - Token usage, cached token savings, session duration
- `/tools` - List currently available tools with descriptions
- `/docs` - Open documentation in browser

**Configuration:**
- `/settings` - Open settings editor
- `/model` - Choose Gemini model via dialog
- `/theme` - Change visual appearance
- `/editor` - Select supported text editors
- `/auth` - Modify authentication methods

**Content & Tools:**
- `/memory` - Manage instructional context from GEMINI.md files
- `/copy` - Transfer last output to clipboard
- `/compress` - Replace chat context with summary to conserve tokens

**Development & Integration:**
- `/extensions` - View active extensions
- `/skills` - Manage Agent Skills
- `/hooks` - Control lifecycle event interception
- `/mcp` - Manage Model Context Protocol servers
- `/ide` - Configure IDE integration

**Other Utilities:**
- `/directory` or `/dir` - Handle multi-directory workspaces
- `/bug` - File GitHub issues
- `/vim` - Toggle vim-mode editing
- `/restore` - Revert files to pre-tool state (if checkpointing enabled)

#### Custom Commands (TOML)
**Status:** Full Support

- Defined via .toml files
- Supports {{args}} parameterization for reusable prompts
- Minimal configuration required (just prompt)
- Can execute shell commands
- Extensions can package custom commands
- Easy-to-use argument substitution

#### IDE Integrations
**Status:** Full Support

- VS Code compatibility confirmed
- Configured via `/ide` command
- Seamless integration with editor workflows

#### Git Integration
**Status:** Partial

**Currently Available:**
- Git-aware filtering: @ commands exclude git-ignored files by default
- Automatic exclusion of .git/, node_modules/, dist/, .env
- Can execute git operations through shell commands

**Requested Features:**
- Native git operations (create commits, branches, PRs)
- Show history and generate pull requests
- Potential tools: create_commit, create_pr, get_git_diff, get_git_log
- Feature requests pending for direct git integration

#### Web Search
**Status:** Full Support

- Real-time internet information retrieval
- Google Search grounding integration
- Built into agent's tooling capabilities
- Available for up-to-date information during tasks

#### Sandbox Modes
**Status:** Full Support

- Execute untrusted code/tools in secure, isolated container
- Checkpointing system for workspace state management
- `/restore` command to revert files to pre-tool state
- Security boundaries via trusted folders
- `.geminiignore` files to protect sensitive data

#### Google Cloud Integration
**Status:** Full Support

**Vertex AI Integration:**
- Three authentication methods:
  - Application Default Credentials (ADC) via gcloud
  - Service Account JSON key
  - Google Cloud API key
- Available without setup in Cloud Shell
- Requires GOOGLE_CLOUD_PROJECT and GOOGLE_CLOUD_LOCATION env vars

**Multi-Auth Support:**
- Google Account login (Gemini Code Assist)
- Gemini API key (unpaid - Flash only)
- Vertex AI Express Mode (no billing required)

#### Cost Tracking (/stats)
**Status:** Full Support

- `/stats` command shows:
  - Token usage statistics
  - Cached token savings
  - Session duration
- Summary presented on exit at end of session
- Community enhancements proposed for spending calculations
- Integrates with Gemini API pricing data

**Pricing Structure:**

**Free Tier:**
- Google Account login
- Unpaid API key (Flash model only)
- Vertex AI Express Mode
- 60 requests/minute, 1,000 requests/day

**Fixed Price:**
- Google AI Pro/Ultra subscriptions
- Gemini Code Assist Standard/Enterprise editions
- Predictable costs for individual developers or enterprises

**Pay-As-You-Go:**
- Flexible option for professional use
- Pay per token/call
- Most flexible for long-running tasks
- Requires mindful usage to avoid unexpected costs

**Additional Features:**

- **Headless Mode:** Automated reasoning for scripts and CI/CD pipelines
- **Token Caching:** Performance optimization for repeated context
- **Memory Management:** Persistent project facts across sessions via GEMINI.md
- **Customizable Themes:** Visual appearance control
- **Telemetry Management:** Privacy controls
- **System Prompt Override:** Customize core model instructions
- **GitHub Actions:** Automated issue triage and PR reviews
- **File Management:** Read code and apply changes directly
- **Shell Commands:** Execute builds, tests, and terminal operations

**Latest Updates:**
- Documentation last updated: January 28, 2026
- Gemini CLI version v0.23.0 validated: January 9, 2026
- Hooks enabled by default since v0.26.0+
- Extensions system actively maintained with browse functionality

**Notable Changes from Previous Research:**
1. All Gemini 2.5 models confirmed at 1M token context window
2. Gemini 3 Preview models available with 1M context
3. Gemini 2.0 Flash deprecation scheduled March 31, 2026
4. Hooks now fully supported (default enabled v0.26.0+)
5. Extensions system matured with comprehensive documentation
6. Cost tracking via /stats is production-ready
7. MCP support fully integrated into extensions
8. Agent Skills in preview for sub-agent capabilities
