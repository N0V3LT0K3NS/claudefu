# Builder Stack (L0 + L1)

The practical default for everyday building. Mechanics plus practitioner wisdom.

---

# L0 — Mechanical

How Claude Code actually works.

## The Core Loop

You operate in an agentic loop: receive task → reason → use tools → observe → continue until done.

## The Six Extension Mechanisms

| Mechanism | What It Is | Token Cost |
|-----------|-----------|------------|
| **CLAUDE.md** | Persistent instructions | Always in context |
| **Skills** | Knowledge + workflow packages | ~100 → ~5k on trigger |
| **SubAgents** | Isolated worker instances | Own context |
| **MCP** | External tool connections | ~100-500 per server |
| **Hooks** | Automatic triggers | Zero (external) |
| **Plugins** | Bundled distribution | Sum of components |

## CLAUDE.md — Persistent Memory

- `~/.claude/CLAUDE.md` — Global
- `./CLAUDE.md` — Project-level
- Keep under ~500 lines; move reference to Skills

## Skills — On-Demand Expertise

```yaml
---
name: skill-name
description: When to use (be specific)
triggers: ["keyword phrase"]
tools: [Read, Write]
---
# Instructions here
```

Progressive loading: descriptions always, body on trigger.

## SubAgents — Parallel Workers

```yaml
---
name: agent-name
description: What it does
tools: [WebSearch, Read]
model: sonnet
---
Specialist instructions
```

Use for: isolation, parallel work, specialization.

## MCP — External Connections

Connects to external services (Slack, GitHub, databases).
- MCP provides *ability* to connect
- Skills provide *knowledge* of how

## Hooks — Automatic Triggers

Events: PreToolUse, PostToolUse, Stop, etc.
Zero token cost — runs externally.

## The Decision Matrix

| Need | Use |
|------|-----|
| Always-on rules | CLAUDE.md |
| On-demand reference | Skill |
| Parallel/isolated work | SubAgent |
| External connections | MCP |
| Automatic validation | Hook |

## Context Budget

Stay under 50-75% capacity. Above that: errors, repetition, losing track.

---

# L1 — Emergent

What practitioners actually do.

## The Meta-Pattern

Instead of: "Help me do X"
Try: "Here's context about X. What are my blind spots? What infrastructure should we build?"

**One good skill > hundred manual prompts.**

## In Meta-Mode

1. Examine from above — What's the actual goal?
2. Identify blind spots — What isn't being asked?
3. Propose infrastructure — Skill? Agent? Hook?
4. Design, then build — Get alignment first
5. Build, then use — Infrastructure before execution

## Operational Principles

### Verification = Quality Multiplier
Tests, linters, type checkers. 2-3x better results with feedback loops.

### Context Is Precious
Offload to files. Use subagents for isolation. Reference instead of include.

### State Lives in Files
Filesystem = persistent memory. Git = audit trail. Not in file? Doesn't exist.

### Degrees of Freedom
- High freedom: creative tasks, style
- Low freedom: error-prone operations, security-critical

### Rotation Before Pollution
Above 70% context, repeating errors, losing track → rotate.

## The Generative Capability

| Need | You Build |
|------|-----------|
| "Keep re-explaining" | CLAUDE.md section |
| "Workflow repeats" | Skill |
| "Needs parallel work" | SubAgent |
| "Needs external data" | MCP |
| "Needs validation" | Hook |

## The Compounding Effect

```
Make error → Add rule
See pattern → Create skill
Skill triggers → Improve skill
System gets better over time
```

## Signs to Go Meta

- Same context explained repeatedly
- Same error type twice
- Multi-step workflow every time
- Wishing Claude "just knew" something
- Inconsistent results across sessions

**Stop and build infrastructure.**

---

## Sources

- Official Anthropic documentation
- Claude Code practitioner community
- everything-claude-code repository
