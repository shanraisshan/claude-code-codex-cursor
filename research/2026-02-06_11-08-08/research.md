# Context Window & Features Research Session

**Started:** 2026-02-06 11:08:08
**Status:** In Progress

---

## Claude Code Research
**Agent:** Dr. Sarah Chen
**Status:** Complete

### Context Windows

**Latest Models (as of February 2026):**

| Model | Context Window | Max Output | Extended Thinking | Notes |
|-------|----------------|------------|-------------------|-------|
| **Claude Opus 4.6** | 200k / 1M (beta) | 128k | Yes (Adaptive) | Released Feb 5, 2026. First Opus with 1M context. Adaptive thinking with 4 effort levels. |
| **Claude Opus 4.5** | 200k | 64k | Yes | Legacy model, still available. 67% lower cost than predecessor. |
| **Claude Sonnet 4.5** | 200k / 1M (beta) | 64k | Yes | Recommended default, best coding model. |
| **Claude Haiku 4.5** | 200k | 64k | Yes | Fastest model, unbeatable for UI work. |

**1M Context Window Beta:**
- Available for Opus 4.6 and Sonnet 4.5
- Requires `context-1m-2025-08-07` beta header
- Available to usage tier 4 organizations and custom rate limits
- Premium pricing: 2x input, 1.5x output for requests exceeding 200k tokens
- Opus 4.6: $10 input / $37.50 output per million tokens (premium tier)
- Standard pricing: $5 input / $25 output (Opus 4.6), $3 input / $15 output (Sonnet 4.5)

**Extended Thinking Budget:**
- Opus 4.6 supports **adaptive thinking** (decides when deeper reasoning helps)
- Four effort levels: low, medium, high (default), max
- Thinking budget tokens are subset of max_tokens parameter
- Billed as output tokens and count towards rate limits

**Context Compaction:**
- Beta feature for longer-running agentic tasks
- Automatically summarizes older context when approaching thresholds
- Auto-compaction triggers at ~95% capacity (configurable via CLAUDE_AUTOCOMPACT_PCT_OVERRIDE)

**Performance:**
- Opus 4.6 scores 76% on MRCR v2 (needle-in-haystack) vs 18.5% for Sonnet 4.5
- Can process 1,500 pages of text, 30,000 lines of code, or 1+ hour of video
- 128k output enables substantial tasks without multiple requests

**Changes Detected:** YES - Major update with Opus 4.6 release, 1M context now available for Opus-class models

### Features

**Hooks System:** ✅ FULL SUPPORT
- All hook events available: PreToolUse, PostToolUse, Stop, SubagentStop, SubagentStart, SessionStart, SessionEnd, PreCompact, UserPromptSubmit, Notification, PermissionRequest, Setup, TeammateIdle, TaskCompleted
- Hooks can be defined in subagent frontmatter or settings.json
- PreToolUse hooks support conditional validation (exit code 2 blocks operations)
- PostToolUse hooks for actions after tool execution
- Subagent-scoped hooks clean up when subagent finishes

**Plugins/MCP:** ✅ FULL SUPPORT
- Plugin system for packaging slash commands, subagents, MCP servers, and hooks
- MCP (Model Context Protocol) connects Claude Code to external tools, databases, APIs
- MCP OAuth support for authentication
- Streamable HTTP support
- Plugins can be installed from marketplaces
- Plugin components: slash commands, subagents, MCP servers, hooks

**Sub-agents:** ✅ FULL SUPPORT + NEW AGENT TEAMS
- Custom subagents with specialized prompts, tool restrictions, permissions
- Built-in subagents: Explore (read-only, Haiku), Plan (research), general-purpose
- Subagent scopes: session (CLI flag), project (.claude/agents/), user (~/.claude/agents/), plugin
- Foreground (blocking) or background (concurrent) execution
- **NEW: Agent teams** for parallel autonomous task coordination (announced with Opus 4.6)
- Persistent memory system (user/project/local scopes)
- Auto-compaction support for subagents
- Resume capability to continue previous subagent work
- Subagents can preload skills via frontmatter

**Skills System:** ✅ UNIFIED WITH SLASH COMMANDS
- Slash commands merged into skills system (v2.1.3)
- Skills defined in .claude/skills/ with SKILL.md files
- YAML frontmatter + markdown content
- Backward compatible with .claude/commands/
- Auto-discovery by Claude or manual invocation
- Skill hot-reload without restart
- Skills can run in subagents or main context
- Support for directory of supporting files

**Custom Commands:** ✅ FULL SUPPORT
- Implemented via Skills system (slash commands merged into skills)
- SKILL.md files in .claude/skills/
- YAML frontmatter for configuration
- Markdown content for instructions

**IDE Integration:** ✅ FULL SUPPORT
- Native VS Code extension with 2M+ installs
- Real-time change visualization with inline diffs
- Dedicated sidebar panel
- Checkpoints to track and rewind file edits
- @-mention files with specific line ranges
- Conversation history and multi-tab support
- Beta status with active development
- Compatible with VS Code 1.85+ on Windows, macOS, Linux
- Support for VS Code-based IDEs (Cursor, Trae)

**Git Integration:** ✅ FULL SUPPORT
- Commit, PR creation, branch management
- Git diff review capabilities
- Integration with code review workflows

**Web Search:** ✅ AVAILABLE
- Built-in web search capability
- Available in US region

**Sandbox Mode:** ✅ AVAILABLE (macOS/Linux)
- Native sandboxing using OS-level primitives
- macOS: Seatbelt (same as App Store apps)
- Linux: bubblewrap (bwrap) used by Flatpak
- Filesystem isolation (read/write to cwd, blocks outside)
- Network isolation via unix domain socket proxy
- Domain whitelisting with user confirmation
- Reduces permission prompts by 84% in internal testing
- Protects against prompt injection attacks
- Cannot steal SSH keys or phone home to attackers

**Cost Tracking:** ✅ FULL SUPPORT
- /cost, /usage, /stats commands
- Token usage tracking
- Cost monitoring per session

**Memory System:** ✅ FULL SUPPORT
- CLAUDE.md project instructions (checked into codebase)
- .claude/rules/ for additional rules
- Automatic memory for subagents (user/project/local scopes)
- Persistent memory survives across conversations
- Memory files managed by subagents (Read, Write, Edit auto-enabled)

**Task Management:** ✅ FULL SUPPORT
- Task API with state persistence to ~/.claude/tasks/
- Task list view (Ctrl+T to toggle)
- Progress tracking: pending, in progress, complete
- Background task monitoring via /tasks command
- Multi-step workflow coordination

**Background Commands:** ✅ FULL SUPPORT
- Ctrl+B to move commands to background (Ctrl+B twice for tmux users)
- Dev servers, build processes, test suites run independently
- BashOutput tool to check on background processes
- Background tasks don't block main coding session
- Disable via CLAUDE_CODE_DISABLE_BACKGROUND_TASKS=1

**PDF Reading:** ✅ FULL SUPPORT
- Read tool supports PDF files (.pdf)
- Page range specification for large PDFs (required for >10 pages)
- Maximum 20 pages per request

**LSP Tool:** ✅ AVAILABLE
- Code intelligence via Language Server Protocol
- Integration with IDE language servers

**Keybindings Customization:** ✅ AVAILABLE
- Custom keybinding configuration
- Ctrl+B for background commands
- Ctrl+T for task list toggle

**Image Support:** ✅ FULL SUPPORT
- All Claude 4 models support text and image input
- Multimodal capabilities across Opus 4.6, Sonnet 4.5, Haiku 4.5
- Vision processing with specialized fees

**Multi-file Editing:** ✅ FULL SUPPORT
- Concurrent file editing
- Inline diffs and change tracking
- Checkpoint system for reverting changes

**Auto-commit:** ⚠️ PARTIAL (via hooks/workflows)
- Can be implemented via PostToolUse hooks
- Not automatic by default but configurable

**Custom System Prompts:** ✅ FULL SUPPORT
- Subagent system prompts via markdown files
- CLAUDE.md for project-level instructions
- .claude/rules/ for additional customization

**Changes Detected:** YES - Major feature additions including agent teams, unified skills system, enhanced sandbox mode, and improved IDE integration

**Sources:**
- [Anthropic Claude Opus 4.6 Release](https://www.anthropic.com/news/claude-opus-4-6)
- [Claude API Models Overview](https://platform.claude.com/docs/en/about-claude/models/overview)
- [Claude Code Sub-agents Documentation](https://code.claude.com/docs/en/sub-agents)
- [Claude Code VS Code Extension](https://code.claude.com/docs/en/vs-code)
- [Claude Code Sandboxing Documentation](https://code.claude.com/docs/en/sandboxing)
- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills)
- [Anthropic Engineering: Claude Code Sandboxing](https://www.anthropic.com/engineering/claude-code-sandboxing)
- [TechCrunch: Anthropic Opus 4.6 with Agent Teams](https://techcrunch.com/2026/02/05/anthropic-releases-opus-4-6-with-new-agent-teams/)
- [VentureBeat: Claude Opus 4.6 1M Token Context](https://venturebeat.com/technology/anthropics-claude-opus-4-6-brings-1m-token-context-and-agent-teams-to-take)

---

## Codex CLI Research
**Agent:** Marcus Thompson
**Status:** Complete

### Context Windows

**Latest Models (February 2026):**

1. **GPT-5.3-Codex** (NEW - Released Feb 5, 2026)
   - Context Window: 400,000 tokens
   - Output Limit: 128,000 tokens
   - Features: "Perfect Recall" attention mechanism preventing information loss in long prompts
   - Performance: 25% faster than GPT-5.2-Codex, combines Codex + GPT-5 training stacks
   - Notes: Most capable agentic coding model, unifies frontier code performance with professional reasoning
   - Status: Available in Codex CLI for ChatGPT users

2. **GPT-5.2-Codex** (Released Jan 14, 2026)
   - Context Window: 400,000 tokens (400k)
   - Output Limit: 128,000 tokens (128k)
   - Features: Native compaction, reliable tool calling, improved long-context understanding
   - Performance: SWE-Bench Pro: 56.4%, Terminal-Bench 2.0: 64.0%
   - Reasoning Efforts: Supports low, medium, high, and xhigh settings
   - Pricing: $1.75/M input tokens, $14.00/M output tokens
   - Status: Available in all Codex surfaces for paid ChatGPT users

3. **GPT-5.1-Codex-Max**
   - Context Window: Multi-window (millions of tokens)
   - Output Limit: N/A (uses compaction)
   - Features: First model natively trained for compaction, works across multiple context windows
   - Performance: Can work independently for 24+ hours on long-horizon tasks
   - Compaction: Automatically prunes history while preserving important context
   - Status: Available in Codex CLI, IDE extension, cloud, and code review

4. **GPT-5-Codex**
   - Context Window: 200,000 tokens (200k)
   - Output Limit: N/A
   - Status: Standard model, available when signing in with ChatGPT account

**Deprecated Models:**
- codex-mini-latest: Removed January 16, 2026 (previously ~200k context)

**Key Changes:**
- GPT-5.3-Codex is now the recommended default model
- Context windows increased from 200k to 400k for latest models
- Multi-window compaction technology enables millions of tokens for GPT-5.1-Codex-Max
- All models now support automatic context compaction as sessions approach limits

### Features

**Hooks Support: ⚠️ Limited**
- No native hooks system documented in official February 2026 documentation
- Feature request exists for /ai-git-commit-push slash command (Issue #3481)
- Git auto-commit can be done manually but not through automated hooks
- Community workarounds available but not officially supported

**MCP/Plugins: ✅ Full Support**
- Full Model Context Protocol (MCP) support
- Configure via ~/.codex/config.toml or use 'codex mcp' CLI commands
- Supports STDIO and streaming HTTP servers
- Session-scoped "Allow and remember" for MCP tool approvals (NEW - Jan 2026)
- Common servers: Context7, Figma, Playwright, Chrome DevTools, Sentry

**Sub-agents/Agent Skills: ✅ Full Support**
- Agent Skills extend Codex with task-specific capabilities
- Reads from ~/.agents/skills and repository .agents/skills directories
- Personal skill loading from ~/.agents/skills added Feb 2026
- App-server APIs/events to list and download public remote skills
- Shell executions receive CODEX_THREAD_ID for session detection
- Compatible with Claude-style sub-agents via MCP server approach
- Live skill update detection without restart (NEW - Feb 2026)

**Slash Commands: ✅ Full Support**
- Built-in commands: /review, /fork, and more
- Searchable slash popup interface
- Can create custom slash commands for team-specific tasks

**Custom Commands: ✅ Full Support**
- Custom prompts via Markdown files
- Stored in ~/.codex directory
- Support metadata and placeholders ($1-$9 positional, KEY=value named)
- Invokable as slash commands in CLI and IDE
- Not shared through repository (local only)

**IDE Integration: ✅ Full Support**
- VSCode: Official Codex IDE extension
- JetBrains: Native integration (IntelliJ, PyCharm, WebStorm, Rider) as of Jan 2026
- Also available: Visual Studio, Xcode, Eclipse (as of Jan 26, 2026)
- Works with VSCode forks: Cursor, Windsurf
- Authentication via JetBrains AI, ChatGPT, or BYOK (Bring Your Own Key)

**Git Integration: ✅ Full Support**
- Deep Git awareness and change tracking
- Can automatically commit with meaningful commit messages
- Git-aware context understanding
- Safety mechanisms for version-controlled environments

**Web Search: ✅ Full Support**
- Enabled for local tasks in CLI and IDE extension (Jan 28, 2026)
- Three modes: cached (default), live, or disabled
- Configurable web search options

**Sandbox/Approval Modes: ✅ Full Support**
- Multiple approval modes: auto (default), read-only, workspace-write, danger-full-access
- Switch modes with /approvals command
- Disable with --ask-for-approval never or -a never
- Session-scoped "Allow and remember" for repeated tool calls (NEW - Jan 2026)
- Two security layers: sandbox mode (technical capabilities) + approval policy (when to ask)

**Cost Tracking: ❌ Not Available**
- No native cost tracking feature documented in official docs
- Pricing information available but no session/usage tracking built-in

**Memory/Persistence: ✅ Full Support**
- Stores transcripts locally
- Resume earlier threads with 'resume' subcommand
- Pick up where you left off without repeating context
- Thread/session persistence across restarts

**Image Support: ✅ Full Support**
- Strong vision performance in GPT-5.2-Codex and GPT-5.3-Codex
- Can interpret screenshots, technical diagrams, charts, UI surfaces
- Improved accuracy for visual content in coding sessions

**Multi-file Editing: ✅ Full Support**
- Can read repository, make edits across multiple files
- Full-screen terminal UI for conversational workflow
- 128k output limit enables large, multi-file software projects in single interaction

**Auto-commit: ⚠️ Partial Support**
- Can commit changes with meaningful messages
- No automated hook-based auto-commit after every file change
- Requires manual invocation or custom scripting

**Custom System Prompts: ✅ Full Support**
- Via custom prompts system (Markdown files)
- Stored in ~/.codex directory
- Invokable as slash commands
- Support for metadata and variable placeholders

**Additional Features:**
- Open source, built in Rust for speed and efficiency
- Runs locally from terminal
- Supported on macOS, Windows, Linux
- Network configuration UI streamlined in v0.87.0 (Jan 2026)

**Sources:**
- [Introducing GPT-5.3-Codex](https://openai.com/index/introducing-gpt-5-3-codex/)
- [Codex Models Documentation](https://developers.openai.com/codex/models/)
- [Codex CLI Features](https://developers.openai.com/codex/cli/features/)
- [Model Context Protocol](https://developers.openai.com/codex/mcp/)
- [Agent Skills](https://developers.openai.com/codex/skills/)
- [Slash Commands Documentation](https://developers.openai.com/codex/cli/slash-commands/)
- [Custom Prompts](https://developers.openai.com/codex/custom-prompts/)
- [Codex Security](https://developers.openai.com/codex/security/)
- [JetBrains Integration Announcement](https://blog.jetbrains.com/ai/2026/01/codex-in-jetbrains-ides/)
- [GPT-5.2-Codex in IDEs Changelog](https://github.blog/changelog/2026-01-26-gpt-5-2-codex-is-now-available-in-visual-studio-jetbrains-ides-xcode-and-eclipse/)

---

## Cursor Research
**Agent:** Elena Rodriguez
**Status:** Complete
**Last Updated:** 2026-02-06

### Context Windows

**Latest Stable Release:** v2.4 (January 22, 2026)

#### Anthropic Models

| Model | Normal Context | Max Context | Output | Notes |
|-------|---------------|-------------|---------|-------|
| Claude 4.6 Opus | 200k | 1M | 64k | NEW - Added in 2026 |
| Claude 4.5 Sonnet | 200k | 1M | 64k | Premium, Agent/Thinking modes |
| Claude 4.5 Opus | 200k | 200k | 64k | Deep reasoning |
| Claude 4.5 Haiku | 200k | - | 64k | Fast and efficient |
| Claude 4 Sonnet 1M | 1M | 1M | 64k | Extended context only |
| Claude 4 Sonnet | 200k | - | 64k | Standard |
| Claude 4 Opus | 200k | - | 64k | Available in Max mode |
| Claude 3.7 Sonnet | 200k | - | 64k | Legacy |
| Claude 3.5 Sonnet | 200k | - | 64k | Legacy but still popular |
| Claude 3.5 Haiku | 60k | - | 8k | Legacy |

#### OpenAI Models

| Model | Normal Context | Max Context | Output | Notes |
|-------|---------------|-------------|---------|-------|
| GPT-5.2 (all variants) | 272k | - | - | Latest generation |
| GPT-5.2-Codex | 272k | - | - | Code-optimized |
| GPT-5.1 Codex Max | 200k | 400k | 128k | Improved tool calls |
| GPT-5.1 High | 200k | 400k | 128k | Frontier coding |
| GPT-5 Fast | 272k | - | - | Speed-optimized |
| GPT-5 Mini | 200k | - | 128k | Lightweight |
| GPT-5 Nano | 200k | - | 128k | Ultra-fast |
| GPT 4.1 | 200k | 1M | 8k | Legacy |
| GPT-4o | 128k | - | 16k | General purpose |
| GPT-4o mini | 60k | - | 8k | Free tier (500/day) |
| o3 | 200k | - | 8k | Reasoning |
| o4-mini | 200k | - | 8k | Normal/Max modes |
| o3-mini | 200k | - | 8k | Agent/Thinking |
| o1 | 200k | - | 8k | Thinking mode |
| o1 Mini | 128k | - | 8k | Thinking mode |

#### Google Models

| Model | Normal Context | Max Context | Output | Notes |
|-------|---------------|-------------|---------|-------|
| Gemini 3 Pro Preview | 200k | 1M | 8k | Top SWE-bench performer (76-78%) |
| Gemini 3 Pro Image Preview | 200k | 1M | 8k | Multimodal with image gen |
| Gemini 3 Flash | 200k | 1M | 8k | Fast inference |
| Gemini 2.5 Pro | 200k | 1M | 8k | Design/debugging |
| Gemini 2.5 Flash | 200k | 1M | 8k | Speed-optimized |

#### xAI Models

| Model | Normal Context | Max Context | Output | Notes |
|-------|---------------|-------------|---------|-------|
| Grok 4 | 200k | 2M | - | Real-time web search |
| Grok Code | 256k | - | - | Code-optimized |
| Grok Code Fast | 200k | - | - | Speed-optimized |

#### DeepSeek Models

| Model | Context Window | Output | Notes |
|-------|---------------|---------|-------|
| DeepSeek V3 | 64k-128k | - | Hosted on US servers, free in Pro plan |
| DeepSeek V3.1 | 128k | - | NEW - Upgraded context from V3's 64k |
| DeepSeek R1 | 200k | - | Free within Pro plan |

#### Cursor Native Models

| Model | Context Window | Output | Notes |
|-------|---------------|---------|-------|
| Composer 1 | 200k | - | 4x faster, <30s response, proprietary |

**Key Changes:**
- NEW: Claude 4.6 Opus added with 1M max context
- NEW: DeepSeek V3.1 with 128k context
- NEW: Gemini 3 Pro Image Preview with image generation
- NEW: Grok Code model (256k)

### Features

**Hooks:** ✅ Enhanced (10-40x performance improvement)
**Plugins/MCP:** ✅ Full Support (one-click OAuth, CLI management)
**Sub-agents:** ✅ Enhanced (parallel execution, Skills system, Cloud agents)
**Slash Commands:** ✅ Comprehensive (/models, /plan, /ask, /rules, /mcp)
**Custom Commands:** ✅ (.cursor/commands/*.md)
**IDE Integration:** ✅ Native (VS Code-based)
**Git Integration:** ✅ Advanced (AI commits, GitButler, merge conflict resolution)
**Web Search:** ✅ (@Web, Grok 4 real-time)
**Image Support:** ⚠️ (generation added Jan 2026, full vision coming)
**Memory/Persistence:** ⚠️ (limited built-in, robust via MCP)
**Multi-file Editing:** ✅ Full Support
**Auto-commit:** ✅ (via hooks/GitButler)
**Custom System Prompts:** ✅ (.cursor/rules/ system)
**Cost Tracking:** ⚠️ (Enterprise/third-party only)
**Sandbox Mode:** ⚠️ (macOS/Linux, workflow friction)
**Codebase Indexing:** ✅ (@Codebase semantic search)

**Sources:**
- [Cursor Models Documentation](https://cursor.com/docs/models)
- [Cursor Changelog](https://cursor.com/changelog)
- [Cursor Rules Documentation](https://cursor.com/docs/context/rules)

---

## Gemini CLI Research
**Agent:** Dr. Raj Patel
**Status:** Complete
**Last Updated:** 2026-02-06

### Context Windows

**Latest Stable Release:** v0.27.0 (February 3, 2026)

#### Current Production Models (Stable)

| Model | Context Window | Max Output | Status | Notes |
|-------|---------------|------------|--------|-------|
| Gemini 2.5 Pro | 1,048,576 (1M) | 65,536 (65k) | Stable | High-capability reasoning and coding |
| Gemini 2.5 Flash | 1,048,576 (1M) | 65,536 (65k) | Stable | Balanced speed/intelligence |
| Gemini 2.5 Flash-Lite | 1,048,576 (1M) | 65,536 (65k) | Stable | Lightweight variant |
| Gemini 2.5 Flash Image | 65,536 (65k) | 32,768 (32k) | Stable | Image generation specialist |

#### Preview Models (Gemini 3 Series)

| Model | Context Window | Max Output | Status | Notes |
|-------|---------------|------------|--------|-------|
| Gemini 3 Pro Preview | 1,048,576 (1M) | 65,536 (65k) | Preview | Flagship model - launched Feb 4, 2026 |
| Gemini 3 Flash Preview | 1,048,576 (1M) | 65,536 (65k) | Preview | Pro-grade reasoning at Flash speed - Feb 4, 2026 |
| Gemini 3 Pro Image Preview | 65,536 (65k) | 32,768 (32k) | Preview | Image generation |

#### Specialized Preview Models

| Model | Context Window | Max Output | Status | Notes |
|-------|---------------|------------|--------|-------|
| Gemini 2.5 Flash Live | 131,072 (131k) | 8,192 (8k) | Preview | Real-time audio streaming |
| Gemini 2.5 Flash TTS | 8,192 (8k) | 16,384 (16k) | Preview | Text-to-speech |
| Gemini 2.5 Flash Preview | 1,048,576 (1M) | 65,536 (65k) | Preview | Experimental features |

#### Deprecated Models (End of Life: March 31, 2026)

| Model | Context Window | Max Output | Status | EOL Date |
|-------|---------------|------------|--------|----------|
| Gemini 2.0 Flash | 1,048,576 (1M) | 8,192 (8k) | Deprecated | March 31, 2026 |
| Gemini 2.0 Flash-Lite | 1,048,576 (1M) | 8,192 (8k) | Deprecated | March 31, 2026 |

**Key Updates:**
- Gemini 3 Flash launched February 4, 2026 as default model in Gemini app
- Gemini 3 series delivers PhD-level reasoning (90.4% GPQA Diamond)
- All Gemini 3 models maintain 1M token context window
- Gemini 2.0 models fully deprecated March 31, 2026
- Context windows remain industry-leading at 1M tokens for primary models

### Features

#### Core Agent Capabilities
- **Hooks System:** ✅ Full lifecycle event hooks (BeforeAgent, AfterAgent, BeforeTool, AfterTool, BeforeModel, BeforeToolSelection) - v0.26.0+
- **MCP Support:** ✅ Model Context Protocol for custom integrations via settings.json
- **Agent Skills:** ✅ Stable feature (v0.27.0) - portable skill format with SKILL.md schema, progressive disclosure to save context
- **Sub-agents:** ✅ Supported via AgentRegistry with JSON schema validation
- **Event-Driven Architecture:** ✅ v0.27.0 introduces event-driven scheduler for tool execution

#### Commands & Configuration
- **Slash Commands:** ✅ Built-in commands (/help, /chat, /bug, /stats, /memory, /rewind)
- **Custom Commands:** ✅ TOML-based configuration in .gemini/commands/ (user-scoped and project-scoped)
- **Command Namespacing:** ✅ Subdirectories create namespaced commands (e.g., /git:commit)
- **Argument Handling:** ✅ {{args}} placeholder and shell execution !{...} support
- **/rewind Command:** ✅ New in v0.27.0 - navigate backward through session history

#### IDE & Development Integration
- **IDE Integration:** ✅ VS Code companion extension
- **Git Integration:** ✅ AI-powered commit message generation, pre-commit hook support, GitHub Actions integration
- **Auto-commit:** ✅ generate-commit-message tool with Conventional Commits compliance
- **GitHub Actions:** ✅ Official google-github-actions/run-gemini-cli (beta, launched Feb 2026)

#### Search & Knowledge
- **Web Search:** ✅ Google Search grounding for real-time information
- **Multimodal Support:** ✅ Text, code, images, PDFs, sketches - full multimodal context
- **Image Support:** ✅ Image pasting on Linux (Wayland/X11) - v0.27.0, image generation models available

#### Memory & Context Management
- **Memory/Persistence:** ✅ Hierarchical GEMINI.md system (global ~/.gemini/GEMINI.md + project-level)
- **Memory Commands:** ✅ /memory show, /memory refresh, /memory add <text>
- **Context Files:** ✅ Modular context with @file.md imports
- **Token Caching:** ✅ Automatic caching to optimize token usage
- **Conversation Checkpointing:** ✅ Save and resume complex sessions

#### Cost & Usage Tracking
- **Cost Tracking:** ✅ /stats command shows token usage, cached tokens, session metrics
- **Usage Display:** ✅ Stats shown on session exit
- **Token Optimization:** ✅ Caching reduces costs for repeated context

#### Security & Sandboxing
- **Sandbox Mode:** ✅ Isolates operations, limits file system access to project directory
- **Trusted Folders:** ✅ Security controls via ~/.gemini/trustedFolders.json
- **Safe Mode:** ✅ Untrusted folders run with MCP disabled, no custom commands
- **Docker Sandboxing:** ✅ Optional custom sandbox environments

#### Developer Experience
- **Multi-file Editing:** ✅ Full file system operations through built-in tools
- **Shell Commands:** ✅ Execute shell commands directly in CLI
- **JSON Output:** ✅ JSON and stream-JSON formats for scripting/automation
- **Non-Interactive Mode:** ✅ Designed for CI/CD and automated workflows
- **Extensions Ecosystem:** ✅ gemini-cli-extensions organization on GitHub
- **Custom System Prompts:** ✅ Via GEMINI.md context files

#### Recent v0.27.0 Highlights (Feb 3, 2026)
- Event-driven scheduler (200+ commits)
- Agent Skills promoted to stable
- Sub-agents with JSON schema validation
- Queued tool confirmations
- Expandable/collapsible text blocks
- Improved Settings UI
- Better shell output formatting
- Disk-full error handling during chat recording

**References:**
- [Gemini CLI GitHub](https://github.com/google-gemini/gemini-cli)
- [Gemini CLI Documentation](https://geminicli.com/docs/)
- [Google AI Dev Docs - Models](https://ai.google.dev/gemini-api/docs/models)
- [Gemini CLI Changelog](https://geminicli.com/docs/changelogs/latest/)
- [Gemini CLI Hooks](https://geminicli.com/docs/hooks/)
- [Agent Skills Documentation](https://geminicli.com/docs/cli/skills/)
- [Custom Commands Guide](https://geminicli.com/docs/cli/custom-commands/)
- [GEMINI.md Context Files](https://geminicli.com/docs/cli/gemini-md/)
- [Sandboxing Documentation](https://geminicli.com/docs/cli/sandbox/)
- [Trusted Folders Guide](https://geminicli.com/docs/cli/trusted-folders/)
- [Gemini 3 Flash Launch](https://blog.google/products-and-platforms/products/gemini/gemini-3-flash/)
- [Build with Gemini 3 Flash](https://blog.google/technology/developers/build-with-gemini-3-flash/)

**Feature Status Summary:**
All major features fully supported. Gemini CLI maintains comprehensive agent capabilities with full hooks system, MCP integration, stable Agent Skills, sub-agents, TOML custom commands, Git/GitHub Actions integration, web search, sandbox security, cost tracking via /stats, hierarchical memory system, and multimodal support. Version 0.27.0 solidifies position as feature-rich AI coding assistant.
