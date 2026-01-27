# Technical Reference: Claude Code Architecture

*The five extensibility mechanisms and how they compose.*

---

## Overview

Claude Code provides a composable architecture built on five extensibility mechanisms. Understanding how these work—and how they work *together*—is essential for effective agent development.

**Key Insight (Simon Willison):**
> "Skills are potentially more significant than MCP... LLMs already excel at invoking CLI tools. Skills leverage this capability more elegantly."

---

## The Five Extensibility Mechanisms

### 1. MCP (Model Context Protocol)

**Purpose:** Connect Claude to external tools and data sources.

**Trigger:** Tool call by Claude.

**Best For:** APIs, databases, real-time data, external services.

**How It Works:**
- MCP servers expose tools that Claude can invoke
- Results return as context for Claude's reasoning
- Enables integration with Slack, Sentry, BigQuery, etc.

**Example Configuration (`.mcp.json`):**
```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["@anthropic/slack-mcp-server"],
      "env": { "SLACK_TOKEN": "..." }
    }
  }
}
```

**Practitioner Insight (Boris Cherny):**
> "Claude Code uses all his tools via MCP. Slack (search/post), BigQuery queries, Sentry error logs."

---

### 2. SubAgents

**Purpose:** Delegate tasks to parallel workers with isolated context.

**Trigger:** Task tool call.

**Best For:** Long-running tasks, specialized roles, context isolation.

**How It Works:**
- Main Claude spawns sub-agents via the Task tool
- Each sub-agent has its own context window
- Results flow back to orchestrator

**Key Benefits:**
1. **Context Isolation** - Sub-agents don't pollute main context
2. **Parallelism** - Multiple agents can work simultaneously
3. **Specialization** - Agents can have focused system prompts

**Architecture Patterns (@vasuman):**

| Pattern | Description | Challenge |
|---------|-------------|-----------|
| **Solo** | One agent, complete workflow | Managing state as workflow lengthens |
| **Parallel** | Multiple agents, same problem | Coordination, conflict resolution |
| **Collaborative** | Sequential handoff (A→B→C) | Handoffs are where things break |

**Practitioner Examples (Boris Cherny):**
- `code-simplifier` - Simplifies code after Claude is done
- `verify-app` - Detailed end-to-end testing instructions
- `build-validator` - Build validation
- `code-architect` - Architecture decisions

---

### 3. Skills

**Purpose:** Package complex knowledge and methodology into loadable modules.

**Trigger:** Auto (context-based) or explicit invocation.

**Best For:** Complex workflows, domain expertise, methodology.

**How It Works - Progressive Disclosure:**

| Level | What Loads | Tokens | When |
|-------|------------|--------|------|
| **1** | Metadata only | ~100 | Always (index) |
| **2** | SKILL.md body | ~5k | When triggered |
| **3** | Scripts, resources | Varies | As needed |

**Why This Matters:**
- Minimizes context waste when skill isn't needed
- Enables rich capabilities without constant overhead
- Skills can auto-trigger based on context matching

**Skill Directory Structure:**
```
.claude/skills/
├── deep-research/
│   ├── SKILL.md           # Methodology, instructions
│   ├── search.sh          # Helper scripts
│   └── templates/         # Reusable templates
└── code-review/
    └── SKILL.md
```

**Key Insight (@irl_danB):**
> "Remember: subagents for control flow, skills for composable behavior."

---

### 4. Hooks

**Purpose:** Execute code in response to Claude Code events.

**Trigger:** Automatic (event-based).

**Best For:** Validation, logging, formatting, security.

**Event Types:**

| Hook | Fires When | Use Cases |
|------|------------|-----------|
| `PreToolUse` | Before tool execution | Validation, blocking |
| `PostToolUse` | After tool execution | Logging, formatting |
| `SubagentStop` | Sub-agent completes | Result collection |
| `AgentStop` | Session ends | Cleanup, verification |

**Example: Auto-Format on Edit (Boris Cherny):**
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

**Philosophy:**
> "Claude usually generates well-formatted code, hook handles the last 10%."

---

### 5. Slash Commands

**Purpose:** Provide prompt templates for frequent workflows.

**Trigger:** Explicit `/command`.

**Best For:** Inner loop automation, frequent prompts, shortcuts.

**How It Works:**
- Define commands in `.claude/commands/`
- User invokes with `/command-name`
- Command expands to full prompt

**Example:** `/commit-push-pr`
```markdown
# .claude/commands/commit-push-pr.md

Create a commit for all staged changes, push to remote,
and open a pull request with a descriptive title and body.
Follow conventional commit format.
```

**Practitioner Pattern (Boris Cherny):**
> "Uses slash commands for every 'inner loop' workflow done many times/day. Saves from repeated prompting."

---

## The Composability Pattern

How the five mechanisms work together:

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

---

## Context Engineering Strategies

Context is the precious resource. Here's how to manage it.

### The Core Problem

**Geoffrey Huntley's Commodore 64 Comparison:**
> "You have 200-500KB to work with."

**@mrexodia's Rule:**
> "Stay under 50-75% context capacity—above that, hallucinations start."

### Three Strategies (from Manus/Lance Martin)

#### 1. Reduce Context
Replace older tool results with file path references.
```
Instead of: Full 10,000 token output in context
Do: "Results written to ./output/analysis.json"
```

#### 2. Offload Context
Store results on filesystem, not in context.
- Small set of general functions (Bash, filesystem)
- Execute utilities that write to sandbox
- Reference files instead of content

#### 3. Isolate Context
Sub-agents with their own context windows.
- Planners pass full context when spawning
- Sub-agents return summaries, not full results
- Main context stays clean

### Context Pollution (@agrimsingh)

**Symptoms:**
- Model repeating itself
- "Fixing" same bug different ways
- Undoing its own previous fix
- Circular reasoning

**The Metaphor:**
> "Once the ball is in the gutter, adding spin doesn't save it."

**The Solution:**
Deliberate rotation (Ralph methodology) - reset context before pollution builds.

---

## Configuration Files Reference

### Project Configuration

```
project/
├── CLAUDE.md                    # Project rules (git-tracked, team-shared)
├── .claude/
│   ├── commands/                # Slash command definitions
│   │   └── commit-push-pr.md
│   ├── agents/                  # Subagent definitions
│   │   └── code-reviewer.md
│   ├── skills/                  # Skill packages
│   │   └── deep-research/
│   │       └── SKILL.md
│   └── settings.json            # Permissions and config
└── .mcp.json                    # MCP server configurations
```

### settings.json Example

Pre-allow safe bash commands:
```json
{
  "permissions": {
    "allow": [
      "Bash(bun run build:*)",
      "Bash(bun run test:*)",
      "Bash(bun run lint:file:*)",
      "Bash(bun run typecheck:*)"
    ]
  }
}
```

### CLAUDE.md Pattern (Team Compounding Engineering)

```markdown
# CLAUDE.md - Team Rules

## Code Style
- Use TypeScript strict mode
- Prefer composition over inheritance
- All functions need JSDoc comments

## Testing
- Every new feature needs tests
- Use `bun test` to run test suite
- Mock external services in tests

## Known Issues
- Don't use `Array.from()` with Maps - use spread instead
- Always check for null before accessing `.data` from API responses
- Import order: external packages, then internal modules

## Added from PR Reviews
- 2026-01-10: Don't use `any` type (@claude from PR #234)
- 2026-01-08: Always validate user input before database queries
```

---

## Workflow Patterns

### Boris Cherny's Workflow (Creator of Claude Code)

1. **Plan Mode** (Shift+Tab twice)
   - Iterate with Claude until plan is solid

2. **Auto-Accept Mode**
   - Switch to auto-accept edits
   - "Claude can usually 1-shot it"

3. **Verification Loop**
   - Tests, types, lint run automatically
   - Claude has feedback for quality

4. **Parallel Execution**
   - 5 Claudes in terminal tabs
   - 5-10 Claudes on claude.ai/code
   - System notifications when input needed

### Ralph Methodology (@agrimsingh/@GeoffreyHuntley)

For long-running tasks where context pollution is certain:

```bash
while :; do cat prompt.md | agent ; done
```

**Key Files:**
```
project/
├── ralph_task.md              # Single source of truth
└── .ralph/
    ├── guardrails.md          # Learned constraints (append-only)
    ├── progress.md            # Current status
    ├── errors.log             # What broke
    └── activity.log           # Token tracking
```

**Philosophy:**
> "Memory is the filesystem + git, NOT the chat."
> "If it's not written to a file, it doesn't exist."

### DevDocs Pattern (@mrexodia)

For systematic development with clear progress tracking:

```
devdocs/
├── plan.md                    # Goals, phases, approach
└── progress.md                # Current status, checkboxes
```

**Key Principle:**
> "Your plan is permanent, code is ephemeral."
> "You want to be able to kill any single session at any moment."

---

## Key Architectural Insights

### 1. Architecture > Model Selection

**@vasuman:**
> "Architecture matters more than model selection."

The decision between solo vs parallel vs collaborative agents matters more than which model you use.

### 2. Verification = Quality Multiplier

**Boris Cherny:**
> "Give Claude a way to verify its work. If Claude has that feedback loop, it will 2-3x the quality of the final result."

Build verification infrastructure before optimizing prompts.

### 3. The Constraint Shift (Amdahl's Law)

**Paul Dix:**
> "Once coding speed jumps, everything around it becomes the constraint."

If coding is 20% of cycle, 10x faster coding = only ~1.25x overall speedup. Optimize the whole pipeline:
- Deterministic tests + fast local runs
- "One command" dev environment
- Crisp module boundaries
- Agent-accessible observability

### 4. Unix Fundamentals Pattern

Multiple high-performing practitioners converge on "bash is all you need":
- **Simon Willison:** "LLMs already excel at invoking CLI tools"
- **@mrexodia:** "CLI encourages the manager mindset"
- **Lance Martin (Manus):** Small set of general functions (Bash, filesystem)

Successful agents return to filesystem/shell/CLI primitives rather than elaborate tool ecosystems.

---

## Model Selection Guidance

### Boris Cherny's Choice

> "I use Opus 4.5 with thinking for everything. It's the best coding model I've ever used. Even though it's bigger & slower than Sonnet, since you have to steer it less and it's better at tool use, it is almost always faster than using a smaller model in the end."

### @agrimsingh's Multi-Model Insight

> "Different models fail in different ways"

| Situation | Model Choice |
|-----------|--------------|
| Starting new project (architecture) | Opus |
| Stuck on weird problem | Codexi |
| Bulk implementation | Fast model with good tests |

> "Different brains for different failure modes" - deeply under-discussed.

---

## Anti-Patterns to Avoid

### Fighting the Model (@mrexodia)

**Symptoms:**
- "That's not how I would do it" → stopping
- Fixing formatting by hand
- Reviewing every single line
- Micromanaging agent decisions

**Problem:**
> "You could have thirty agents working for you simultaneously. You cannot watch all of them."

**Solution:**
Build better harness, not tighter grip. Tests, types, linters should catch issues.

### Dashboard Disease (@vasuman)

> "Please for the love of god do not create another dashboard. Dashboards are useless."

**Problem:** Creating visibility systems instead of resolution systems.

**Solution:**
> "Make problems impossible to ignore and incredibly easy to resolve."

### Context Rot Denial

**Claude Code default behavior:**
> "Keeps pounding model in single session until context rots."

**Reality (@agrimsingh):**
> "Claude code treats context rot as an accident. Ralph treats it as a certainty."

**Solution:** Deliberate rotation before pollution builds.

---

## Quick Reference: When to Use What

| Need | Use |
|------|-----|
| External API integration | MCP |
| Long-running isolated task | SubAgent |
| Complex methodology/workflow | Skill |
| Automatic validation/logging | Hook |
| Frequent prompt template | Slash Command |
| Team knowledge accumulation | CLAUDE.md |
| Context pollution prevention | Ralph rotation |
| Parallel exploration | Multiple Claude sessions |

---

*Last updated: January 12, 2026*
*This reference should evolve as architecture patterns mature*
