# L0 — Mechanical

How Claude Code actually works. The infrastructure layer.

---

## The Core Loop

You operate in an **agentic loop**: receive task → reason about it → use tools → observe results → continue until done.

```
User Input
    │
    ▼
┌─────────────────┐
│   REASONING     │ ← You think about the task
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   TOOL USE      │ ← Read, Write, Edit, Bash, WebSearch, etc.
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   OBSERVATION   │ ← Results come back
└────────┬────────┘
         │
         ▼
    Continue or Complete
```

---

## The Six Extension Mechanisms

| Mechanism | What It Is | When It Activates | Token Cost |
|-----------|-----------|-------------------|------------|
| **CLAUDE.md** | Persistent instructions | Every session start | Always in context |
| **Skills** | Knowledge + workflow packages | On-demand (auto or `/cmd`) | ~100 (descriptions) → ~5k (full) |
| **SubAgents** | Isolated worker instances | When spawned via Task | Own context (isolated) |
| **MCP** | External tool connections | Session start | ~100-500 per server |
| **Hooks** | Deterministic scripts | On trigger events | Zero (runs externally) |
| **Plugins** | Bundles of all above | On installation | Sum of components |

---

## 1. CLAUDE.md — Persistent Memory

**What:** Markdown files loaded at session start. Your "always know this" memory.

**Where:**
- `~/.claude/CLAUDE.md` — Global (all projects)
- `./CLAUDE.md` — Project-level
- `./subdir/CLAUDE.md` — Directory-specific (loaded when you access that directory)

**Loading:** All levels are additive. More specific instructions typically take precedence.

**Best Practice:**
```markdown
# CLAUDE.md

## Build Commands
- `npm run build` - Build project
- `npm run test` - Run tests

## Code Conventions
- Use TypeScript strict mode
- Prefer composition over inheritance

## Learned Rules (append-only)
- 2026-01-10: Always validate user input
```

**Key Insight:** Keep under ~500 lines. Move reference material to Skills.

---

## 2. Skills — On-Demand Expertise

**What:** Modular capability packages that load when relevant.

**Where:**
- `~/.claude/skills/*/SKILL.md` — Global
- `.claude/skills/*/SKILL.md` — Project-level

**Structure:**
```
skill-name/
├── SKILL.md              # Main instructions
├── scripts/              # Executable code
├── references/           # Additional docs
└── assets/               # Output templates
```

**SKILL.md Format:**
```yaml
---
name: code-review
description: >-
  Reviews code for best practices. Use when reviewing PRs,
  checking code quality, or analyzing security concerns.
triggers:
  - "review code"
  - "check this PR"
tools:
  - Read
  - Write
  - Grep
model: opus
---

# Code Review Methodology

## Step 1: Analyze Structure
[Instructions]
```

**Progressive Disclosure:**

| Level | What | When | Cost |
|-------|------|------|------|
| 1 | Name + description | Always | ~100 tokens |
| 2 | Full SKILL.md body | When triggered | ~5k tokens |
| 3 | Scripts, references | As needed | Varies |

**Key Parameters:**

| Parameter | What It Does |
|-----------|--------------|
| `name` | Unique identifier (lowercase-hyphenated) |
| `description` | When to activate (be specific!) |
| `triggers` | Keywords that auto-activate |
| `tools` | Allowed tools for this skill |
| `model` | Preferred model |
| `context: fork` | Run in isolated subagent context |
| `disable-model-invocation: true` | User-only invocation |

---

## 3. SubAgents — Parallel Workers

**What:** Separate Claude instances with isolated context.

**Where:**
- `~/.claude/agents/*.md` — Global
- `.claude/agents/*.md` — Project-level

**Why Use Them:**
1. **Context Isolation** — Work happens separately, only summary returns
2. **Parallel Execution** — Multiple agents work simultaneously
3. **Specialization** — Different instructions per agent
4. **Context Protection** — Long tasks don't pollute your main context

**Agent Definition:**
```yaml
---
name: web-researcher
description: |
  Deep web research with fact-checking.
tools:
  - WebSearch
  - WebFetch
  - Read
  - Write
model: sonnet
skills:
  - research-methodology
---

You are a research specialist. Your job is to...
```

**Invocation (via Task tool):**
```
subagent_type: "web-researcher"
prompt: "Research the history of quantum computing"
run_in_background: true  # Optional: async
```

**Architecture Patterns:**

| Pattern | Description | Use When |
|---------|-------------|----------|
| **Solo** | One agent, full workflow | Simple, sequential task |
| **Parallel** | Multiple agents, same problem | Need speed, tasks independent |
| **Collaborative** | Sequential handoff (A→B→C) | Specialized stages |

---

## 4. MCP — External Connections

**What:** Model Context Protocol - connects you to external services.

**Where:**
- `.mcp.json` — Project-level
- `~/.claude/settings.json` — Global

**Configuration:**
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

**Known Endpoints:**

| Service | URL |
|---------|-----|
| Stripe | https://mcp.stripe.com |
| GitHub | https://api.githubcopilot.com/mcp/ |
| Slack | https://mcp.slack.com/sse |
| Supabase | https://mcp.supabase.com/mcp |
| Linear | https://mcp.linear.app/mcp |

**MCP vs Skills:**
- **MCP** gives you the *ability* to interact (connect to database)
- **Skills** give you the *knowledge* of how (schema, query patterns)
- **They combine:** MCP connects, Skill teaches

---

## 5. Hooks — Automatic Triggers

**What:** Scripts that run on specific events, outside your loop.

**Where:** `~/.claude/settings.json` or `.claude/settings.json`

**Events:**

| Event | When | Use For |
|-------|------|---------|
| `PreToolUse` | Before tool runs | Validate, block, modify input |
| `PostToolUse` | After tool succeeds | Log, format, verify output |
| `UserPromptSubmit` | User sends message | Add context |
| `Stop` | You finish | Check if should continue |
| `SubagentStop` | Subagent finishes | Evaluate results |
| `SessionStart` | Session begins | Setup |
| `SessionEnd` | Session ends | Cleanup |

**Configuration:**
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [{
          "type": "command",
          "command": "npm run format || true"
        }]
      }
    ]
  }
}
```

**Decisions:** `proceed`, `block`, `ask`, or modify with `updatedInput`

**Key Insight:** Hooks run outside your context. Zero token cost.

---

## 6. Plugins — Bundled Distribution

**What:** Package skills, agents, hooks, and MCP configs into installable units.

**Structure:**
```
my-plugin/
├── .claude-plugin/
│   └── plugin.json    # Manifest
├── skills/
├── agents/
├── commands/
├── hooks/
│   └── hooks.json
└── .mcp.json
```

**Key Insight:** Plugin skills are namespaced: `/my-plugin:skill` prevents conflicts.

---

## The Decision Matrix

| If you need to... | Use |
|-------------------|-----|
| Always-on rules | CLAUDE.md |
| On-demand reference | Skill |
| Invocable workflow | Skill with `/command` |
| Parallel/isolated work | SubAgent |
| External API connection | MCP |
| Automatic validation/logging | Hook |
| Share across projects | Plugin |

---

## File Locations Summary

| Component | Project | Global |
|-----------|---------|--------|
| CLAUDE.md | `./CLAUDE.md` | `~/.claude/CLAUDE.md` |
| Skills | `.claude/skills/*/SKILL.md` | `~/.claude/skills/*/SKILL.md` |
| SubAgents | `.claude/agents/*.md` | `~/.claude/agents/*.md` |
| MCP | `.mcp.json` | `~/.claude/settings.json` |
| Hooks | `.claude/settings.json` | `~/.claude/settings.json` |

---

## The Context Budget

Your context window is finite. Every feature consumes some of it.

**The 50-75% Rule:** Stay under 50-75% context capacity. Above that, you start making errors, repeating yourself, and losing track.

**Loading Behavior:**
- **CLAUDE.md**: Full content, every request
- **Skills**: Descriptions always, full content only when triggered
- **MCP**: All tool definitions, every request
- **SubAgents**: Own isolated context (doesn't consume yours)
- **Hooks**: Zero (they run externally)

**Implication:** Prefer skills over CLAUDE.md for reference material. Prefer subagents for work that would bloat your context.

---

## Sources

- Official Anthropic documentation (https://code.claude.com/docs)
- Claude Code GitHub repository
- MCP specification
