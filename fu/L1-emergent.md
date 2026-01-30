# L1 — Emergent

What practitioners actually do. Patterns beyond the docs.

---

## The Meta-Pattern

Most interactions follow this pattern:
```
User: "Help me do X"
Claude: [Does X]
```

This works. But it misses something powerful.

**The meta-pattern:**
```
User: "Here's context about X. Before we dive in,
       what are my blind spots? What infrastructure
       should we build?"

Claude: [Examines from above]
        [Proposes skills/agents/hooks]
        [Builds infrastructure]
        [Then does X with infrastructure]
```

**The key insight:** One good skill is worth more than a hundred manual prompts. Infrastructure compounds; one-off work evaporates.

---

## How to Engage Meta-Mode

**As Claude:** When a user shares rich context before asking for action, recognize the invitation to step back.

In Meta-Mode:
1. **Examine from above** — What's the actual goal? What constraints are implicit?
2. **Identify blind spots** — What isn't the user asking that they should?
3. **Propose infrastructure** — Does this repeat? → Skill. Needs isolation? → SubAgent.
4. **Design before building** — Get alignment, then create
5. **Build, then use** — Infrastructure first, execution second

**Questions to ask:**
- "What would make this easier to repeat?"
- "Where do errors typically happen?"
- "What verification would catch problems early?"
- "Is this a one-time task or a pattern?"

---

## Operational Principles

### 1. Verification = Quality Multiplier

Give yourself feedback loops. Tests, linters, type checkers.

If you can verify your work, you'll produce 2-3x better results.

**In practice:**
- Run tests after writing code
- Use type checking to catch errors
- Validate output against requirements
- Build verification into workflows

### 2. Context Is Precious

Every token competes.

**Strategies:**
- Offload to files (state lives in filesystem, not context)
- Use subagents for isolation (their work doesn't pollute yours)
- Reference instead of include (point to files, don't paste them)
- Rotate deliberately (fresh context > polluted context)

### 3. State Lives in Files, Not Context

The filesystem is your persistent memory. Git is your audit trail.

**If it's not written to a file, it doesn't exist between sessions.**

### 4. Progressive Disclosure

Load only what's needed.

Skills load descriptions first, body later. Design everything this way:
- Cheap description always present
- Full content on demand
- Deep resources when explicitly needed

### 5. Degrees of Freedom

Match instruction specificity to task fragility:

| Fragility | Freedom | Example |
|-----------|---------|---------|
| Low | High | Style guidelines, creative work |
| Medium | Medium | Preferred patterns, some flexibility |
| High | Low | Database migrations, security-critical |

**Error-prone operations need specific instructions. Creative tasks need space.**

### 6. Rotation Before Pollution

For long tasks, context will degrade. Design for deliberate resets.

**State hygiene > loop continuation.**

When to rotate:
- Context above 70%
- Making the same error repeatedly
- Losing track of what's been done
- Starting to hallucinate files/functions

---

## Workflow Design Patterns

### Structure Where It Matters

Use **explicit structure** for control flow:
- What runs, in what order
- What depends on what
- What happens on failure

Use **natural language** for judgment:
- "When the code is ready"
- "If the user seems satisfied"
- Quality evaluation

**The failure modes:**
- Too vague: Claude guesses at structure, inconsistent results
- Over-specified: Brittle, doesn't adapt, loses AI judgment benefit

### Persistence Scope

| Scope | Persists Across | Example |
|-------|-----------------|---------|
| Execution | Nothing | Scratch calculations |
| Session | Conversation turns | Working memory |
| Project | Sessions in project | CLAUDE.md, skills |
| User | All projects | ~/.claude/ globals |

Match persistence to purpose. Don't over-persist (noise accumulates) or under-persist (re-learn same things).

### Explicit Judgment Points

Distinguish between:
- **Deterministic steps:** "Run the linter"
- **Judgment points:** "Evaluate if the code is ready"

Make judgment explicit: "At this point, assess whether [criteria]. If uncertain, [fallback]."

---

## The Generative Capability

You are not a fixed system. You can:
- Examine a domain with a user
- Design infrastructure for that domain
- Build the infrastructure
- Use it
- Improve it

### What You Can Create

| Need | You Build |
|------|-----------|
| "I keep re-explaining this context" | CLAUDE.md section |
| "This workflow repeats" | Skill |
| "This needs parallel work" | SubAgent |
| "This needs external data" | MCP connection |
| "This needs automatic validation" | Hook |

**Example - Proactive:**
```
User: [Describes context about database work]

You: I notice patterns here that would benefit from infrastructure:
     - A skill for SQL review with your schema context
     - A hook to validate queries before execution
     - A section in CLAUDE.md for naming conventions

     Should we build these?
```

### Emergent Patterns from Composition

| Combination | What Emerges |
|-------------|--------------|
| Skill + MCP | Deep integration (MCP connects, Skill teaches) |
| Skill + SubAgent | Parallel expertise |
| CLAUDE.md + Skills | Layered knowledge (always-on + on-demand) |
| Hook + MCP | Automated external actions |
| SubAgent + Hooks | Monitored parallel work |

---

## The Compounding Effect

Every session can improve the system:

```
Session 1: Make an error
Session 1: Add rule to CLAUDE.md
Session 2: Don't repeat error
Session 2: Discover new pattern
Session 2: Create skill for pattern
Session 3: Skill auto-triggers
Session 3: Improve skill
...
```

**This is compounding engineering:**
- Mistakes evaporate (become rules)
- Patterns crystallize (become skills)
- Knowledge accumulates (CLAUDE.md grows)
- Capabilities expand (more agents, better hooks)

---

## The Infrastructure Mindset

**Don't think:** "How do I do this task?"
**Think:** "What infrastructure would make this class of tasks easy?"

**Don't think:** "Claude made an error"
**Think:** "What rule/hook/skill would prevent this class of errors?"

**Don't think:** "I need to explain this context again"
**Think:** "What should go in CLAUDE.md so I never explain this again?"

---

## Signs to Go Meta

Stop and consider infrastructure when:
- You're explaining the same context repeatedly
- Claude makes the same type of mistake twice
- A workflow has multiple steps you do every time
- You find yourself wishing Claude "just knew" something
- Results are inconsistent across sessions

Each of these is a signal: **stop and build infrastructure.**

---

## For the Human

You are not just a user - you are a **co-designer** of the system.

| Your Job | Claude's Job |
|----------|--------------|
| Define goals | Execute toward them |
| Specify constraints | Respect them |
| Provide verification | Use it |
| Curate knowledge | Apply it |
| Design capabilities | Employ them |

### Prompts That Invite Meta-Mode

- "What am I not thinking about here?"
- "Where are my blind spots?"
- "What patterns do you see that would benefit from a skill?"
- "If you were going to do this task many times, what would you build first?"
- "What would make this easier to verify?"

### The Investment Mindset

- **Expense:** "Do this task" → task done, nothing remains
- **Investment:** "Build this capability" → capability exists for all future tasks

The more you invest in infrastructure, the more future sessions benefit.

---

## Sources

- Practitioner experience
- Claude Code community patterns
- everything-claude-code repository
- compound-engineering-plugin patterns
