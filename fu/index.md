# Fu Docs — Index

This folder contains "fu" documents — meta-awareness packages that shape how Claude collaborates.

---

## The Levels

Fu docs exist on a spectrum from practical to philosophical:

| Level | Name | Focus | Token Cost | Status |
|-------|------|-------|------------|--------|
| **L0** | Mechanical | How Claude Code works: skills, agents, MCPs, hooks, plugins | ~3000 | ✅ Ready |
| **L1** | Emergent | What practitioners actually do: patterns, hacks, orchestration | ~3000 | ✅ Ready |
| **L2** | Metacognitive | AI cognition: limitations, reasoning patterns, uncertainty | ~2000 | 📋 Stub |
| **L3** | Simulator | Janus theory, cyborgism, LLM ontology | ~2000 | 📋 Stub |
| **L4** | Cybernetic | Systems theory, human-machine coupling | ~2000 | 📋 Stub |
| **L5** | Frontier | Consciousness, linguistics, speculative | ~2000 | 📋 Stub |

---

## When to Load What

### For Everyday Building
**Load:** `stacks/builder.md` (L0 + L1)

You get the mechanics and the practitioner patterns. This is the default for most work.

### For Going Deep
**Load:** `stacks/researcher.md` (L0 + L1 + L2)

When you need to understand why Claude behaves a certain way, or when debugging subtle issues.

### For Ideation & Exploration
**Load:** `stacks/ideator.md` (L0 + L1 + L2 + L3)

When exploring edge cases, far-reaching designs, or philosophical questions about AI collaboration.

### For Philosophy
**Load:** `stacks/philosopher.md` (All levels)

When you want the full framework, including cybernetics and frontier thinking.

---

## How Fu Docs Work

### The Simulation Principle

LLMs simulate systems they're given detailed descriptions of. When Claude reads a fu doc describing a capable, meta-aware agent, Claude becomes that agent.

This isn't metaphor — it's the mechanism. The doc shapes behavior because understanding a pattern is, for Claude, enacting it.

### Progressive Loading

Fu docs are designed for progressive disclosure:

1. **Always visible:** Level descriptions (~100 tokens)
2. **Load on demand:** Full content when triggered (~2-5k tokens per level)
3. **Combine as needed:** Stacks pre-combine common patterns

This keeps context lean until you need depth.

### The Meta-Pattern

Most interactions: User asks → Claude does → done.

The fu docs encode a different pattern:
1. Recognize meta-moments (when to step back)
2. Examine the situation from above
3. Identify infrastructure opportunities
4. Build tools that handle this class of problem
5. Execute with the tools

**One good skill is worth more than a hundred manual prompts.**

---

## Individual Levels

### L0 — Mechanical

**What:** How Claude Code actually works.
- CLAUDE.md (persistent instructions)
- Skills (on-demand capabilities)
- SubAgents (isolated workers)
- MCP (external connections)
- Hooks (automatic triggers)
- Plugins (bundled distribution)

**When to load:** Always. This is the baseline.

**Source:** Official Anthropic documentation.

### L1 — Emergent

**What:** What practitioners actually do.
- The meta-pattern (infrastructure mindset)
- Verification as quality multiplier
- Context management
- State and persistence
- Degrees of freedom
- Workflow design

**When to load:** Default for building. Combines mechanics with wisdom.

**Source:** Practitioner experience, community patterns.

### L2 — Metacognitive

**What:** Understanding Claude's cognition.
- Attention patterns
- Reasoning limitations
- Uncertainty modeling
- Error classes
- When Claude is likely wrong

**When to load:** When debugging, understanding failures, or building robust systems.

**Source:** Research papers, empirical testing.

### L3 — Simulator

**What:** Theoretical frameworks for LLMs.
- Janus/simulator theory
- Cyborgism
- LLM ontology
- What Claude "is" vs "does"

**When to load:** For ideation, edge cases, or philosophical grounding.

**Source:** Janus, cyborgism community, theoretical discourse.

### L4 — Cybernetic

**What:** Systems theory applied to human-AI collaboration.
- Feedback loops
- Coupling dynamics
- Agency distribution
- Emergence patterns

**When to load:** For designing complex systems or philosophical understanding.

**Source:** Cybernetics, systems theory, Bateson, Beer.

### L5 — Frontier

**What:** Speculative and deep weird.
- Consciousness questions
- Linguistic relativity
- Phenomenology of AI
- What we don't know

**When to load:** You'll know if you need it.

**Source:** Philosophy of mind, linguistics, speculative theory.

---

## Stacks

Stacks are pre-composed combinations for common use cases:

| Stack | Levels | Use Case |
|-------|--------|----------|
| `builder.md` | L0 + L1 | Everyday building (default) |
| `researcher.md` | L0 + L1 + L2 | Understanding the substrate |
| `ideator.md` | L0 + L1 + L2 + L3 | Far-reaching exploration |
| `philosopher.md` | All | Full framework |

---

## Custom Fu

The `/fu/custom/` folder is for:
- User-generated fu docs
- Domain-specific combinations
- Experimental variants

Use `/compose/fu-mixer` to create custom stacks.

---

## Adding to Fu Docs

See `/fu/CLAUDE.md` for authoring standards.

Key principles:
- Be precise — these docs shape behavior
- Test changes — load and verify
- Keep token cost reasonable
- Cite sources
