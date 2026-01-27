# Practitioner Wisdom: Claude Code in the Wild

*What people on the ground are discovering - captured from 15+ high-signal Twitter threads and blog posts.*

---

## Executive Summary

This document captures practitioner patterns emerging from the Claude Code community. The most striking finding: **multiple independent practitioners are converging on the same conclusions**, suggesting these represent genuine discovered truths rather than opinions.

**Top Sources:**
- Boris Cherny (Creator of Claude Code) - 7.3M views
- @vasuman - Production agents masterclass
- @agrimsingh - Ralph methodology definitive guide
- @mrexodia - "Vibe Engineering" comprehensive guide

---

## Part 1: From the Creator - Boris Cherny's Setup

*7.3M views - Jan 2, 2026*

Boris Cherny, creator of Claude Code, shared his surprisingly "vanilla" setup. Key insight: **Claude Code works great out of the box**.

### Parallel Execution
- Runs **5 Claudes in parallel** in terminal (tabs 1-5)
- Also runs **5-10 Claudes on claude.ai/code** in parallel
- "Teleports back and forth" between local and web sessions
- Uses system notifications to know when Claude needs input

### Model Choice
> "I use Opus 4.5 with thinking for everything. It's the best coding model I've ever used. Even though it's bigger & slower than Sonnet, since you have to steer it less and it's better at tool use, it is almost always faster than using a smaller model in the end."

### Team CLAUDE.md Practice (Compounding Engineering)
- Team shares **single CLAUDE.md** for Claude Code repo - checked into git
- Whole team contributes multiple times a week
- "Anytime we see Claude do something incorrectly we add it to CLAUDE.md"
- During code review: **tag @claude on PRs to add rules**
- Uses Claude Code GitHub Action for this

This is their version of **"Compounding Engineering"** (@danshipper's term) - mistakes evaporate, lessons accumulate.

### Plan Mode Workflow
> "Most sessions start in Plan mode (shift+tab twice). If my goal is to write a Pull Request, I will use Plan mode, and go back and forth with Claude until I like its plan. From there, I switch into auto-accept edits mode and Claude can usually 1-shot it."

### Slash Commands for Inner Loops
- Uses slash commands for every "inner loop" workflow done many times/day
- Commands checked into git in `.claude/commands/`
- Example: `/commit-push-pr` - Commit, push, and open a PR

### Subagents
Uses regularly:
- `code-simplifier` - Simplifies code after Claude is done
- `verify-app` - Detailed end-to-end testing instructions
- `build-validator` - Build validation
- `code-architect` - Architecture decisions
- `oncall-guide` - On-call procedures

### Hooks
**PostToolUse hook** to format code after every Write|Edit:
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

### Permissions (NOT --dangerously-skip-permissions)
Uses `/permissions` to pre-allow safe bash commands, checked into `.claude/settings.json`:
```
Bash(bun run build:*)
Bash(bun run test:*)
Bash(bun run lint:file:*)
Bash(bun run typecheck:*)
```

### Most Important Tip
> **"Give Claude a way to verify its work. If Claude has that feedback loop, it will 2-3x the quality of the final result."**

---

## Part 2: Production Agent Lessons - @vasuman

*521K views - "100x a business with AI"*

From someone running a $3M ARR enterprise agent company. These are lessons from deploying production agents for over a year.

### Lesson 1: Context Is Everything
> "Context is often the biggest difference between an agent worth $1M and an agent worth $0."

Three key areas:
- **What the agent remembers** - Not just current task, but history of what led here
- **How information flows** - Structured input/output at each stage (like Claude Code's /compact)
- **What the agent knows about the domain** - Can't just point at documents

Bad context = agent calls same tool repeatedly because it forgot, contradicts earlier decisions.
Good context = agent operates like someone with domain knowledge.

### Lesson 2: Agents Multiply Outcomes
> WRONG: "This will do the work so we don't have to hire someone"
> RIGHT: "This will let three people do what used to require fifteen"

Agents eliminate friction around human judgment, not judgment itself. "Most of what humans were doing wasn't the valuable part of their job, but overhead to get there."

### Lesson 3: Memory and State - 3 Architectural Patterns

| Pattern | Description | Challenge |
|---------|-------------|-----------|
| **Solo agents** | One agent, complete workflow | Managing state as workflow lengthens |
| **Parallel agents** | Faster, multiple agents same problem | Coordination, conflict resolution |
| **Collaborative agents** | Sequential handoff (A→B→C) | Handoffs are where things break |

> "These are architectural decisions, not implementation schematics."

### Lesson 4: Catch Exceptions
> "Please for the love of god do not create another dashboard. Dashboards are useless."

Agent's job: make problems **impossible to ignore** and **incredibly easy to resolve**.
> "Use AI to force resolution of problems, not create visibility into problems."

### Lesson 5: Economics - AI Agents vs Generic SaaS
- SaaS accumulates **tech debt** (integrations, outdated systems, vendor churn)
- Agents built in-house accumulate **capability** (investment compounds)

> "Most companies purchasing AI SaaS churn within 6 months, see absolutely no productivity gains. Only companies who see AI gains have custom agents built specifically for them."

### Lesson 6: Deploy Time
> "If your AI agent project has a year-long timeline, you've already lost."

Get to production in 3 months max.

> "Context engineers are just prompt engineers 2.0"

**TLDR:** "The technology is ready, you're probably not."

---

## Part 3: The Ralph Methodology - @agrimsingh

*374.7K views - "Ralph for Idiots: The Only Explanation You Need"*

Definitive explanation of the "ralph" methodology gaining traction in the community.

### Core Philosophy
> "Ralph works because it treats AI like a volatile process, not a reliable collaborator."
> "Your progress should persist. Your failures should evaporate."

### What Ralph IS vs ISN'T
- NOT: "an agent that remembers forever"
- IS: "an agent that forgets on purpose"
- Purest form: `while :; do cat prompt.md | agent ; done`
- Memory = filesystem + git, NOT the chat
- "If it's not written to a file, it doesn't exist"

### The Core Problem: Context Pollution
Context window fills with: files read, commands ran, outputs, **wrong turns**, hallucinated plans.

> "You can keep adding, but you can't delete."

Symptoms: repeating itself, "fixing" same bug different ways, circular reasoning.

> **"Once the ball is in the gutter, adding spin doesn't save it."**

Ralph throws away polluted context and starts fresh.

### State Architecture
```
Context (bad for state)     | Files + git (good for state)
--------------------------- | ---------------------------
Dies with convo             | Only what you choose to write
Polluted by dead ends       | Can be rolled back
Memory can drift            | Git doesn't hallucinate
```

### The Anchor File Pattern
Single source-of-truth: `ralph_task.md` with task, test_command, checkboxes.

`.ralph/` directory contains:
- `guardrails.md`: learned constraints ("signs")
- `progress.md`: what's done / next
- `errors.log`: what blew up
- `activity.log`: token tracking

> **"The loop is not the technique. State hygiene is the technique."**

### Critical Insight: Claude Code is "Accidentally Anti-Ralph"
- CC keeps pounding model in single session until context rots
- No visibility into context health
> "Claude code treats context rot as an accident. Ralph treats it as a certainty."

Ralph rotates deliberately BEFORE pollution builds up.

### Guardrails: Kaizen for AI
When something breaks → add "sign" to `guardrails.md`:
```markdown
### sign: check imports before adding
- trigger: adding a new import statement
- instruction: check if import already exists
- added after: iteration 3 (duplicate import broke build)
```

> "Guardrails are append-only. Mistakes evaporate. Lessons accumulate."
> **"Basically kaizen, but for a golden retriever with a soldering iron."**

### When to Use Ralph

| USE RALPH | DON'T USE RALPH |
|-----------|-----------------|
| Specs are crisp | Still deciding what to build |
| Success is machine-verifiable (tests, types) | Taste/judgment matters |
| Bulk execution (CRUD, migrations, porting) | Can't define "done" |

> **"If you can't write checkboxes, you're not ready to loop. You're ready to think."**

---

## Part 4: Vibe Engineering - @mrexodia

*149.9K views - "What I've Learned Working with AI Coding Agents"*

Comprehensive practitioner guide from months of full-time agent work.

### Core Philosophy
> "The model is like a genius intern with amnesia. It works at 100x speed but has zero long-term memory."
> "Code is now extremely cheap."

### Agents Are Just Loops
Simon Willison's definition: "An agent runs tools in a loop to achieve a goal"
> "From an engineering perspective, these agents are really lame. It's literally just a for loop. But that's actually nice, because it means these systems aren't magic."

### Context Window Is Precious
> **Stay under 50-75% capacity** - above that, hallucinations start.

- "What even is in my context?" - current tooling terrible at answering this
- GitHub Copilot puts 30,000 tokens by default - 15% gone before you start
- Geoffrey Huntley's Commodore 64 comparison - 200-500KB to work with
> "Compaction = basically death for your useful assistant"

### The Great Decoupling (Gemini's term)
Decouple **programming** (typing code) from **engineering** (architecture, goals, "why").
> "You can suddenly use all programming languages instead of just ones you're familiar with."

But LLMs cannot answer: How do components fit? Does this provide value?

### "You Just Got Promoted"
New title: **Tech Lead + QA Lead**

Write specs, plans, examples. Define "done", how to test. Review outcomes, not lines of code.
> Hardest part: **letting go of details, trusting system with precious code**

### Stop Fighting the Model
Signs of fighting:
- "That's not how I would do it" → stop
- Fixing formatting by hand
- Reviewing every single line of code

> **"You could have thirty agents working for you simultaneously. You cannot watch all of them."**

Better: write better harness, tests, linter rules. Wrong approach = bad plan. Delete, articulate better, try again.

> "That's why when people say 'AI makes me slower' - it's because they're making themselves a bottleneck."

### Project Setup Is Everything
**Hard requirement**: build, test, lint with single command.
- Print minimal, actionable error messages (not "test passed" 1000x)
- "If a human gets lost onboarding, an LLM is definitely going to be lost"
- "Every new context is essentially a new team member who needs to onboard"

### Design for Black Boxes
Small, isolated systems with clear inputs/outputs.
> "If you build a monolith of 100,000 lines, LLMs won't do as good a job."
> "Small, isolated, composable is the name of the game."

### CLI Over IDE
> "IDE integrations are a local optimum" - human interfaces that encourage fighting the model.

CLI = forcing function. Models know terminals, can't work in GUIs.
> **"CLI encourages the manager mindset because you simply don't see the code."**

Windows users: "get off" - agents trained on Unix shells, path issues waste context.

### TDD Is No Longer a Scam
For humans: silly, costly to maintain.
For LLMs: **"the best thing ever"** - feedback loop by design.
> "You can do crazy things when you have a test spec."

### DevDocs Pattern (similar to Ralph)
- `devdocs/plan.md`: goals, phases, approach
- `devdocs/progress.md`: current status, checkboxes
> **"Your plan is permanent, code is ephemeral."**
> "You want to be able to kill any single session at any moment."

### Key Quote
> **"The only way to get good at working with agents is to try. The first month, you're probably not going to be productive. You're going to swear a lot."**

---

## Part 5: The Great Engineering Divergence - Paul Dix

*243.7K views - "2026: The Great Engineering Divergence"*

### Core Thesis
> "Once coding speed jumps, everything around it becomes the constraint."

### Amdahl's Law for Software Delivery
If coding is 20% of the end-to-end cycle, making it 10x faster only yields ~1.25x overall speedup.

> "Almost no organization's existing software delivery process is capable of taking in 10x more code."

Developers report 20-50% more productive, but if pipeline could handle it → 10x-100x.

### The Divergence
- **Winners**: Organizations that update processes for non-code chokepoints
- **Losers**: Those bottlenecked in review, testing, release

### Agent-Accessible Pipelines
Properties that make software delivery accessible to agents:
- Deterministic tests + fast local runs
- "One command" dev environment
- Crisp module boundaries
- Docs colocated with code
- Golden datasets + perf harnesses
- Agent-accessible observability

### YC Observation
> "Nearly all the code for companies in this latest batch was written by AI, despite these companies having programmers in their founding teams."

---

## Part 6: Other Notable Insights

### Harrison Chase (@hwchase17) - 165K views
> "In software, code documents the app. In AI, the traces do."

Source of truth shifted from static code to runtime behavior.

### Dan Shipper (@danshipper) - 72K views
**Agent-native Architectures**: "Growing a garden" vs "building a skyscraper"
- Skyscraper: rigid blueprints, deterministic, top-down
- Garden: organic growth, adaptation, emergent

### Aaron Levie (@levie) - 4.7M views
**"Jevons Paradox for Knowledge Work"**
- Historical: More efficient coal → more coal demand
- Now: More efficient knowledge work → more knowledge work demand
- Implication: AI won't eliminate jobs, will expand what's possible

### @irl_danB - Technical Architecture
> "Remember: subagents for control flow, skills for composable behavior"

Claude Code as "intelligent inversion of control container" - can wire up dependencies and orchestrate interactions.

### @NickADobos + @Dimillian
> "Turn sections of your codebase into skills. That way agents can easily see the key parts and start exploring there first."

---

## Appendix: Quick Reference

### The Essential Setup (from Boris)
1. `.claude/commands/` - Inner loop automation
2. `.claude/agents/` - Subagent definitions
3. `.claude/settings.json` - Pre-allowed permissions
4. `.mcp.json` - MCP server configs
5. `CLAUDE.md` - Team rules (git-tracked)

### The Ralph Stack
1. `ralph_task.md` - Source of truth
2. `.ralph/guardrails.md` - Learned constraints
3. `.ralph/progress.md` - Current status
4. `.ralph/errors.log` - What broke
5. `.ralph/activity.log` - Token tracking

### The Workflow (Boris's Pattern)
1. Plan mode (shift+tab twice) → iterate until good plan
2. Switch to auto-accept edits mode
3. Let Claude work with verification (tests, types, lint)
4. Background agents or ralph rotation for long tasks
5. Commit/review/add learnings to CLAUDE.md

---

*Last updated: January 12, 2026*
*Sources: 15+ Twitter threads, cumulative 20M+ views*
