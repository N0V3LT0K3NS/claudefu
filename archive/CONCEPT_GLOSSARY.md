# Concept Glossary: Emerging Vocabulary of Agent Development

*Terms practitioners are coining as they discover new patterns.*

---

## Core Concepts

### Agent-Native Architecture
**Source:** Dan Shipper (@danshipper)
**Definition:** Software architecture designed from the ground up for AI agents rather than adapted from human-oriented designs.
**Metaphor:** "Growing a garden" vs "building a skyscraper"
- Skyscraper: rigid blueprints, deterministic, top-down
- Garden: organic growth, adaptation, emergent patterns
**Usage:** "This app is agent-native - it's basically Claude Code in a trenchcoat."

---

### Compounding Engineering
**Source:** Dan Shipper, popularized by Boris Cherny
**Definition:** The practice of systematically capturing AI mistakes as rules for future prevention, creating an accumulating knowledge base that improves agent behavior over time.
**Implementation:** Git-tracked CLAUDE.md that team members update during code review.
**Key insight:** "Mistakes evaporate. Lessons accumulate."

---

### Context Engineering
**Source:** Multiple - becoming industry standard
**Definition:** The discipline of optimizing what information enters an AI's context window to maximize utility within token constraints.
**Strategies (from Lance Martin/Manus):**
1. **Reduce** - Replace tool results with file references
2. **Offload** - Store on filesystem, not in context
3. **Isolate** - Sub-agents with own context windows

**Quote:** "Context engineers are just prompt engineers 2.0" (@vasuman)

---

### Context Pollution
**Source:** @agrimsingh (Ralph for Idiots)
**Definition:** The degradation of agent performance caused by accumulated irrelevant or contradictory information in the context window.
**Symptoms:**
- Repeating itself
- "Fixing" same bug different ways
- Undoing its own previous fix
- Circular reasoning
**Key metaphor:** "Once the ball is in the gutter, adding spin doesn't save it."

---

### Context Rot
**Source:** Multiple practitioners
**Definition:** The inevitable degradation of a long-running AI session as context fills with outdated, contradictory, or hallucinated information.
**Key distinction:**
- Claude Code treats context rot as an **accident**
- Ralph treats context rot as a **certainty**

---

### The Great Decoupling
**Source:** Gemini team
**Definition:** The separation of **programming** (physically typing code) from **engineering** (architecture, goals, purpose).
**Implication:** LLMs will be better at the former; humans remain essential for the latter.
**Quote:** "You can suddenly use all programming languages instead of just ones you're familiar with."

---

### The Great Engineering Divergence
**Source:** Paul Dix
**Definition:** The predicted split between organizations that adapt their processes for AI-generated code vs those that bottleneck in review, testing, and release.
**Based on:** Amdahl's Law - optimizing one part of a system is limited by other parts.

---

### Guardrails (Ralph context)
**Source:** @agrimsingh, Geoffrey Huntley
**Definition:** Append-only rules in `.ralph/guardrails.md` that capture lessons from agent failures.
**Format:**
```markdown
### sign: check imports before adding
- trigger: adding a new import statement
- instruction: check if import already exists
- added after: iteration 3
```
**Philosophy:** "Basically kaizen, but for a golden retriever with a soldering iron."

---

### Inner Loop / Outer Loop
**Source:** Boris Cherny, common in software engineering
**Definition:**
- **Inner loop:** Workflows done many times per day (commit, test, lint)
- **Outer loop:** Less frequent but more complex workflows (releases, refactors)
**Application:** Use slash commands for inner loop, skills/subagents for outer loop.

---

### Jevons Paradox for Knowledge Work
**Source:** Aaron Levie (@levie)
**Definition:** The phenomenon where increased efficiency in AI-assisted knowledge work leads to increased demand for that work, not decreased employment.
**Historical parallel:** More efficient coal use → more coal demand
**Application:** AI won't eliminate knowledge work; it will expand what's possible.

---

### Perception-Articulation Flywheel
**Source:** User's philosophical framework (SESSION_CONTEXT.md)
**Definition:** The mutually reinforcing cycle of perceiving meaningful structure and articulating it into transferable symbols.
**Mechanism:**
```
noticing → naming → re-noticing through the name → re-naming at higher fidelity
```
**Key insight:** "Your vocabulary isn't just a set of labels; it's a set of instruments. Each new concept is a new sensor and a new actuator."
**Evidence:** Multiple practitioners describe this phenomenon independently (Harrison Chase's "traces," @agrimsingh's "guardrails," Boris's "compounding engineering").

---

### Progressive Disclosure (Skills context)
**Source:** Anthropic Engineering
**Definition:** The three-level loading system for Skills:
- **Level 1:** Metadata only (~100 tokens) - always loaded
- **Level 2:** SKILL.md body (~5k tokens) - when triggered
- **Level 3:** Scripts, resources - as needed
**Purpose:** Minimize context usage while enabling complex behaviors.

---

### Ralph / Ralph Loop
**Source:** Geoffrey Huntley (coined), @agrimsingh (explained)
**Definition:** A methodology for long-running AI tasks that deliberately resets context to prevent pollution.
**Purest form:** `while :; do cat prompt.md | agent ; done`
**Core principle:** "Memory" is the filesystem + git, NOT the chat.
**Philosophy:** "An agent that forgets on purpose."
**Key files:**
- `ralph_task.md` - Single source of truth
- `.ralph/guardrails.md` - Learned constraints
- `.ralph/progress.md` - Current status

---

### State Hygiene
**Source:** @agrimsingh
**Definition:** The discipline of managing where agent state lives (durable files vs volatile context).
**Key insight:** "The loop is not the technique. State hygiene is the technique."
**Comparison:**
| Bad State (Context) | Good State (Files + Git) |
|--------------------|--------------------------|
| Dies with conversation | Persists |
| Polluted by dead ends | Can be rolled back |
| Memory can drift | Git doesn't hallucinate |

---

### Traces as Documentation
**Source:** Harrison Chase (@hwchase17)
**Definition:** The paradigm shift from static code as documentation to runtime traces as documentation.
**Quote:** "In software, code documents the app. In AI, the traces do."
**Implication:** Source of truth moves from what you wrote to what actually happened.

---

### Vibe Engineering / Vibe Coding
**Source:** @mrexodia (article title)
**Definition:** The practice of working effectively with AI coding agents through intuition developed over time.
**Key aspects:**
- Understanding context limits
- Knowing when to fight vs trust
- Building verification harnesses
- Managing parallel agents
**Quote:** "The first month, you're probably not going to be productive. You're going to swear a lot."

---

## Role Concepts

### Genius Intern with Amnesia
**Source:** @mrexodia
**Definition:** Mental model for thinking about AI agents - incredibly fast and capable, but with zero long-term memory.
**Implication:** Design systems that don't rely on the agent "remembering."

---

### Tech Lead + QA Lead
**Source:** @mrexodia
**Definition:** The new role of humans working with AI agents.
**Responsibilities:**
- Write specs, plans, examples
- Define what "done" means
- Review outcomes, not lines of code
- Trust but verify

---

### Mini-You / Employee Frame
**Source:** Zvi Mowshowitz (@TheZvi)
**Definition:** Mental model for Claude Code - not a tool, but a capable employee with judgment.
**Implication:** Give context and intent, not just commands.

---

## Anti-Patterns

### Fighting the Model
**Source:** @mrexodia
**Definition:** Counterproductive behaviors that make humans the bottleneck.
**Symptoms:**
- "That's not how I would do it" → stopping
- Fixing formatting by hand
- Reviewing every single line
- Micromanaging agent decisions
**Solution:** Build better harness, not tighter grip.

---

### Dashboard Disease
**Source:** @vasuman
**Definition:** The impulse to create visibility systems instead of resolution systems.
**Quote:** "Please for the love of god do not create another dashboard. Dashboards are useless."
**Alternative:** "Make problems impossible to ignore and incredibly easy to resolve."

---

## File/Directory Conventions

### .ralph/
Directory structure for Ralph methodology:
```
.ralph/
├── guardrails.md    # Learned constraints (append-only)
├── progress.md      # Current status
├── errors.log       # What broke
└── activity.log     # Token tracking
```

### .claude/
Claude Code configuration directory:
```
.claude/
├── commands/        # Slash command definitions
├── agents/          # Subagent definitions
├── settings.json    # Permissions and config
└── plans/           # Plan mode output
```

### CLAUDE.md
Git-tracked rules file that accumulates team learnings about what Claude should/shouldn't do in this codebase.

### devdocs/
Pattern similar to Ralph, used by @mrexodia:
```
devdocs/
├── plan.md          # Goals, phases, approach
└── progress.md      # Current status, checkboxes
```

---

*Last updated: January 12, 2026*
*This glossary will expand as new vocabulary emerges*
