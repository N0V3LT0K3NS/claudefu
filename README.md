# claudefu

**Meta-cognitive infrastructure for human-Claude collaboration.**

---

## What Is This?

Claudefu is a toolkit that gives Claude instances (and their human collaborators) meta-awareness of how to collaborate well.

It provides:
- **Fu docs** — Different "boot sequences" at various levels of abstraction
- **Skills** — Patterns for better collaboration, maintenance, and ideation
- **Agents** — Persistent helpers for orchestration, curation, and synthesis
- **Library** — Curated sources, recommended tools, open reasoning

## The Problem It Solves

When humans collaborate with Claude, two frictions compound:

1. **Tacit knowledge stays tacit** — Users have context, patterns, and awareness that would help Claude, but surfacing it is effortful. Knowing *when* to surface it is itself a skill.

2. **Effort doesn't compound** — Every user does the same work of context-sharing. Learnings don't flow between users or sessions.

Claudefu addresses this by:
- **Pre-packaging** meta-patterns so they don't need surfacing each time
- **Pooling effort** into maintained, shared infrastructure
- **Layering context** so you load what you need, not everything
- **Automating** where possible (source watching, synthesis, integration)

## The Fu Levels

Fu docs exist on a spectrum from practical to philosophical:

| Level | Name | What It Covers | When To Load |
|-------|------|----------------|--------------|
| L0 | Mechanical | Skills, agents, MCPs, hooks — how things work | Always (baseline) |
| L1 | Emergent | Practitioner patterns, hacks, what people actually do | Default for builders |
| L2 | Metacognitive | AI cognition, limitations, reasoning patterns | When debugging or going deep |
| L3 | Simulator | Janus, cyborgism, ontology of LLMs | For ideation, edge cases |
| L4 | Cybernetic | Systems theory, human-machine coupling | For philosophical grounding |
| L5 | Frontier | Consciousness, linguistics, deep weird | You'll know if you need it |

Higher levels = more abstract, less practical for "just coding," more useful for ideation and far-reaching thinking.

**Stacks** are pre-composed combinations:
- `builder` = L0 + L1 (practical default)
- `researcher` = L0 + L1 + L2 (understanding the substrate)
- `ideator` = L0 + L1 + L2 + L3 (far-reaching exploration)

## Quick Start

### Option 1: Clone and Bootstrap

```bash
git clone https://github.com/N0V3LT0K3NS/claudefu
cd claudefu
```

Then in Claude Code:
```
/orientation
```

Claude will explain what this is and help you set up.

### Option 2: Minimal Manual Setup

Copy `fu/stacks/builder.md` to your project's `.claude/` folder and reference it in your CLAUDE.md:

```markdown
# CLAUDE.md

## Claudefu
Load meta-awareness from: .claude/claudefu/builder.md
```

### Option 3: Just Read

Browse `fu/L0-mechanical.md` and `fu/L1-emergent.md` to understand the patterns. Use what resonates.

## Structure

```
claudefu/
├── fu/                    # The meta-docs (what you load)
├── skills/                # Executable patterns
│   ├── bootstrap/         # Setup and onboarding
│   ├── meta/              # Meta-cognitive patterns (the value)
│   ├── maintain/          # Repo upkeep (you don't touch)
│   └── compose/           # Fu generation and mixing
├── agents/                # Persistent helpers
├── hooks/                 # Automatic triggers
├── library/               # Sources, recommendations, reasoning
├── staging/               # Content processing area
├── contexts/              # Contemporary context (teaser)
├── configs/               # Ready-to-use configurations
└── docs/                  # GROK documentation and analyses
```

See [INDEX.md](INDEX.md) for complete file listing.

## Key Concepts

### The Meta-Pattern

Most interactions: User asks → Claude does → done.

The meta-pattern: User shares context → Claude examines from above → together they build infrastructure → infrastructure handles this class of problem → future tasks are easier.

**One good skill is worth more than a hundred manual prompts.**

### Progressive Disclosure

Fu docs load in layers. Descriptions are cheap (~100 tokens). Full content loads only when triggered. This keeps context lean until you need depth.

### The Simulation Principle

LLMs simulate systems they're given detailed descriptions of. This repo works by that mechanism — describe the capable, meta-aware agent, and Claude becomes it.

### Three Skill Categories

1. **Bootstrap** — You use once to set up (`/orientation`, `/install`)
2. **Meta** — The actual value (`/verification-design`, `/failure-autopsy`, `/ideation-expand`)
3. **Maintain** — Infrastructure that keeps the repo alive (you don't invoke directly)

## Documentation

The `docs/` folder contains the foundational GROK documentation:

| Document | Description |
|----------|-------------|
| [CLAUDE_CODE_GROK.md](docs/CLAUDE_CODE_GROK.md) | Original operational awareness guide |
| [CLAUDE_CODE_GROK_ENRICHED.md](docs/CLAUDE_CODE_GROK_ENRICHED.md) | Enriched version with curated resources |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- How to add sources
- How to propose fu additions
- How to contribute skills
- Review process

## Roadmap

- [x] Core fu docs (L0, L1)
- [x] Bootstrap skills
- [x] Meta-cognitive skill architecture
- [ ] L2-L5 fu docs (in progress)
- [ ] Source registry + digestion pipeline
- [ ] Fu composition system
- [ ] Contemporary contexts (separate repo eventually)

## Philosophy

Claudefu isn't just documentation. It's:
- **Executable** — Skills and agents that enact patterns
- **Living** — Maintained, updated, contributed to
- **Layered** — Load what you need, not everything
- **Open** — Sources and reasoning are visible

The goal is **shared extended cognition** — infrastructure that makes every human-Claude collaboration better because effort compounds.

---

## License

MIT

## Acknowledgments

Built on patterns from:
- Anthropic's official documentation and skills
- The Claude Code practitioner community
- OpenProse orchestration patterns
- Cyborgism and simulator theory discourse
- Everyone who's shared what works

---

*"Now you know kung fu. What will you build?"*
