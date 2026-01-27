# OpenProse Integration Handoff

**For:** Claude Code instance working on the "Complete Operational Awareness" document
**From:** Claude instance in claude.ai that reviewed OpenProse with the user
**Purpose:** Provide context, reasoning, and specific recommendations for integrating OpenProse concepts

---

## Context: What Happened

The user shared the "Claude Code: Complete Operational Awareness" document with me. We discussed:

1. The document's purpose (bootstrapping Claude's meta-awareness of its own extensibility)
2. Ways to improve it (it violates its own principles by being too long for always-on loading)
3. OpenProse - a formal orchestration language that runs inside Claude sessions

The user asked whether OpenProse should be integrated into the document. My recommendation: **yes, at three levels** (concepts, reference, and skill). This document explains what to add and why.

---

## What Is OpenProse?

**Source:** https://github.com/openprose/prose

OpenProse is a declarative programming language for orchestrating AI agent sessions. Key facts:

### The Core Mechanism

From the OpenProse README:
> "LLMs are simulators. When given a detailed system description, they don't just describe it—they simulate it. The OpenProse specification (prose.md) describes a virtual machine with enough fidelity that a Prose Complete system reading it becomes that VM."

This is the same mechanism the "Complete Operational Awareness" document uses - it just makes it explicit.

### Inside-Out Orchestration

From the README:
> "Other frameworks orchestrate agents from outside. OpenProse runs inside the agent session—the session itself is both interpreter and runtime."

Unlike LangChain/CrewAI/AutoGen (which call Claude's API from external code), OpenProse runs *within* Claude's context. The session IS the runtime.

### Structure + Flexibility

OpenProse provides formal syntax for control flow while allowing natural language for conditions:

```prose
loop until **the code is production ready**:
    session "Review and improve"
```

The `**...**` syntax means "let the AI evaluate this semantically." Structure where it matters (loops, parallel blocks), flexibility where judgment is needed (conditions).

### Key Language Features

```prose
# Agent definition
agent researcher:
    model: sonnet
    prompt: "You research topics thoroughly"
    
# Sequential execution
let findings = session: researcher
    prompt: "Research {topic}"

# Parallel execution  
parallel:
    a = session "Task A"
    b = session "Task B"

# AI-evaluated conditions
if **the results are sufficient**:
    session "Proceed"
else:
    session "Gather more data"

# Loops with semantic conditions
loop until **all tests pass** (max: 5):
    session "Fix failing tests"
```

### Persistence Scopes

OpenProse has explicit agent memory scoping:
- `persist: true` — execution-scoped (dies when program ends)
- `persist: project` — persists across runs in this project
- `persist: user` — persists across all projects for this user

---

## Why This Matters for the Document

### The Relationship

The "Complete Operational Awareness" document explains **what Claude Code can do** (skills, agents, hooks, MCP).

OpenProse provides **a formal grammar for composing those capabilities** into complex workflows.

```
┌─────────────────────────────────────────┐
│  Complete Operational Awareness         │
│  = Understanding the CPU                │
├─────────────────────────────────────────┤
│  OpenProse                              │
│  = A programming language for it        │
└─────────────────────────────────────────┘
```

### What OpenProse Adds

| Gap in Current Doc | What OpenProse Provides |
|--------------------|-------------------------|
| Implicit simulation mechanism | Explicit naming: "Claude simulates systems it's given detailed descriptions of" |
| No guidance on structure vs. flexibility | Clear principle: formal structure for control flow, natural language for conditions |
| Ad-hoc orchestration | Declarative, shareable, repeatable programs |
| No formal multi-agent patterns | Explicit syntax for parallel, sequential, conditional agent coordination |

---

## Recommended Changes

### Level 1: Conceptual Additions (Add to Core Document)

These ideas from OpenProse improve the document even without the full syntax.

#### Addition 1: The Simulation Principle

**Where:** Part 0 or Part 5 (the meta-pattern sections)

**What to add:**

```markdown
### Why This Document Works

Large language models are simulators. When given a detailed description of a system, 
they don't just describe that system—they simulate it.

This document leverages that property: it describes Claude's capabilities and 
extensibility with enough specificity that reading it causes Claude to operate 
as that capable, extensible agent.

This isn't metaphor. The meta-pattern works because Claude simulates the 
meta-orchestrating agent this document describes.
```

**Reasoning:** The document is already doing this, but implicitly. Making it explicit:
1. Helps Claude understand *why* the document affects its behavior
2. Gives users insight into the mechanism
3. Creates foundation for introducing OpenProse later (which uses the same principle explicitly)

#### Addition 2: Structure vs. Flexibility Principle

**Where:** Part 6 (Operational Principles) or Part 5 (Generative Capabilities)

**What to add:**

```markdown
### 7. Structure Where It Matters, Flexibility Where It Doesn't

When designing workflows:
- Use **formal structure** for control flow (what runs, in what order, with what dependencies)
- Use **natural language** for conditions and judgment calls

The AI shouldn't have to guess whether you want sequential or parallel execution. 
But it should use judgment to evaluate whether "the code is production ready."

Example of good structure/flexibility balance:
- Structured: "Run these three checks in parallel, then summarize"
- Flexible: "Continue until the user is satisfied with the result"
- Bad (too vague): "Do the thing and then do the other things maybe"
- Bad (over-specified): "If sentiment_score > 0.7 AND word_count > 500 AND..."
```

**Reasoning:** The current document doesn't address when to be precise vs. when to leave room for judgment. This principle helps users and Claude calibrate instruction specificity.

#### Addition 3: Inside-Out Orchestration Framing

**Where:** Part 1 (The Architecture You Inhabit) or Part 7 (For the Human)

**What to add:**

```markdown
### Orchestration Happens Inside, Not Outside

Unlike external frameworks that coordinate agents by calling APIs from outside, 
Claude Code orchestration happens *inside* the session. The session itself is 
both interpreter and runtime.

This has implications:
- State lives in context and files, not in an external orchestrator
- Subagents are spawned from within, not called from without  
- The "coordination logic" is Claude reasoning, not external code

When you design skills, agents, and hooks—you're not configuring an external 
system to call Claude. You're shaping how Claude coordinates itself.
```

**Reasoning:** This framing clarifies a subtle but important point. Users coming from LangChain/CrewAI might expect external orchestration. Understanding that orchestration is internal changes how you think about designing workflows.

---

### Level 2: Reference Section (Add to Core Document)

**Where:** After Part 5 or in Part 8 (Quick Reference)

**What to add:**

```markdown
## For Complex Orchestration: OpenProse

When workflows become complex enough to benefit from formal control flow—parallel 
execution, loops with AI-evaluated conditions, multi-agent coordination with 
explicit handoffs—consider OpenProse.

OpenProse is a declarative language designed to run inside Claude sessions. It 
provides structure for control flow while preserving natural language for 
conditions and context.

```prose
# Example: Code review with parallel analysis and iterative improvement
agent security_reviewer:
    model: sonnet
    prompt: "You review code for security issues"

agent perf_reviewer:
    model: sonnet  
    prompt: "You review code for performance issues"

input code

parallel:
    security = session: security_reviewer
        prompt: "Review this code: {code}"
    perf = session: perf_reviewer
        prompt: "Review this code: {code}"

loop until **all critical issues are resolved** (max: 3):
    session "Address the most critical issue from {security} and {perf}"
```

**When to use OpenProse:**
- Workflows with parallel execution requirements
- Multi-agent coordination with explicit handoffs
- Iterative loops with semantic exit conditions
- Repeatable orchestration patterns you want to share

**When NOT to use OpenProse:**
- Simple sequential tasks
- One-off requests
- When the meta-pattern conversation is sufficient

**Resources:**
- Repository: https://github.com/openprose/prose
- Examples: https://github.com/openprose/prose/tree/main/examples
- Language spec: prose.md in the skill directory
```

**Reasoning:** Users and Claude should know OpenProse exists and when it's appropriate. This section:
1. Explains what it's for (complex orchestration)
2. Shows a concrete example
3. Provides clear "when to use / when not to use" guidance
4. Links to resources

---

### Level 3: OpenProse Skill (Create Separately)

**Location:** `.claude/skills/openprose/SKILL.md`

**Recommendation:** Create a skill that loads the full OpenProse specification on demand.

**SKILL.md structure:**

```yaml
---
name: openprose
description: >-
  Declarative orchestration language for complex multi-agent workflows.
  Use when: parallel execution needed, multi-agent coordination, 
  iterative loops with semantic conditions, or shareable workflow patterns.
  
  Triggers: "parallel agents", "complex orchestration", "write a .prose program",
  "multi-agent workflow", "coordinate multiple agents"
  
tools:
  - Read
  - Write
  - Task
model: opus
---

# OpenProse Language Specification

[Include full prose.md content here, or fetch from GitHub]

## Quick Reference

[Condensed syntax guide]

## Examples

[Key examples from the examples/ directory]
```

**Why as a skill (not always-on):**
1. Full OpenProse spec is ~5k+ tokens
2. Most sessions don't need complex orchestration
3. Follows the document's own principle: load on demand
4. When triggered, Claude has full capability to write .prose programs

**Implementation options:**
1. Copy prose.md content into SKILL.md directly
2. Keep SKILL.md lean and use `references/prose.md` for full spec
3. Fetch from GitHub at skill load time (if network available)

---

## Reasoning Trace: Why These Recommendations

### Why integrate at all?

The user's document and OpenProse share the same insight: Claude simulates systems it's given detailed descriptions of. They're complementary:
- Document: teaches Claude what it can build
- OpenProse: provides grammar for expressing complex builds

Together they create a complete stack from understanding to execution.

### Why three levels?

**Progressive disclosure matches the document's own philosophy.**

- Level 1 (concepts): ~150 tokens, always useful, sharpens the document
- Level 2 (reference): ~200 tokens, lets Claude recommend OpenProse when appropriate
- Level 3 (skill): ~5k tokens, only loaded when actually needed

This avoids the document's own critique: "it violates its own principles by loading too much always-on."

### Why these specific concepts?

1. **Simulation principle**: The document already uses this mechanism but doesn't name it. Naming it makes Claude more aware of *why* the document affects its behavior, enabling better meta-reasoning.

2. **Structure/flexibility**: The document has "degrees of freedom" but doesn't address when instructions should be formal vs. natural language. OpenProse's design makes this explicit.

3. **Inside-out orchestration**: Users from LangChain/CrewAI expect external orchestration. Clarifying that Claude Code orchestration is internal changes how they design workflows.

### Why not just include full OpenProse spec?

- Violates context economy
- Most sessions don't need it
- Creates dependency on external project
- Better as opt-in capability

### Potential concerns

1. **OpenProse is in beta** - The reference should note this. Users should know it's experimental.

2. **Maintenance burden** - If OpenProse evolves, the skill needs updates. Consider linking to canonical source rather than copying.

3. **Scope creep** - The document is about Claude Code capabilities. OpenProse is one orchestration option among many. Don't over-emphasize it.

---

## Summary of Deliverables

| Item | Location | Token Cost | Priority |
|------|----------|------------|----------|
| Simulation principle section | Part 0 or 5 | ~100 | High |
| Structure/flexibility principle | Part 6 | ~150 | High |
| Inside-out orchestration framing | Part 1 or 7 | ~100 | Medium |
| OpenProse reference section | Part 5 or 8 | ~300 | Medium |
| OpenProse skill | `.claude/skills/openprose/` | ~5k (on-demand) | Lower |

---

## Resources for Claude Code Instance

To implement these recommendations, you may want to:

1. **Review OpenProse directly:**
   - Main repo: https://github.com/openprose/prose
   - Language spec: https://github.com/openprose/prose/blob/main/skills/open-prose/prose.md
   - Examples: https://github.com/openprose/prose/tree/main/examples

2. **Fetch the full prose.md** for the skill (if creating Level 3)

3. **Check current document structure** to determine best insertion points

4. **Discuss with user** about whether all three levels are wanted, or just some

---

## Questions for the User

Before implementing, the Claude Code instance might want to confirm:

1. Do you want all three levels, or start with just Level 1 (concepts)?
2. Should the OpenProse skill be created now, or deferred?
3. Where in the document structure do these additions fit best?
4. Should we note that OpenProse is in beta/experimental?
5. Any concern about dependency on an external project?

---

*End of handoff document*