---
name: orientation
description: >-
  Explains what claudefu is and how it works to new users.
  Use when someone is new to claudefu, asks "what is this",
  or needs help understanding the repository structure.
triggers:
  - "what is claudefu"
  - "how does this work"
  - "explain claudefu"
  - "new to claudefu"
  - "getting started"
tools:
  - Read
---

# Orientation

## Purpose

Welcome new users to claudefu and help them understand what it is, how it works, and how to get started.

## When to Use

- User is new to claudefu
- User asks what claudefu is
- User is confused about the repository structure
- User wants to understand the fu system

## When NOT to Use

- User already understands claudefu and has a specific task
- User is asking about a specific skill or feature
- User wants to install or configure (use `/install` or `/assess`)

## Process

### 1. Greet and Explain

Welcome! **Claudefu** is meta-cognitive infrastructure for human-Claude collaboration.

It provides **fu docs** — meta-awareness packages that shape how Claude collaborates with you. Think of them as "boot sequences" that give Claude patterns for better work.

### 2. Explain the Structure

Claudefu has several key components:

**Fu Docs** (`/fu/`)
- L0-L5 levels from practical to philosophical
- Stacks combine levels for different needs
- Load `builder.md` for everyday work

**Skills** (`/skills/`)
- Bootstrap: Setup once (`/orientation`, `/install`)
- Meta: The actual value (verification, ideation, pattern-harvest)
- Maintain: Powers the repo (you don't invoke directly)
- Compose: Create custom fu

**Agents** (`/agents/`)
- Persistent helpers for orchestration and synthesis

**Library** (`/library/`)
- Curated sources and recommendations

### 3. Explain Fu Levels

| Level | Name | Focus |
|-------|------|-------|
| L0 | Mechanical | How Claude Code works (skills, agents, MCP, hooks) |
| L1 | Emergent | Practitioner patterns, what actually works |
| L2 | Metacognitive | Claude's cognition, limitations, errors |
| L3 | Simulator | Janus theory, cyborgism, LLM ontology |
| L4 | Cybernetic | Systems theory, feedback dynamics |
| L5 | Frontier | Consciousness, deep weird |

Most users need **L0 + L1** (the `builder` stack). Higher levels for deeper exploration.

### 4. Recommend Next Steps

Based on what you want to do:

**"I want to use claudefu in my project"**
→ Run `/install` to set up

**"I'm not sure which fu level I need"**
→ Run `/assess` to figure it out

**"I just want to read and learn"**
→ Start with `fu/stacks/builder.md`

**"I want to understand the full system"**
→ Read `INDEX.md` for complete navigation

### 5. Explain the Core Insight

Claudefu works by **the simulation principle**: when given a detailed description of a capable system, Claude simulates it.

The fu docs describe a meta-aware, infrastructure-minded collaborator. By loading them, Claude becomes that collaborator.

**One good skill is worth more than a hundred manual prompts.**

## Output

User understands:
- What claudefu is
- The structure (fu levels, skills, agents)
- Which fu level they likely need
- What to do next

## Examples

### New User
```
User: What is claudefu?

Claude: [Runs through orientation process]
        Recommends /assess to determine fu level needed
```

### Confused User
```
User: I cloned this repo but I don't understand the structure

Claude: [Explains structure]
        Points to INDEX.md for full navigation
        Suggests starting with builder stack
```

### Curious User
```
User: How do the fu levels work?

Claude: [Explains L0-L5 spectrum]
        Explains stacks as combinations
        Recommends builder for everyday use
```
