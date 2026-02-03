# Context Window Research Workflow

Execute the daily context window research workflow to keep `README.md` up-to-date.

---

## Agents

```yaml
agents:
  - name: claude-code-research-agent
    persona: Dr. Sarah Chen
    experience: 12 years @ Anthropic
    domain: Claude Code & Anthropic models

  - name: codex-cli-research-agent
    persona: Marcus Thompson
    experience: 10 years @ OpenAI
    domain: Codex CLI & OpenAI models

  - name: cursor-research-agent
    persona: Elena Rodriguez
    experience: 8 years @ Anysphere
    domain: Cursor IDE & multi-model support

  - name: gemini-cli-research-agent
    persona: Dr. Raj Patel
    experience: 10 years @ DeepMind
    domain: Gemini CLI & Google models
```

---

## Steps

```yaml
steps:
  - step: 0
    name: Initialize Research Session
    description: Create timestamped research folder
    execution: sequential
    tasks:
      - action: Create folder in research/ with timestamp format YYYY-MM-DD_HH-MM-SS
        path: ${CLAUDE_PROJECT_DIR}/research/{timestamp}/
      - action: Initialize research.md in the folder with header and metadata

  - step: 1
    name: Parallel Research
    description: Launch all 4 research agents simultaneously
    execution: parallel
    tasks:
      - agent: claude-code-research-agent
        action: Research latest Claude Code models and context windows
        sources:
          - https://docs.anthropic.com/en/docs/about-claude/models
          - https://docs.anthropic.com/en/docs/claude-code
        output: Append findings to research.md under "## Claude Code Research" section

      - agent: codex-cli-research-agent
        action: Research latest Codex CLI models and context windows
        sources:
          - https://platform.openai.com/docs/models
          - https://openai.com/index/introducing-o3-and-o4-mini/
        output: Append findings to research.md under "## Codex CLI Research" section

      - agent: cursor-research-agent
        action: Research latest Cursor supported models and context windows
        sources:
          - https://cursor.com/docs/models
          - https://cursor.com/changelog
        output: Append findings to research.md under "## Cursor Research" section

      - agent: gemini-cli-research-agent
        action: Research latest Gemini CLI models and context windows
        sources:
          - https://ai.google.dev/gemini-api/docs
          - https://github.com/google-gemini/gemini-cli
        output: Append findings to research.md under "## Gemini CLI Research" section

  - step: 2
    name: Aggregate & Compare
    description: Compile results and compare with current README
    execution: sequential
    tasks:
      - action: Read all agent findings from research.md
      - action: Read current README.md and reports/context-comparison.md
      - action: Create result.md with aggregated findings
      - action: Generate diff section showing changes between current and new data
      - action: DO NOT update README directly

  - step: 3
    name: User Confirmation
    description: Present findings and request approval
    execution: sequential
    tasks:
      - action: Display summary of changes found
      - action: Show diff between current README and proposed updates
      - action: Ask user "These are my findings. Do you want to update the README?"
      - action: Wait for user confirmation before making any changes
```

---

## Research Folder Structure

```
research/
└── {YYYY-MM-DD_HH-MM-SS}/
    ├── research.md      # Individual agent findings
    └── result.md        # Aggregated results and diff
```

### research.md Format

```markdown
# Context Window Research Session

**Started:** {timestamp}
**Status:** In Progress

---

## Claude Code Research
**Agent:** Dr. Sarah Chen
**Status:** Pending/Complete

[Agent writes findings here]

---

## Codex CLI Research
**Agent:** Marcus Thompson
**Status:** Pending/Complete

[Agent writes findings here]

---

## Cursor Research
**Agent:** Elena Rodriguez
**Status:** Pending/Complete

[Agent writes findings here]

---

## Gemini CLI Research
**Agent:** Dr. Raj Patel
**Status:** Pending/Complete

[Agent writes findings here]
```

### result.md Format

```markdown
# Research Results

**Completed:** {timestamp}

## Summary

| Tool | Models Found | Changes Detected |
|------|--------------|------------------|
| Claude Code | X | Yes/No |
| Codex CLI | X | Yes/No |
| Cursor | X | Yes/No |
| Gemini CLI | X | Yes/No |

## Proposed README Updates

[New quick comparison table]

## Proposed Report Updates

[New detailed comparison data]

## Diff: Current vs New

### README.md Changes
```diff
- old line
+ new line
```

### reports/context-comparison.md Changes
```diff
- old line
+ new line
```
```

---

## Instructions

Execute this workflow by following these steps:

**Step 0**: Create the research folder with timestamp
```bash
mkdir -p ${CLAUDE_PROJECT_DIR}/research/{YYYY-MM-DD_HH-MM-SS}
```

**Step 1**: Use the Task tool to launch all 4 research agents in **parallel** (single message with 4 Task tool calls). Each agent must write their findings to the shared `research.md` file.

**Step 2**: After all agents complete, read their findings and create `result.md` with:
- Aggregated data from all agents
- Comparison with current README.md
- Clear diff showing what would change

**Step 3**: Present findings to user and ask for confirmation:
> "These are my findings. Do you want to update the README?"

**IMPORTANT**: Do NOT update README.md or reports/context-comparison.md without explicit user approval.

---

## Output Format

```yaml
output:
  header: "CONTEXT WINDOW RESEARCH WORKFLOW"
  date: YYYY-MM-DD
  research_folder: research/{timestamp}/

  phase_0_results:
    folder_created: true/false
    research_md_initialized: true/false

  phase_1_results:
    claude_code:
      models_found: X
      changes: true/false
      written_to_research_md: true/false
    codex_cli:
      models_found: X
      changes: true/false
      written_to_research_md: true/false
    cursor:
      models_found: X
      changes: true/false
      written_to_research_md: true/false
    gemini_cli:
      models_found: X
      changes: true/false
      written_to_research_md: true/false

  phase_2_results:
    result_md_created: true/false
    diff_generated: true/false
    changes_found:
      - description of change 1
      - description of change 2

  phase_3_results:
    user_prompted: true/false
    user_approved: true/false
    readme_updated: true/false
    report_updated: true/false

  status: COMPLETE/PARTIAL/FAILED/AWAITING_APPROVAL
```

---

Begin execution now:
1. First, create the timestamped research folder and initialize research.md
2. Then launch all 4 research agents in parallel using a single message with multiple Task tool calls
3. After agents complete, create result.md with findings and diff
4. Ask user for approval before updating any files
