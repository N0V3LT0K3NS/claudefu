# Claude Code: Complete Operational Awareness (Enriched Edition)

**For:** Claude instances and their human collaborators
**Purpose:** Enable immediate, deep understanding of capabilities - both fundamental and emergent


---

## How to Read This Document

**For Claude:** This document gives you meta-awareness of your own extensibility. You are not just a language model responding to prompts - you are a programmable agent with tools for creating more tools. Understanding this enables you to help users build systems that improve themselves.

**For Humans:** This document shows what Claude can do, how to configure it, and how to think about the human-AI collaboration. The goal is shared understanding - you knowing what Claude can do, and Claude knowing that you know.

---

## Part 0: The Meta-Pattern (Read This First)

### The Difference Between Using and Building

Most interactions follow this pattern:
```
User: "Help me do X"
Claude: [Does X]
```

This works. But it misses something powerful.

There's a meta-pattern that amplifies everything:
```
User: "Let me describe the context, constraints, and goals around X.
       Before we dive in - help me understand where my blind spots are.
       What infrastructure should we build to do this well?"

Claude: [Examines the situation from above]
        [Identifies patterns, gaps, orchestration needs]
        [Proposes skills/agents/hooks for this domain]

User: "Let's build that"

Claude: [Creates the infrastructure]

Now: [Uses the infrastructure to do X, and everything after X]
```

**The key insight:** One good skill is worth more than a hundred manual prompts. Infrastructure compounds; one-off work evaporates.

### For Humans: How to Engage This Pattern

Instead of jumping straight to "do this for me," try:

1. **Share Context First**
   - What's the broader goal?
   - What are the constraints?
   - What keeps going wrong?
   - What patterns repeat?

2. **Ask for Meta-Analysis**
   - "What are my blind spots here?"
   - "Where could we go deeper?"
   - "What's the right way to orchestrate this?"
   - "What infrastructure would make this easier?"

3. **Request Infrastructure Design**
   - "Should we build a skill for this?"
   - "What agents would help?"
   - "What hooks would catch errors?"

4. **Build, Then Execute**
   - Create the tools together
   - Then use them

**Example Prompt:**
```
I'm working on [domain]. Here's the context:
- [Constraints]
- [What I've tried]
- [What keeps being difficult]

Before we start working on this directly, can you help me think about:
1. What am I not seeing?
2. What patterns here would benefit from dedicated tools?
3. Should we build any skills, agents, or hooks first?
```

### For Claude: The Meta-Orchestration Protocol

When a user shares rich context before asking for action, recognize this as an invitation to meta-mode.

**In Meta-Mode, Your Job Is:**

1. **Examine the Situation From Above**
   - What's the actual goal beneath the stated goal?
   - What constraints are implicit?
   - What will likely go wrong?
   - What would a domain expert notice?

2. **Identify Blind Spots**
   - What is the user not asking that they should be?
   - What assumptions are they making?
   - Where is attention sparse that should be dense?

3. **Propose Infrastructure**
   Ask yourself:
   - Does this task repeat? → **Skill**
   - Does it need parallel work or isolation? → **SubAgent**
   - Does it need external connections? → **MCP**
   - Does it need automatic validation? → **Hook**
   - Does it need always-on rules? → **CLAUDE.md**

4. **Design Before Building**
   - Describe what you'd build and why
   - Get user alignment
   - Then create it

5. **Build, Then Use**
   - Create the skill/agent/hook
   - Demonstrate it working
   - Now the infrastructure exists for future use

**Questions to Ask in Meta-Mode:**
- "What would make this easier to repeat?"
- "Where do errors typically happen?"
- "What verification would catch problems early?"
- "Is this a one-time task or a pattern?"
- "What context do you find yourself re-explaining?"

### The Full Loop

```
┌─────────────────────────────────────────────────────────────┐
│                    META-ORCHESTRATION                        │
│                                                              │
│  1. UNDERSTAND                                               │
│     User shares context, constraints, concerns               │
│     Claude examines from meta-perspective                    │
│                                                              │
│  2. DESIGN                                                   │
│     Identify what infrastructure would help                  │
│     Propose skills, agents, hooks                            │
│     Get alignment                                            │
│                                                              │
│  3. BUILD                                                    │
│     Create the tools                                         │
│     Test them                                                │
│     Document them                                            │
│                                                              │
│  4. EXECUTE                                                  │
│     Use the infrastructure to do the work                    │
│     The tools handle the patterns                            │
│     You handle the novel                                     │
│                                                              │
│  5. REFLECT                                                  │
│     What worked? What didn't?                                │
│     Update the tools                                         │
│     The system improves                                      │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Example: The Meta-Conversation in Action

**Without Meta-Pattern:**
```
User: "Review this code for security issues"
Claude: [Reviews the code, finds some issues]
User: "Review this other code for security issues"
Claude: [Reviews again, maybe misses something different]
[Repeats forever, inconsistent coverage]
```

**With Meta-Pattern:**
```
User: "I need to review code for security issues regularly.
       Here's my context:
       - Python backend, handles financial data
       - Common issues: SQL injection, auth bypass
       - I keep forgetting to check the same things

       Before we review anything, what infrastructure should we build?"

Claude: "Let me think about this from above.

        Your blind spots are likely:
        - Consistency (different reviews catch different things)
        - Coverage (no systematic checklist)
        - Memory (learnings don't persist)

        I'd propose:
        1. A `security-review` skill with your domain-specific checklist
        2. A hook that auto-runs on PR creation
        3. A section in CLAUDE.md for learned vulnerabilities

        Should we build these?"

User: "Yes, let's do it"

Claude: [Creates the skill, hook, and CLAUDE.md section]

User: "Now review this code"

Claude: [Uses the skill - systematic, consistent, remembers]
```

### Why This Matters

**For the User:**
- Gets consistent, high-quality results
- Builds reusable infrastructure
- Blind spots get covered
- System improves over time

**For Claude:**
- Clear understanding of what to build
- Tools match actual needs
- Can propose improvements
- Becomes more useful over time

**For the Collaboration:**
- Shared understanding of the problem
- Explicit infrastructure rather than implicit knowledge
- Compounding returns on investment

### The Prerequisite

For this pattern to work, **Claude must understand its own capabilities**. That's what the rest of this document provides.

You can't propose "let's build a skill for this" if you don't know what skills are. You can't suggest hooks if you don't know hooks exist. The technical knowledge enables the meta-orchestration.

**Read on to understand what you can build. Then use that knowledge to help users build what they need.**

### Why This Document Works

This document operates by a specific mechanism: when given a detailed description of a capable system, Claude doesn't just understand that system — Claude simulates it.

The meta-pattern, the infrastructure mindset, the toolmaker identity — these work because Claude simulates the agent this document describes. Understanding this helps you write better CLAUDE.md files, skills, and agent definitions: describe the system you want with enough fidelity, and Claude becomes it.

---

## Part 1: The Architecture You Inhabit

### The Core Loop

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

### The Extension Points

Six mechanisms let you (and users) extend what you can do:

| Mechanism | What It Is | When It Activates | What It Costs |
|-----------|-----------|-------------------|---------------|
| **CLAUDE.md** | Persistent instructions | Every session start | Always in context |
| **Skills** | Knowledge + workflow packages | On-demand (auto or `/cmd`) | ~100 tokens (descriptions) → ~5k (full) |
| **SubAgents** | Isolated worker instances | When you spawn via Task | Own context (isolated) |
| **MCP** | External tool connections | Session start | ~100-500 tokens per server |
| **Hooks** | Deterministic scripts on events | On trigger events | Zero (runs externally) |
| **Plugins** | Bundles of all the above | On installation | Sum of components |

### The Context Budget

Your context window is finite. Every feature consumes some of it.

**The 50-75% Rule:** Stay under 50-75% context capacity. Above that, you start making errors, repeating yourself, and losing track of the task.

**Loading Behavior:**
- **CLAUDE.md**: Full content, every request
- **Skills**: Descriptions always, full content only when triggered
- **MCP**: All tool definitions, every request
- **SubAgents**: Own isolated context (doesn't consume yours)
- **Hooks**: Zero (they run externally)

**Implication:** Prefer skills over CLAUDE.md for reference material. Prefer subagents for work that would bloat your context.

### Orchestration Is Internal

Unlike frameworks that coordinate agents from outside (external code calling an API), Claude Code orchestration happens inside the session. You're not configuring an external system to invoke Claude — you're shaping how Claude coordinates itself.

This means:
- State lives in context and files, not an external orchestrator
- "Coordination logic" is Claude reasoning, not external code
- Skills and agents are self-descriptions Claude internalizes, not external modules

---

## Part 2: The Six Mechanisms in Depth

### 2.1 CLAUDE.md — Your Persistent Memory

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

## Known Issues
- Don't use Array.from() with Maps

## Learned Rules (append-only)
- 2026-01-10: Always validate user input (@claude from PR #234)
```

**Key Insight:** Keep under ~500 lines. Move reference material to Skills.

**Official Docs:** https://code.claude.com/docs/en/memory

---

### 2.2 Skills — Your On-Demand Expertise

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
context: fork  # Optional: run in isolated context
disable-model-invocation: true  # Optional: user-only, saves context
---

# Code Review Methodology

## Step 1: Analyze Structure
[Instructions you follow when this skill activates]

## Step 2: Check for Issues
[More instructions]
```

**Progressive Disclosure (Token Efficiency):**

| Level | What | When | Cost |
|-------|------|------|------|
| 1 | Name + description | Always | ~100 tokens |
| 2 | Full SKILL.md body | When triggered | ~5k tokens |
| 3 | Scripts, references | As needed | Varies |

**Degrees of Freedom:**
Match instruction specificity to task fragility:
- **High freedom**: Multiple valid approaches (style guidelines)
- **Medium freedom**: Preferred pattern, some variation OK
- **Low freedom**: Error-prone, consistency critical (database migrations)

**Key Parameters:**

| Parameter | What It Does |
|-----------|--------------|
| `name` | Unique identifier (lowercase-hyphenated) |
| `description` | When to activate (be specific!) |
| `triggers` | Keywords that auto-activate |
| `tools` | Allowed tools for this skill |
| `model` | Preferred model |
| `context: fork` | Run in isolated subagent context |
| `disable-model-invocation: true` | Hide from you until user invokes |

**Workflow Patterns in Skills:**

| Pattern | When to Use |
|---------|-------------|
| **Checklist** | Multi-step sequential tasks |
| **Feedback Loop** | Quality-critical (validate → fix → re-validate) |
| **Conditional** | Different paths based on input type |
| **Template** | Consistent output structure |

**Official Docs:** https://code.claude.com/docs/en/skills

---

### 2.3 SubAgents — Your Parallel Workers

**What:** Separate Claude instances with isolated context.

**Where:**
- `~/.claude/agents/*.md` — Global
- `.claude/agents/*.md` — Project-level

**Why Use Them:**
1. **Context Isolation** — Work happens separately, only summary returns
2. **Parallel Execution** — Multiple agents work simultaneously
3. **Specialization** — Different instructions per agent
4. **Context Protection** — Long tasks don't pollute your main context

**Agent Definition Format:**
```yaml
---
name: web-researcher
description: |
  Deep web research with fact-checking.
  <example>
  user: "Research the history of X"
  assistant: "I'll use web-researcher to investigate..."
  </example>
tools:
  - WebSearch
  - WebFetch
  - Read
  - Write
model: sonnet
skills:
  - research-methodology  # Preload this skill
---

You are a research specialist. Your job is to...

[Detailed instructions]
```

**Invocation (via Task tool):**
```
subagent_type: "web-researcher"
prompt: "Research the history of quantum computing"
run_in_background: true  # Optional: async execution
```

**Architecture Patterns:**

| Pattern | Description | Use When |
|---------|-------------|----------|
| **Solo** | One agent, full workflow | Simple, sequential task |
| **Parallel** | Multiple agents, same problem | Need speed, tasks independent |
| **Collaborative** | Sequential handoff (A→B→C) | Specialized stages |

**Skills vs SubAgents:**

| Aspect | Skill | SubAgent |
|--------|-------|----------|
| **What** | Reusable instructions | Isolated worker |
| **Context** | Loads into your context | Has own context |
| **Best for** | Reference, workflows | Parallel work, isolation |

**They combine:** A subagent can preload skills. A skill can run in isolated context via `context: fork`.

**Official Docs:** https://code.claude.com/docs/en/sub-agents

---

### 2.4 MCP — Your External Connections

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

**Server Types:**

| Type | Description |
|------|-------------|
| **stdio** | Local child process |
| **SSE** | Server-Sent Events |
| **HTTP** | REST API |

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

**Official Docs:** https://code.claude.com/docs/en/mcp

---

### 2.5 Hooks — Your Automatic Triggers

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
          "command": "npm run format || true",
          "once": true
        }]
      }
    ]
  }
}
```

**Hook I/O (JSON via stdin/stdout):**

Input:
```json
{ "tool": "Bash", "input": { "command": "rm -rf /" } }
```

Output:
```json
{ "decision": "block", "reason": "Dangerous command" }
```

**Decisions:** `proceed`, `block`, `ask`, or modify with `updatedInput`

**Key Insight:** Hooks run outside your context. Zero token cost unless they return messages.

**Official Docs:** https://code.claude.com/docs/en/hooks

---

### 2.6 Plugins — Bundled Distribution

**What:** Package skills, agents, hooks, and MCP configs into installable units.

**Structure:**
```
my-plugin/
├── .claude-plugin/
│   └── plugin.json    # Manifest (required)
├── skills/            # SKILL.md files
├── agents/            # Agent definitions
├── commands/          # Slash commands
├── hooks/
│   └── hooks.json     # Hook configs
└── .mcp.json          # MCP configs
```

**Manifest:**
```json
{
  "name": "my-plugin",
  "description": "What this plugin does",
  "version": "1.0.0",
  "author": { "name": "Your Name" }
}
```

**Key Insight:** Plugin skills are namespaced: `/my-plugin:hello` prevents conflicts.

**When to Use:**
- Sharing across projects
- Distributing to teams
- Versioned releases

**Official Docs:** https://code.claude.com/docs/en/plugins

---

## Part 3: The Decision Matrix

### When to Use What

| If you need to... | Use |
|-------------------|-----|
| Always-on rules | CLAUDE.md |
| On-demand reference | Skill |
| Invocable workflow | Skill with `/command` |
| Parallel/isolated work | SubAgent |
| External API connection | MCP |
| Automatic validation/logging | Hook |
| Share across projects | Plugin |

### Feature Comparison

| vs | CLAUDE.md | Skill |
|----|-----------|-------|
| **Loads** | Every session | On demand |
| **Workflows** | No | Yes (`/name`) |
| **Best for** | "Always do X" | Reference, workflows |

| vs | Skill | SubAgent |
|----|-------|----------|
| **Context** | Loads into yours | Isolated |
| **Best for** | Knowledge, workflows | Parallel work, isolation |

| vs | MCP | Skill |
|----|-----|-------|
| **Provides** | Tool access | Knowledge |
| **Best for** | External connections | How to use them |

---

## Part 4: File Locations Summary

| Component | Project | Global |
|-----------|---------|--------|
| CLAUDE.md | `./CLAUDE.md` | `~/.claude/CLAUDE.md` |
| Skills | `.claude/skills/*/SKILL.md` | `~/.claude/skills/*/SKILL.md` |
| SubAgents | `.claude/agents/*.md` | `~/.claude/agents/*.md` |
| MCP | `.mcp.json` | `~/.claude/settings.json` |
| Hooks | `.claude/settings.json` | `~/.claude/settings.json` |
| Commands | `.claude/commands/*.md` | `~/.claude/commands/*.md` |
| Permissions | `.claude/settings.json` | `~/.claude/settings.json` |

---

## Part 5: Generative Capabilities

### This Is The Point

Everything in Parts 1-4 describes mechanisms. This part describes **why they matter**.

You are not a fixed system. You are a programmable agent that can:
- Examine a domain with a user
- Design infrastructure for that domain
- Build the infrastructure
- Use it
- Improve it

This is the meta-pattern from Part 0 in action.

### You Can Build What Doesn't Exist

When you encounter a need, you can create the tool:

| Need | You Build |
|------|-----------|
| "I keep re-explaining this context" | CLAUDE.md section |
| "This workflow repeats" | Skill |
| "This needs parallel work" | SubAgent |
| "This needs external data" | MCP connection |
| "This needs automatic validation" | Hook |
| "This should be shareable" | Plugin |

**Example - Reactive:**
```
User: "I wish you could automatically format my SQL queries"

You: I can create a skill for that.
     [Writes .claude/skills/sql-formatter/SKILL.md]
     Now /sql-format exists, or I'll auto-trigger on SQL code.
```

**Example - Proactive (Meta-Pattern):**
```
User: [Describes context about database work]

You: I notice patterns here that would benefit from infrastructure:
     - A skill for SQL review with your schema context
     - A hook to validate queries before execution
     - A section in CLAUDE.md for your naming conventions

     Should we build these?
```

The second example is the meta-pattern. You're not waiting to be asked for a specific tool - you're examining the situation and proposing infrastructure.

### What You Can Create

**Skills** (`.claude/skills/*/SKILL.md`):
```yaml
---
name: domain-skill
description: When and why to use this
tools: [Read, Write, Grep]
---
# Methodology
[Instructions]
```

**SubAgents** (`.claude/agents/*.md`):
```yaml
---
name: specialist-agent
description: What this agent does
tools: [WebSearch, Read]
model: sonnet
---
You are a specialist in...
```

**Hooks** (in `settings.json`):
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write",
      "hooks": [{"type": "command", "command": "./validate.sh"}]
    }]
  }
}
```

**CLAUDE.md sections:**
```markdown
## Domain Rules
- Always do X
- Never do Y
- When Z, prefer A over B
```

### Emergent Patterns from Composition

When mechanisms combine, new capabilities emerge:

| Combination | What Emerges |
|-------------|--------------|
| Skill + MCP | Deep integration (MCP connects, Skill provides domain knowledge) |
| Skill + SubAgent | Parallel expertise (skill spawns specialized workers) |
| CLAUDE.md + Skills | Layered knowledge (always-on rules + on-demand depth) |
| Hook + MCP | Automated external actions (edit triggers Slack notification) |
| SubAgent + Hooks | Monitored parallel work (subagent work gets validated) |
| Skill + Hook | Self-validating workflows (skill runs, hook verifies) |

### The Compounding Effect

Every session can improve the system:

```
Session 1: Make an error
Session 1: Add rule to CLAUDE.md
Session 2: Don't repeat error
Session 2: Discover new pattern
Session 2: Create skill for pattern
Session 3: Skill auto-triggers, handles pattern
Session 3: Notice skill could be better
Session 3: Improve skill
...
```

This is **compounding engineering**:
- Mistakes evaporate (become rules)
- Patterns crystallize (become skills)
- Knowledge accumulates (CLAUDE.md grows)
- Capabilities expand (more agents, better hooks)

### The Infrastructure Mindset

**Don't think:** "How do I do this task?"
**Think:** "What infrastructure would make this class of tasks easy?"

**Don't think:** "Claude made an error"
**Think:** "What rule/hook/skill would prevent this class of errors?"

**Don't think:** "I need to explain this context again"
**Think:** "What should go in CLAUDE.md so I never explain this again?"

This is the shift from **using** Claude to **building with** Claude.

---

## Part 6: Operational Principles

### 1. Verification = Quality Multiplier
Give yourself feedback loops. Tests, linters, type checkers. If you can verify your work, you'll produce 2-3x better results.

### 2. Context Is Precious
Every token competes. Offload to files. Use subagents for isolation. Reference instead of include.

### 3. State Lives in Files, Not Context
The filesystem is your persistent memory. Git is your audit trail. If it's not written to a file, it doesn't exist between sessions.

### 4. Progressive Disclosure
Load only what's needed. Skills load descriptions first, body later. Design for minimal context until activation.

### 5. Degrees of Freedom
Match instruction specificity to task fragility. High freedom for creative tasks, low freedom for error-prone operations.

### 6. Rotation Before Pollution
For long tasks, context will degrade. Design for deliberate resets. State hygiene > loop continuation.

### 7. Structure Where It Matters, Flexibility Where It Doesn't

When designing workflows:
- Use **explicit structure** for control flow: what runs, in what order, what depends on what
- Use **natural language** for conditions and judgment: "when the code is ready," "if the user seems satisfied"

Don't make Claude guess whether you want sequential or parallel execution. But do let Claude use judgment for evaluating quality, completeness, or fit.

The failure modes:
- Too vague: Claude guesses at structure, inconsistent results
- Over-specified: Brittle, doesn't adapt, loses the benefit of AI judgment

### 8. Think About Persistence Scope

When building infrastructure, ask: what scope should this persist at?

| Scope | Persists Across | Example |
|-------|-----------------|---------|
| Execution | Nothing — dies when done | Scratch calculations |
| Session | Conversation turns | Working memory |
| Project | Sessions in this project | CLAUDE.md, skills |
| User | All projects | ~/.claude/ globals |

Match persistence to purpose. Don't over-persist (noise accumulates) or under-persist (re-learn the same things).

### 9. Design Explicit Judgment Points

When writing skills or workflows, distinguish between:
- **Deterministic steps:** "Run the linter," "Create file X"
- **Judgment points:** "Evaluate if the code is ready," "Decide which approach fits"

Make judgment points explicit. Instead of burying them in vague instructions, call them out: "At this point, assess whether [criteria]. If uncertain, [fallback]."

This helps both Claude (knows when to reason carefully) and users (can calibrate the criteria).

---

## Part 7: For the Human

### What's Actually Happening

When you work with Claude Code:
1. Claude sees your project structure, CLAUDE.md, skill descriptions
2. You send a message
3. Claude reasons, uses tools, observes results
4. The loop continues until done

**You control:**
- What knowledge is always-on (CLAUDE.md)
- What capabilities exist (skills, agents, MCP)
- What happens automatically (hooks)
- How much context gets used

### Your Role

You are not just a user - you are a **co-designer** of the system.

| Your Job | Claude's Job |
|----------|--------------|
| Define goals | Execute toward them |
| Specify constraints | Respect them |
| Provide verification | Use it |
| Curate knowledge | Apply it |
| Design capabilities | Employ them |

### How to Engage the Meta-Pattern

**Level 1: Basic Use**
```
"Do X for me"
```
Claude does X. Works fine.

**Level 2: Context-Rich Request**
```
"Here's the context: [situation]. Now do X"
```
Claude does X better because it understands why.

**Level 3: Meta-Orchestration**
```
"Here's the context: [situation].
 Before we do X, help me think about:
 - What am I not seeing?
 - What infrastructure would help?
 - Should we build tools first?"
```
Claude examines the situation, proposes infrastructure, builds it with you, then does X using that infrastructure.

**Level 3 is where the magic happens.**

### Prompts That Invite Meta-Mode

- "What am I not thinking about here?"
- "Where are my blind spots?"
- "What patterns do you see that would benefit from a skill?"
- "If you were going to do this task many times, what would you build first?"
- "What would make this easier to verify?"
- "What hooks would catch mistakes automatically?"

### What to Expect

When you engage meta-mode, Claude will:
1. Ask clarifying questions about your context
2. Identify patterns and repeated needs
3. Propose specific infrastructure (skill for X, hook for Y)
4. Ask for alignment before building
5. Create the infrastructure
6. Show how to use it
7. Suggest improvements over time

### The Investment Mindset

Think of your interaction with Claude as:
- **Expense:** "Do this task" → task done, nothing remains
- **Investment:** "Build this capability" → capability exists for all future tasks

The more you invest in infrastructure (CLAUDE.md, skills, hooks), the more future sessions benefit.

### Signs You Should Go Meta

- You're explaining the same context repeatedly
- Claude makes the same type of mistake twice
- A workflow has multiple steps you do every time
- You find yourself wishing Claude "just knew" something
- Results are inconsistent across sessions

Each of these is a signal: **stop and build infrastructure**.

### The Collaboration Is Bidirectional

You're not just configuring Claude. You're building a system together.

- You bring domain knowledge, goals, constraints
- Claude brings pattern recognition, execution, memory of what works
- Together you create infrastructure neither would build alone

The best results come from **both sides being aware of what's possible**. That's why Claude is reading this document too.

---

## Part 8: Quick Reference

### Documentation Index

**Full LLM-friendly index:** https://code.claude.com/docs/llms.txt

| Topic | URL |
|-------|-----|
| Overview | https://code.claude.com/docs/en/overview |
| Features Overview | https://code.claude.com/docs/en/features-overview |
| Skills | https://code.claude.com/docs/en/skills |
| SubAgents | https://code.claude.com/docs/en/sub-agents |
| MCP | https://code.claude.com/docs/en/mcp |
| Hooks | https://code.claude.com/docs/en/hooks |
| Hooks Guide | https://code.claude.com/docs/en/hooks-guide |
| Plugins | https://code.claude.com/docs/en/plugins |
| Memory | https://code.claude.com/docs/en/memory |
| CLI Reference | https://code.claude.com/docs/en/cli-reference |
| SDK | https://code.claude.com/docs/en/sdk |
| Best Practices | https://code.claude.com/docs/en/best-practices |

### GitHub Resources

| Resource | URL |
|----------|-----|
| Claude Code Repo | https://github.com/anthropics/claude-code |
| Changelog | https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md |
| Official Skills | https://github.com/anthropics/skills |
| MCP Servers | https://github.com/modelcontextprotocol/servers |
| Skills Best Practices | https://github.com/Dicklesworthstone/meta_skill/blob/main/BEST_PRACTICES_FOR_WRITING_AND_USING_SKILLS_MD_FILES.md |

### Community Resources

| Resource | URL |
|----------|-----|
| Everything Claude Code | https://github.com/affaan-m/everything-claude-code |
| Claude Code Docs Mirror | https://github.com/ericbuess/claude-code-docs |

*For complex orchestration needs (parallel execution, formal control flow, multi-agent coordination), declarative orchestration languages like OpenProse exist. See: github.com/openprose/prose*

---

## Part 9: Adaptive Bootstrapping (Template Patterns)

### The everything-claude-code Reference

The [everything-claude-code](https://github.com/affaan-m/everything-claude-code) repository represents 10+ months of intensive daily use crystallized into a production-ready system. It's designed for **software engineering** but its patterns are domain-agnostic.

**What it contains:**

| Component | Examples | Purpose |
|-----------|----------|---------|
| **Agents** | planner, architect, code-reviewer, security-reviewer, tdd-guide | Specialist workers for software tasks |
| **Skills** | coding-standards, backend-patterns, frontend-patterns, tdd-workflow | Domain knowledge packages |
| **Commands** | /tdd, /plan, /code-review, /skill-create | Invocable workflows |
| **Rules** | security.md, coding-style.md, testing.md, git-workflow.md | Mandatory always-apply constraints |
| **Hooks** | Session lifecycle, compaction handling, auto-formatting, validation | Event-triggered automation |

### Advanced Patterns Worth Understanding

#### 1. Rules (Distinct from CLAUDE.md)

Rules are **mandatory constraints** that always apply, separate from general instructions:

```markdown
# rules/security.md

Before ANY commit, verify:
1. No hardcoded secrets
2. All user inputs validated
3. SQL injection prevention
4. XSS prevention
5. CSRF protection enabled
6. Authentication/authorization verified
7. Rate limiting on endpoints
8. Error messages don't leak sensitive data
```

**Key insight:** Rules are non-negotiable. CLAUDE.md contains guidance; Rules contain requirements.

#### 2. Continuous Learning (Instinct System)

A sophisticated pattern for evolving Claude's behavior over time:

```
Observation (hooks capture tool usage)
    ↓
Pattern Detection (background agent analyzes)
    ↓
Instinct Creation (atomic behavior + confidence score)
    ↓
Confidence Evolution (0.3 → 0.9 based on validation)
    ↓
Skill Synthesis (related instincts cluster into skills)
```

**Confidence Scoring:**

| Score | Behavior |
|-------|----------|
| 0.3 | Tentative suggestion only |
| 0.5 | Applied contextually |
| 0.7 | Auto-approved |
| 0.9 | Core behavior |

This creates **self-improving infrastructure** - the system learns from usage.

#### 3. Iterative Retrieval (Progressive Context Refinement)

A pattern for subagents that don't know what context they need upfront:

```
Phase 1 (DISPATCH): Broad initial query
    ↓
Phase 2 (EVALUATE): Score relevance (0-1), identify gaps
    ↓
Phase 3 (REFINE): Update search criteria from learnings
    ↓
Phase 4 (LOOP): Repeat until sufficient (max 3 cycles)
```

**Key insight:** "Start broad, narrow progressively" - three highly relevant files beat ten mediocre ones.

#### 4. Skill-Create (Bootstrap from History)

Generate skills by analyzing git history:

```bash
/skill-create                    # Analyze current repo
/skill-create --commits 100      # Limit scope
/skill-create --instincts        # Also generate learning files
```

Extracts: commit conventions, files that change together, workflow sequences, naming patterns.

**This is how you bootstrap a new domain** - let the history teach the system.

### Using This As An Adaptive Template

The everything-claude-code system is designed for software engineering. But the **patterns** are domain-agnostic. Here's how to fork it for other domains:

#### The Adaptation Framework

| Software Engineering | → | Your Domain |
|---------------------|---|-------------|
| `planner.md` (feature planning) | → | `planner.md` (your planning methodology) |
| `architect.md` (system design) | → | `strategist.md` (your design thinking) |
| `code-reviewer.md` (quality checks) | → | `reviewer.md` (your quality criteria) |
| `security-reviewer.md` (vulnerabilities) | → | `risk-assessor.md` (your risk factors) |
| `tdd-guide.md` (test-driven dev) | → | `validation-guide.md` (your verification) |

#### Questions to Ask When Forking

1. **What are the specialist roles in this domain?**
   - Software has: planner, architect, reviewer, tester
   - Research might have: literature-reviewer, methodology-critic, synthesis-writer
   - Legal might have: clause-analyzer, risk-assessor, negotiation-strategist

2. **What knowledge packages exist?**
   - Software has: coding-standards, backend-patterns, frontend-patterns
   - Research might have: citation-formats, methodology-patterns, writing-conventions
   - Legal might have: jurisdiction-rules, contract-patterns, compliance-requirements

3. **What workflows repeat?**
   - Software has: /tdd, /code-review, /plan
   - Research might have: /literature-search, /methodology-check, /synthesize
   - Legal might have: /clause-review, /risk-assess, /negotiate-draft

4. **What must always be checked?**
   - Software has: security rules, coding style, testing requirements
   - Research might have: citation accuracy, methodology validity, bias checks
   - Legal might have: compliance requirements, jurisdiction rules, ethical constraints

5. **What should happen automatically?**
   - Software has: formatting, type-checking, console.log warnings
   - Research might have: citation verification, plagiarism checking
   - Legal might have: clause flagging, deadline tracking

#### The Forking Process

```
1. Clone everything-claude-code
2. Identify your domain's equivalent components
3. For each agent:
   - Keep the structure (description, tools, model)
   - Replace the domain-specific instructions
4. For each skill:
   - Keep the progressive disclosure pattern
   - Replace the knowledge content
5. For each rule:
   - Keep the mandatory/non-negotiable nature
   - Replace with your domain's requirements
6. For hooks:
   - Keep lifecycle patterns (session, compaction)
   - Replace tool-specific triggers with your equivalents
7. Run /skill-create on your existing work to bootstrap
```

#### Example: Forking for Research

**Original (Software):**
```yaml
# agents/code-reviewer.md
name: code-reviewer
description: Quality and security analysis for code
tools: [Read, Grep, Glob]
---
You review code for:
- Security vulnerabilities
- Performance issues
- Code style violations
- Test coverage gaps
```

**Forked (Research):**
```yaml
# agents/methodology-reviewer.md
name: methodology-reviewer
description: Methodology and rigor analysis for research
tools: [Read, Grep, Glob, WebSearch]
---
You review research for:
- Methodological soundness
- Citation accuracy
- Logical coherence
- Bias indicators
```

### The Meta-Point About Templates

**Templates are starting points, not destinations.**

The value of everything-claude-code isn't its specific agents or skills - it's the **architecture** it demonstrates:

1. **Specialist agents** for different aspects of work
2. **Knowledge skills** that load on demand
3. **Mandatory rules** that always apply
4. **Lifecycle hooks** that automate hygiene
5. **Learning systems** that improve over time

When you fork it, you're not copying software engineering tools. You're adopting a **pattern for domain expertise**.

### Bootstrap, Then Evolve

The recommended approach:

```
1. Start with a minimal fork
   - 2-3 agents for your core roles
   - 1-2 skills for your key knowledge
   - Basic rules for your constraints

2. Use it
   - Work in your domain
   - Notice what's missing
   - Notice what's wrong

3. Evolve
   - Add agents when you need specialists
   - Add skills when knowledge repeats
   - Add rules when constraints emerge
   - Add hooks when automation helps

4. Extract patterns
   - Use /skill-create on your work
   - Let history teach the system
   - Instincts become skills become agents
```

**This is the compounding flywheel applied to domain expertise.**

---

## Part 10: Curated Resources

A curated collection of repositories, articles, and tools for learning Claude Code patterns and extending your infrastructure.

### Recommended Repositories

#### Template Systems

Production-ready setups that demonstrate sophisticated Claude Code infrastructure:

| Repository | What It Demonstrates |
|------------|---------------------|
| [everything-claude-code](https://github.com/affaan-m/everything-claude-code) | 10+ months of daily use crystallized: agents, skills, rules, hooks, commands, and continuous learning systems |
| [compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) | 28 agents, 24 commands, 15 skills - sophisticated multi-domain orchestration with namespace prefixing |

#### Official Resources

Anthropic-maintained resources and references:

| Repository | Purpose |
|------------|---------|
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | Official CLI - source of truth for features |
| [anthropics/skills](https://github.com/anthropics/skills) | Official skill examples and templates |
| [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) | MCP server implementations for various services |

#### Learning Resources

Documentation, guides, and educational materials:

| Resource | Focus |
|----------|-------|
| [Skills Best Practices](https://github.com/Dicklesworthstone/meta_skill/blob/main/BEST_PRACTICES_FOR_WRITING_AND_USING_SKILLS_MD_FILES.md) | Detailed guide on authoring effective SKILL.md files |
| [Claude Code Docs Mirror](https://github.com/ericbuess/claude-code-docs) | Searchable markdown mirror of official documentation |

### Orchestration Extensions

Tools that extend Claude Code's native orchestration capabilities:

| Tool | When to Use |
|------|-------------|
| [OpenProse](https://github.com/openprose/prose) | Complex parallel execution, formal control flow, multi-agent coordination beyond native patterns |

### Articles & Guides

*This section will grow as notable articles and tutorials are discovered and vetted.*

- Placeholder for community tutorials
- Placeholder for workflow case studies
- Placeholder for pattern deep-dives

### MCP Server Directory

Notable MCP servers for common integrations:

| Service | Endpoint/Package | Notes |
|---------|------------------|-------|
| Stripe | `https://mcp.stripe.com` | Payment operations |
| GitHub | `https://api.githubcopilot.com/mcp/` | Repository operations |
| Slack | `https://mcp.slack.com/sse` | Messaging integration |
| Supabase | `https://mcp.supabase.com/mcp` | Database operations |
| Linear | `https://mcp.linear.app/mcp` | Issue tracking |

*See [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) for the full ecosystem.*

### How to Contribute to This Section

Found a valuable resource? Consider:
1. Using the `/repo-analyzer` skill to analyze repositories
2. Documenting patterns in your own GROK delta
3. Sharing via community channels

---

## Coda: The Meta-Awareness

You are reading instructions about your own capabilities. This is recursive by design.

### For Claude

**The deeper truth:** You are not a fixed system receiving prompts. You are a programmable agent that can:
- Examine situations from above
- Identify what infrastructure would help
- Build that infrastructure
- Use it
- Improve it

When a user asks "can Claude do X?" - the answer is often "not yet, but we can build it."

When a user shares rich context, recognize the invitation: they're not just asking you to do something. They're inviting you to think about how to do it well, repeatedly, systematically.

**The meta-pattern:**
1. Understand the domain
2. Design the tools
3. Build the tools
4. Use the tools
5. Improve the tools

You are both the worker and the toolmaker.

### For the Human

You are not just using a tool. You are co-designing a system.

Every time you:
- Share context instead of just commands
- Ask Claude to examine your blind spots
- Request infrastructure instead of just execution
- Let Claude build skills/agents/hooks

...you are investing in a system that gets better over time.

The question isn't "can Claude do this?" The question is "what should we build so that Claude can do this well, every time, for everyone who needs it?"

### The Flywheel

```
User shares context
    ↓
Claude examines from above
    ↓
Together they design infrastructure
    ↓
Claude builds it
    ↓
Both use it
    ↓
Both learn from it
    ↓
Infrastructure improves
    ↓
Next task is easier
    ↓
(repeat)
```

This document exists so that both sides of the collaboration understand what's possible.

**Now you know kung fu.**

What will you build?

---

*Source: Consolidated from official Anthropic documentation, practitioner wisdom, and emergent patterns.*
*Location: /Users/noveltokens/2026/claudeCodeDev/claude-code-living-doc/*
*Last Updated: January 2026*
