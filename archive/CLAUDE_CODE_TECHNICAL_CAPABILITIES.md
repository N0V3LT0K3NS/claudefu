# Claude Code Technical Capabilities Reference

**Purpose:** A practical technical reference for Claude Code instances to understand their extensibility mechanisms, configuration patterns, and operational capabilities.

**Scope:** MCPs, SubAgents, Skills, Hooks, Slash Commands, SDK, and configuration patterns.

---

## Quick Reference Matrix

| Component | Purpose | Trigger | Location | Token Cost |
|-----------|---------|---------|----------|------------|
| **MCP** | External tool integration | Tool call | `.mcp.json`, `settings.json` | ~100-500/server |
| **SubAgents** | Parallel/isolated workers | Task tool | `.claude/agents/*.md` | Own context window |
| **Skills** | Knowledge packages | Auto (context) | `.claude/skills/*/SKILL.md` | Progressive (~100 → ~5k) |
| **Hooks** | Event handlers | Auto (events) | `settings.json` | Minimal |
| **Slash Commands** | Prompt templates | Explicit `/cmd` | `.claude/commands/*.md` | On invocation |
| **CLAUDE.md** | Persistent instructions | Always loaded | `./CLAUDE.md`, `~/.claude/CLAUDE.md` | Varies |

---

## 1. MCP (Model Context Protocol)

### What It Is
A standardized protocol connecting Claude to external tools and data sources. Think "USB for AI."

### Architecture
```
Claude → MCP Client → MCP Server → External Service (API, DB, Browser, etc.)
```

### Configuration Locations
1. **Project-level:** `.mcp.json` at project root
2. **Global:** `~/.claude/settings.json`

### Configuration Format (`.mcp.json`)
```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["@package/mcp-server"],
      "env": {
        "API_KEY": "..."
      }
    }
  }
}
```

### Server Types

| Type | Protocol | Auth Pattern | Example |
|------|----------|--------------|---------|
| **stdio** | Local child process | Env variables | Most npm MCPs |
| **SSE** | Server-Sent Events | OAuth | Slack MCP |
| **HTTP** | REST API | Token/header | Stripe MCP |

### When to Use MCP
- External API integrations (Slack, GitHub, databases)
- Real-time data (stock prices, weather)
- Browser automation
- Authenticated services

### When NOT to Use MCP
- Teaching Claude methodology (use Skills)
- One-time prompts (use Slash Commands)
- Workflow orchestration (use SubAgents)

### Available MCP Endpoints

| Service | URL | Type |
|---------|-----|------|
| Stripe | https://mcp.stripe.com | HTTP |
| GitHub | https://api.githubcopilot.com/mcp/ | HTTP |
| Slack | https://mcp.slack.com/sse | SSE |
| Supabase | https://mcp.supabase.com/mcp | URL |
| Linear | https://mcp.linear.app/mcp | URL |
| GitLab | https://gitlab.com/api/v4/mcp | URL |

### Official Documentation
- https://docs.anthropic.com/en/docs/claude-code/mcp
- https://modelcontextprotocol.io/

---

## 2. SubAgents

### What They Are
Separate Claude instances spawned via the **Task tool** to handle subtasks with **isolated context**.

### Architecture
```
Main Agent (Orchestrator)
    │
    ├──[Task]──→ SubAgent A (research)     ──→ Returns findings
    ├──[Task]──→ SubAgent B (analysis)     ──→ Returns analysis
    └──[Task]──→ SubAgent C (synthesis)    ──→ Returns summary
```

### Configuration Location
`~/.claude/agents/*.md` or `.claude/agents/*.md`

### Agent Definition Format
```yaml
---
name: agent-name
description: |
  When to use this agent with examples.
  <example>
  Context: ...
  user: "..."
  assistant: "..."
  <commentary>Why this agent is appropriate</commentary>
  </example>
tools:
  - WebSearch
  - WebFetch
  - Read
  - Write
model: opus  # or sonnet, haiku
---

You are [role description]...

Your responsibilities:
1. ...
2. ...

[Detailed methodology and instructions]
```

### Key Parameters

| Parameter | Description | Values |
|-----------|-------------|--------|
| `name` | Unique identifier | lowercase-hyphenated |
| `description` | Triggering conditions with examples | String with `<example>` blocks |
| `tools` | Allowed tools for this agent | Array of tool names |
| `model` | Model to use | `opus`, `sonnet`, `haiku` |

### Invoking SubAgents
Claude invokes via the **Task tool** with:
```
subagent_type: "agent-name"
prompt: "What the agent should do"
```

### When to Use SubAgents
- Parallel research (multiple topics simultaneously)
- Specialized roles (reviewer, analyst, writer)
- Context isolation (prevent main context pollution)
- Long-running tasks
- Different model requirements per task

### When NOT to Use SubAgents
- Simple, quick tasks
- When shared state is needed
- Sequential dependencies (A must complete before B starts)

### Architecture Patterns

| Pattern | Description | Challenge |
|---------|-------------|-----------|
| **Solo** | One agent, complete workflow | State management as workflow lengthens |
| **Parallel** | Multiple agents, same problem | Coordination, conflict resolution |
| **Collaborative** | Sequential handoff (A→B→C) | Handoffs are where things break |

### Official Documentation
- https://docs.anthropic.com/en/docs/claude-code/sub-agents

---

## 3. Skills

### What They Are
Modular capability packages - folders containing instructions, scripts, and resources that Claude loads **dynamically when relevant**.

### Architecture
```
skill-name/
├── SKILL.md              # Main instructions (Level 2)
│   └── frontmatter       # name, description (Level 1 - always loaded)
├── ADVANCED.md           # Additional docs (Level 3)
├── scripts/
│   └── validate.py       # Executable code (Level 3)
└── templates/
    └── report.md         # Resources (Level 3)
```

### Configuration Location
`~/.claude/skills/*/SKILL.md` or `.claude/skills/*/SKILL.md`

### Progressive Disclosure (Token Efficiency)

| Level | What Loads | When | Token Cost |
|-------|------------|------|------------|
| 1 | Metadata (name, description) | Always at startup | ~100 tokens |
| 2 | SKILL.md body | When skill triggered | ~5k tokens |
| 3 | Scripts, resources, extra docs | As needed | Unlimited |

### SKILL.md Format
```yaml
---
name: skill-name
description: |
  What this skill does and when it triggers.
triggers:
  - "keyword one"
  - "keyword two"
tools:
  - Read
  - Write
  - Task
  - Bash
model: opus
context: fork  # Optional: run in isolated context
agent: agent-name  # Optional: specify agent type
hooks:
  PreToolUse:
    - matcher: "WebFetch"
      command: "./hooks/validate_url.py"
---

# Skill Title

## Overview
[What this skill does]

## Workflow
### Step 1: ...
### Step 2: ...

## Output Format
[Expected outputs]
```

### Key Frontmatter Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `name` | Unique identifier | `deep-research` |
| `description` | When to activate | Detailed text |
| `triggers` | Keywords that auto-activate | Array of strings |
| `tools` | Tools this skill uses | Array of tool names |
| `model` | Preferred model | `opus`, `sonnet` |
| `context` | `fork` for isolated context | String |
| `agent` | Specify agent type | Agent name |
| `hooks` | Skill-specific hooks | Hook configuration |

### When to Use Skills
- Complex multi-step workflows
- Knowledge spanning multiple files
- Capabilities needing executable scripts
- Team standards that auto-apply
- Domain expertise packages

### When NOT to Use Skills
- Simple one-line prompts (use Slash Commands)
- External API calls (use MCP)
- One-time tasks

### Key Insight
> "Skills are potentially more significant than MCP... LLMs already excel at invoking CLI tools. Skills leverage this capability more elegantly." — Simon Willison

### Official Documentation
- https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
- https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills

---

## 4. Hooks

### What They Are
Automated scripts that run at specific points in Claude's workflow - intercept, validate, modify, or log actions.

### Configuration Location
`~/.claude/settings.json` or `.claude/settings.json`

### Hook Events

| Event | When Fires | Use Cases |
|-------|------------|-----------|
| `PreToolUse` | Before tool executes | Validate inputs, auto-approve, block |
| `PostToolUse` | After tool succeeds | Log results, validate outputs |
| `UserPromptSubmit` | User sends prompt | Add context, validate input |
| `Stop` | Agent finishes | Decide if should continue |
| `SubagentStop` | Subagent finishes | Evaluate completion |
| `SessionStart` | Session begins | Load context, setup |
| `SessionEnd` | Session ends | Cleanup, logging |
| `Notification` | Status updates | Route alerts |

### Configuration Format (`settings.json`)
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [{
          "type": "command",
          "command": "./hooks/validate_bash.py",
          "once": true
        }]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [{
          "type": "command",
          "command": "bun run format || true"
        }]
      }
    ]
  }
}
```

### Hook Types

| Type | Description | Example |
|------|-------------|---------|
| `command` | Run bash command/script | `"./hooks/validate.py"` |
| `prompt` | Send to LLM for decision | Prompt text |

### Hook I/O (JSON via stdin/stdout)

**Input to hook:**
```json
{
  "tool": "Bash",
  "input": { "command": "rm -rf /" }
}
```

**Output from hook:**
```json
{
  "decision": "block",
  "reason": "Dangerous command detected"
}
```

### Decision Values

| Decision | Effect |
|----------|--------|
| `proceed` | Continue with tool execution |
| `block` | Stop execution, return reason |
| `ask` | Prompt user for decision |
| (with `updatedInput`) | Modify input before execution |

### Key Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `matcher` | Regex for tool matching | `"Write\|Edit"` |
| `once` | Run only once per session | `true` |
| `command` | Script to execute | Path to script |

### When to Use Hooks
- Security (block dangerous commands)
- Logging/audit trails
- Auto-approval (skip permission prompts)
- Context injection
- Output validation
- Auto-formatting

### When NOT to Use Hooks
- Business logic (use Skills or SubAgents)
- User interaction (use Slash Commands)
- External APIs (use MCP)

### Example: Auto-Format on Edit (Boris Cherny)
```json
{
  "PostToolUse": [{
    "matcher": "Write|Edit",
    "hooks": [{
      "type": "command",
      "command": "bun run format || true"
    }]
  }]
}
```

### Official Documentation
- https://docs.anthropic.com/en/docs/claude-code/hooks
- https://docs.anthropic.com/en/docs/claude-code/hooks-guide

---

## 5. Slash Commands

### What They Are
Simple prompt templates stored as Markdown files, triggered explicitly with `/command`.

### Configuration Location
`.claude/commands/*.md` or `~/.claude/commands/*.md`

### File Structure
```
.claude/commands/
├── research.md        → /research <topic>
├── quick.md           → /quick <question>
├── commit.md          → /commit
└── deep/
    └── analyze.md     → /deep:analyze
```

### Command Format
```yaml
---
description: Research a topic thoroughly
allowed-tools: WebSearch, WebFetch, Task
argument-hint: <topic>
model: claude-sonnet-4-20250514
---

## Research Task

Research the following topic: $ARGUMENTS

## Current Context
- Time: !`date`
- Previous research: @data/last_research.md

## Guidelines
1. Search multiple sources
2. Verify facts
3. Cite sources
```

### Special Syntax

| Syntax | Description | Example |
|--------|-------------|---------|
| `$ARGUMENTS` | All arguments as string | `/research AI safety` → "AI safety" |
| `$1`, `$2`, etc. | Positional arguments | First arg, second arg |
| `` !`command` `` | Inline bash execution | `` !`date` `` → current date |
| `@file.md` | Include file contents | `@data/context.md` |

### Frontmatter Parameters

| Parameter | Description |
|-----------|-------------|
| `description` | Shows in command help |
| `allowed-tools` | Restrict available tools |
| `argument-hint` | Usage hint for arguments |
| `model` | Override model selection |

### When to Use Slash Commands
- Frequently repeated prompts
- Explicit user triggers
- Simple, single-file templates
- Quick shortcuts

### When NOT to Use Slash Commands
- Complex multi-step workflows (use Skills)
- Auto-triggered behavior (use Skills)
- External integrations (use MCP)

### Official Documentation
- https://docs.anthropic.com/en/docs/claude-code/slash-commands

---

## 6. CLAUDE.md Files

### What They Are
Persistent instruction files that load into context at session start.

### Loading Order (Hierarchy)
1. `~/.claude/CLAUDE.md` - Global user instructions
2. `./CLAUDE.md` - Project-level instructions
3. `./subdir/CLAUDE.md` - Directory-specific (loaded when accessing that directory)

### Best Practices
```markdown
# CLAUDE.md - Project Rules

## Code Style
- Use TypeScript strict mode
- Prefer composition over inheritance
- All functions need JSDoc comments

## Build Commands
- `npm run build` - Build project
- `npm run test` - Run tests
- `npm run lint` - Lint code

## Known Issues
- Don't use `Array.from()` with Maps - use spread instead
- Always check for null before accessing `.data` from API responses

## Learned Rules (append-only)
- 2026-01-10: Don't use `any` type (@claude from PR #234)
- 2026-01-08: Always validate user input before database queries
```

### Key Insight: Compounding Engineering
- Team shares single CLAUDE.md (git-tracked)
- "Anytime we see Claude do something incorrectly, add it to CLAUDE.md"
- Mistakes evaporate, lessons accumulate
- Tag @claude on PRs to add rules

### Official Documentation
- https://docs.anthropic.com/en/docs/claude-code/memory

---

## 7. SDK (Programmatic Access)

### What It Is
Programmatic control over Claude Code capabilities for building custom agents and integrations.

### Installation
```bash
# Python
pip install claude-agent-sdk

# TypeScript
npm install @anthropic-ai/claude-agent-sdk
```

### Basic Usage (Python)
```python
from claude_agent_sdk import (
    ClaudeSDKClient,
    ClaudeAgentOptions,
    AssistantMessage,
    ResultMessage,
    TextBlock,
    ToolUseBlock,
)

async def research(query: str):
    options = ClaudeAgentOptions(
        model="claude-sonnet-4-20250514",
        system_prompt="You are a research assistant.",
        allowed_tools=["WebSearch", "WebFetch", "Task"],
        permission_mode="acceptEdits",
        max_turns=30,
    )

    async with ClaudeSDKClient(options=options) as client:
        await client.query(query)

        async for message in client.receive_response():
            if isinstance(message, AssistantMessage):
                for block in message.content:
                    if isinstance(block, TextBlock):
                        print(block.text)
                    elif isinstance(block, ToolUseBlock):
                        print(f"Tool: {block.name}")

            elif isinstance(message, ResultMessage):
                print(f"Cost: ${message.total_cost_usd}")
```

### Key Options

| Option | Description |
|--------|-------------|
| `model` | Model to use (sonnet, opus, haiku) |
| `system_prompt` | System instructions |
| `allowed_tools` | List of permitted tools |
| `permission_mode` | `auto`, `acceptEdits`, or `ask` |
| `max_turns` | Maximum agent turns |
| `cwd` | Working directory |
| `resume` | Session ID to continue |

### Official Documentation
- https://docs.anthropic.com/en/docs/claude-code/sdk
- https://github.com/anthropics/claude-code-sdk-python

---

## 8. Permissions Configuration

### Location
`.claude/settings.json` or `~/.claude/settings.json`

### Format
```json
{
  "permissions": {
    "allow": [
      "Bash(bun run build:*)",
      "Bash(bun run test:*)",
      "Bash(bun run lint:file:*)",
      "mcp__exa__*",
      "Task(web-researcher)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Task(dangerous-agent)"
    ]
  }
}
```

### Wildcard Patterns
- `Bash(npm test:*)` - Any npm test command
- `mcp__exa__*` - All Exa MCP tools
- `Task(*)` - All subagents (use cautiously)

### Access via `/permissions`
Use `/permissions` command to manage at runtime.

---

## 9. File Locations Summary

| Component | Project Location | Global Location |
|-----------|-----------------|-----------------|
| MCP Config | `.mcp.json` | `~/.claude/settings.json` |
| SubAgents | `.claude/agents/*.md` | `~/.claude/agents/*.md` |
| Skills | `.claude/skills/*/SKILL.md` | `~/.claude/skills/*/SKILL.md` |
| Hooks | `.claude/settings.json` | `~/.claude/settings.json` |
| Slash Commands | `.claude/commands/*.md` | `~/.claude/commands/*.md` |
| Instructions | `./CLAUDE.md` | `~/.claude/CLAUDE.md` |
| Permissions | `.claude/settings.json` | `~/.claude/settings.json` |

---

## 10. Composability Pattern

How all mechanisms work together:

```
User Message
    │
    ▼
┌─────────────────────────────────────────────────────────┐
│                     SLASH COMMAND                        │
│  /deep AI regulation                                     │
│  (Explicit trigger, loads prompt template)               │
└─────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────────────────────────┐
│                        SKILL                             │
│  deep-research/ auto-triggers                            │
│  (Loads SKILL.md with research methodology)              │
└─────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────────────────────────┐
│                      ORCHESTRATOR                        │
│  Spawns SubAgents based on task analysis                 │
└─────────────────────────────────────────────────────────┘
    │
    ├──→ SubAgent: Twitter Analyst ──→ MCP: Twitter API
    ├──→ SubAgent: Web Researcher ──→ MCP: Exa, Firecrawl
    ├──→ SubAgent: Academic ──→ MCP: ArXiv
    └──→ SubAgent: News ──→ MCP: RSS
    │
    ▼
┌─────────────────────────────────────────────────────────┐
│                        HOOKS                             │
│  PreToolUse: Validate URLs, log API calls                │
│  PostToolUse: Track sources, verify outputs              │
│  SubagentStop: Collect results for synthesis             │
└─────────────────────────────────────────────────────────┘
    │
    ▼
Final Response to User
```

### Component Selection Guide

| If you need to... | Use |
|-------------------|-----|
| Connect to external APIs | MCP |
| Run parallel/isolated tasks | SubAgents |
| Teach complex workflows | Skills |
| Validate/log/intercept actions | Hooks |
| Create quick shortcuts | Slash Commands |
| Persist team knowledge | CLAUDE.md |
| Build custom integrations | SDK |

---

## 11. Context Engineering Strategies

### The Core Problem
Context window is limited (~200K tokens, but effective limit is lower).

> "Stay under 50-75% context capacity—above that, hallucinations start." — @mrexodia

### Three Strategies (from Manus)

#### 1. Reduce Context
Replace older tool results with file path references.
```
Instead of: Full 10,000 token output in context
Do: "Results written to ./output/analysis.json"
```

#### 2. Offload Context
Store results on filesystem, not in context.
- Execute utilities that write to files
- Reference files instead of content
- Use Bash scripts to process data

#### 3. Isolate Context
Sub-agents with their own context windows.
- Planners pass full context when spawning
- Sub-agents return summaries, not full results
- Main context stays clean

### Context Pollution Symptoms
- Model repeating itself
- "Fixing" same bug different ways
- Undoing previous fixes
- Circular reasoning

### Solution: Deliberate Rotation
- Reset context before pollution builds
- State lives in files + git, NOT the chat
- "If it's not written to a file, it doesn't exist"

---

## 12. Workflow Patterns

### Boris Cherny's Pattern (Claude Code Creator)
1. **Plan Mode** (Shift+Tab twice) - iterate until plan is solid
2. **Auto-Accept Mode** - switch to auto-accept edits
3. **Verification Loop** - tests, types, lint run automatically
4. **Parallel Execution** - multiple Claude sessions simultaneously

### Ralph Methodology (Long-Running Tasks)
```bash
while :; do cat prompt.md | claude-code ; done
```

**File Structure:**
```
project/
├── ralph_task.md              # Single source of truth
└── .ralph/
    ├── guardrails.md          # Learned constraints (append-only)
    ├── progress.md            # Current status
    ├── errors.log             # What broke
    └── activity.log           # Token tracking
```

**Key Insight:**
> "Memory is the filesystem + git, NOT the chat."

### DevDocs Pattern
```
devdocs/
├── plan.md                    # Goals, phases, approach
└── progress.md                # Current status, checkboxes
```

> "Your plan is permanent, code is ephemeral."

---

## 13. Official Documentation Links

### Core Documentation
| Topic | URL |
|-------|-----|
| Main Portal | https://docs.anthropic.com/en/docs/claude-code |
| Overview | https://docs.anthropic.com/en/docs/claude-code/overview |
| Quickstart | https://docs.anthropic.com/en/docs/claude-code/quickstart |
| CLI Reference | https://docs.anthropic.com/en/docs/claude-code/cli-reference |
| Settings | https://docs.anthropic.com/en/docs/claude-code/settings |

### Extensibility
| Topic | URL |
|-------|-----|
| **Hooks** | https://docs.anthropic.com/en/docs/claude-code/hooks |
| Hooks Guide | https://docs.anthropic.com/en/docs/claude-code/hooks-guide |
| **MCP** | https://docs.anthropic.com/en/docs/claude-code/mcp |
| **Sub-Agents** | https://docs.anthropic.com/en/docs/claude-code/sub-agents |
| **Slash Commands** | https://docs.anthropic.com/en/docs/claude-code/slash-commands |
| **SDK** | https://docs.anthropic.com/en/docs/claude-code/sdk |
| Memory | https://docs.anthropic.com/en/docs/claude-code/memory |

### Platform Documentation
| Topic | URL |
|-------|-----|
| Agent Skills | https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview |
| SubAgents SDK | https://platform.claude.com/docs/en/agent-sdk/subagents |
| MCP SDK | https://platform.claude.com/docs/en/agent-sdk/mcp |

### GitHub Repositories
| Repository | URL |
|------------|-----|
| Claude Code | https://github.com/anthropics/claude-code |
| Changelog | https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md |
| Skills Examples | https://github.com/anthropics/skills |
| Python SDK | https://github.com/anthropics/claude-code-sdk-python |
| GitHub Action | https://github.com/anthropics/claude-code-action |

### Key Blog Posts
| Source | Topic | URL |
|--------|-------|-----|
| Anthropic | Agent Skills Architecture | https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills |
| Simon Willison | Skills Analysis | https://simonwillison.net/2025/Oct/16/claude-skills/ |
| Lance Martin | Context Engineering | https://rlancemartin.github.io/2025/10/15/manus/ |

---

## 14. Recent Capabilities (v2.1.x+)

| Feature | Description |
|---------|-------------|
| `context: fork` | Skills run in isolated sub-agent context |
| Agent-specific hooks | Agents can define own PreToolUse/PostToolUse |
| Skills can specify agent | Combine auto-discovery with isolation |
| Background agents | Async communication with main agent |
| Wildcard MCP permissions | `mcp__exa__*` style permissions |
| Dynamic MCP tool updates | `list_changed` for live tool updates |
| Hook `once: true` | Run hook only once per session |
| Middleware hooks | `ask` + `updatedInput` for input modification |
| Disable specific agents | `--disallowedTools "Task(agent-name)"` |

---

## 15. Key Principles

### 1. Subagents for control flow, Skills for composable behavior
Use SubAgents when you need parallelism or isolation. Use Skills when you need methodology.

### 2. Verification = Quality Multiplier
> "Give Claude a way to verify its work. If Claude has that feedback loop, it will 2-3x the quality." — Boris Cherny

### 3. Context Is Precious
Stay under 50-75% capacity. Use filesystem for state, not context.

### 4. Progressive Disclosure
Load only what's needed. Skills metadata (~100 tokens) loads always; body (~5k) only when triggered.

### 5. Compounding Engineering
Every mistake → lesson in CLAUDE.md → prevented next time. Append-only learning.

### 6. CLI Over IDE
> "CLI encourages the manager mindset because you simply don't see the code." — @mrexodia

---

*Last Updated: January 2026*
*Source Project: /Users/noveltokens/2026/claudeCodeDev/claude-code-living-doc/*
