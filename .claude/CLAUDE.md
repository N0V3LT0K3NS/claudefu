# .claude Infrastructure Context

This directory contains Claude Code infrastructure that extends Claude's capabilities.

## What Lives Here

### Skills (`skills/`)

Modular capability packages that load on-demand:

| Skill | Triggers | Purpose |
|-------|----------|---------|
| repo-analyzer | "analyze repo", "extract patterns" | Analyze repositories for Claude Code infrastructure |

### How Skills Work

1. **Discovery**: Claude sees skill descriptions at session start (~100 tokens each)
2. **Activation**: When triggers match or user invokes `/skill-name`, full content loads
3. **Execution**: Claude follows the skill's methodology
4. **Output**: Skill produces defined artifacts (reports, files, etc.)

## Extending This Infrastructure

### Adding a New Skill

```bash
.claude/skills/[skill-name]/
├── SKILL.md                    # Required: Main instructions
├── checklists/                 # Optional: Verification checklists
├── frameworks/                 # Optional: Classification schemas
├── templates/                  # Optional: Output templates
└── scripts/                    # Optional: Executable helpers
```

**SKILL.md Frontmatter:**
```yaml
---
name: skill-name
description: |
  When to use this skill. Be specific about triggers.
triggers:
  - "keyword phrase"
  - "another trigger"
tools:
  - Read
  - Write
  - Bash
model: opus  # or sonnet, haiku
---

# Skill Name

[Methodology and instructions]
```

### Skill Design Principles

1. **Progressive Disclosure**: Description loads first, body only when triggered
2. **Clear Triggers**: Specific phrases that indicate when to activate
3. **Defined Outputs**: What artifacts the skill produces
4. **Tool Restrictions**: Minimal tools needed for the task
5. **Workflow Structure**: Step-by-step methodology

### Relationship to GROK Documentation

Skills in this directory should align with patterns documented in `docs/CLAUDE_CODE_GROK_ENRICHED.md`:

| GROK Section | Relevant Skill Patterns |
|--------------|------------------------|
| Part 2.2 (Skills) | Frontmatter format, progressive disclosure |
| Part 5 (Generative) | Composition patterns, emergent capabilities |
| Part 6 (Operational) | Verification, context management |
| Part 9 (Bootstrapping) | Template patterns, domain adaptation |

### Self-Improvement Loop

```
Use skill → Discover limitation → Improve skill → Document in GROK
     ↑                                                    │
     └────────────────────────────────────────────────────┘
```

When a skill reveals new patterns or limitations:
1. Update the skill to address the limitation
2. If the pattern is generalizable, add to GROK_ENRICHED.md
3. If a new skill is needed, create it following these guidelines

## Current Capabilities

### repo-analyzer

**Purpose**: Deep analysis of repositories for Claude Code infrastructure patterns

**What it finds**:
- CLAUDE.md files (rules, learnings, conventions)
- Skills (frontmatter, workflows, triggers)
- Agents (specializations, tools, relationships)
- Hooks (events, matchers, automation)
- MCP servers (connections, endpoints)
- Commands (arguments, workflows)
- Plugins (manifests, bundled components)

**What it produces**:
- Analysis report (structured inventory + pattern analysis)
- GROK delta (suggested additions to documentation)

**Invocation**: `/repo-analyzer [local path or GitHub URL]`

## Meta-Awareness

This infrastructure is self-describing:
- Skills know how to create more skills
- Analysis produces documentation improvements
- CLAUDE.md files teach Claude about CLAUDE.md files

The goal is **compounding capability**: each use of the infrastructure should make future use easier.
