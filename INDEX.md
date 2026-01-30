# Claudefu Index

Complete file listing with descriptions.

---

## Root

| File | Description |
|------|-------------|
| `README.md` | Entry point, vision, quick start |
| `INDEX.md` | This file — complete navigation |
| `CLAUDE.md` | Instructions for Claude instances working in this repo |
| `CHANGELOG.md` | Version history, what's changed |
| `CONTRIBUTING.md` | How to contribute sources, skills, fu content |
| `LICENSE` | MIT |

---

## `/fu` — The Meta-Docs

What users load to give Claude meta-awareness.

```
fu/
├── L0-mechanical.md           # How things work (skills, agents, MCPs, hooks)
├── L1-emergent.md             # Practitioner patterns, hacks, what actually works
├── L2-metacognitive.md        # AI cognition, limitations, reasoning
├── L3-simulator.md            # Janus, cyborgism, ontology of LLMs
├── L4-cybernetic.md           # Systems theory, Deleuze, Land, human-machine coupling
├── L5-frontier.md             # Consciousness, linguistics, deep weird
│
├── index.md                   # Map of levels, when to use which
│
├── stacks/                    # Pre-composed combinations
│   ├── builder.md             # L0 + L1 (practical default)
│   ├── researcher.md          # L0 + L1 + L2
│   ├── ideator.md             # L0 + L1 + L2 + L3
│   └── philosopher.md         # Everything
│
└── custom/                    # User-generated or composed fus
    └── .gitkeep
```

| Level | Status | Description |
|-------|--------|-------------|
| L0 | ✅ Ready | Anthropic docs synthesis, mechanics |
| L1 | ✅ Ready | Emergent patterns from practitioners |
| L2 | 📋 Stub | Metacognitive, AI-nature awareness |
| L3 | 📋 Stub | Simulator theory, cyborgism |
| L4 | 📋 Stub | Cybernetics, philosophy |
| L5 | 📋 Stub | Frontier, speculative |

---

## `/skills` — Executable Patterns

### `/skills/bootstrap` — Setup & Onboarding

*Users touch once or rarely.*

```
skills/bootstrap/
├── orientation/
│   └── SKILL.md               # "What is claudefu, how does it work"
├── assess/
│   └── SKILL.md               # "What do you need? Which fu level?"
├── install/
│   └── SKILL.md               # "Let's set you up"
├── update/
│   └── SKILL.md               # "Claudefu has updates, want them?"
└── customize/
    └── SKILL.md               # "Adjust your setup"
```

### `/skills/meta` — Meta-Cognitive Patterns

*The actual value. What users came for.*

```
skills/meta/
├── before-work/
│   ├── verification-design/   # Define success criteria before building
│   ├── assumption-audit/      # Surface implicit assumptions
│   ├── scope-negotiation/     # Minimal vs infrastructure — decide
│   └── decomposition-check/   # One agent or many?
│
├── during-work/
│   ├── confidence-signal/     # Flag uncertainty levels
│   ├── knowledge-gap-signal/  # "I don't know X, should I find out?"
│   ├── stuck-escalation/      # After N failures, surface options
│   └── parallel-opportunity/  # Notice when parallel would help
│
├── after-work/
│   ├── failure-autopsy/       # Understand error class, prevent
│   ├── pattern-harvest/       # Extract what's worth keeping
│   └── solution-generalizer/  # Does this apply elsewhere?
│
├── session/
│   ├── context-health/        # Monitor context, warn before degradation
│   ├── session-retrospective/ # At end, what should persist?
│   └── handoff-protocol/      # Prepare state for continuation
│
└── ideation/
    ├── divergent-expansion/   # Explore possibility space
    ├── constraint-surfacing/  # Make implicit constraints explicit
    ├── perspective-shift/     # Try different angles
    ├── synthesis-check/       # Are we converging too early?
    └── decision-scaffold/     # Structure decision when ready
```

### `/skills/maintain` — Repo Infrastructure

*Users don't touch directly. Powers the repo.*

```
skills/maintain/
├── sources/
│   ├── add-source/            # Evaluate and add a new source
│   ├── evaluate-pending/      # Review pending sources
│   ├── blacklist-source/      # Remove with reasoning
│   └── audit-sources/         # Periodic quality review
│
├── digest/
│   ├── exhaustive-ingest/     # Process whole corpus
│   ├── corpus-synthesize/     # Find patterns across digests
│   ├── bootstrap-fu/          # Generate fu from synthesis
│   ├── feed-check/            # Check sources for new content
│   ├── incremental-ingest/    # Process single new item
│   ├── integrate-new/         # Add to existing structure
│   └── digest-report/         # What's been processed
│
├── format/
│   ├── doc-formatter/         # Standardize formatting
│   ├── link-checker/          # Verify external links
│   └── index-rebuilder/       # Update indexes
│
└── changelog/
    └── changelog-updater/     # Update changelog on changes
```

### `/skills/compose` — Fu Generation

*Mix sources and levels to create new fu variants.*

```
skills/compose/
├── fu-mixer/                  # Combine existing fu levels
├── fu-from-sources/           # Generate fu from raw sources
├── custom-fu-builder/         # Interactive fu creation
└── fu-diff/                   # Compare two fu variants
```

---

## `/agents` — Persistent Helpers

```
agents/
├── bootstrap/
│   └── guide.md               # Knows your setup, answers questions
│
├── meta/
│   ├── meta-orchestrator.md   # Recognizes meta-moments, routes to skills
│   ├── ideation-partner.md    # Specialized for ideation sessions
│   ├── critic.md              # Adversarial — pokes holes, stress tests
│   └── integrator.md          # Synthesizes across threads/sessions
│
├── maintain/
│   ├── source-curator.md      # Manages source registry
│   ├── feed-watcher.md        # Monitors for new content
│   ├── corpus-processor.md    # Parallel digestion
│   ├── synthesis-engine.md    # Cross-item synthesis
│   └── staleness-checker.md   # Flags outdated content
│
└── compose/
    └── fu-architect.md        # Designs fu compositions
```

---

## `/hooks` — Automatic Triggers

```
hooks/
├── meta/
│   ├── on-error.json          # Consider failure-autopsy
│   ├── on-success.json        # Consider pattern-harvest
│   └── context-threshold.json # Trigger context-health at 70%
│
└── maintain/
    ├── on-pr.json             # Format check, link check
    ├── on-merge.json          # Rebuild indexes, update changelog
    └── scheduled-digest.json  # Periodic feed processing
```

---

## `/library` — Sources & Recommendations

### `/library/source-registry` — What We Pull From

```
library/source-registry/
├── README.md                  # How source management works
├── whitelist/
│   ├── index.md               # Master list
│   ├── L0/                    # Mechanical sources
│   ├── L1/                    # Emergent sources
│   ├── L2/                    # Metacognitive sources
│   └── .../
├── blacklist/
│   ├── index.md               # Why each is excluded
│   └── entries/
├── pending/
│   ├── index.md               # Under consideration
│   └── entries/
└── schema/
    ├── source-entry.md        # Template for documenting sources
    └── evaluation-criteria.md # How to decide
```

### `/library/sources` — Detailed Source Documentation

```
library/sources/
├── L0-mechanical/
│   ├── index.md
│   ├── anthropic-docs.md
│   ├── ericbuess-claude-docs.md
│   └── ...
├── L1-emergent/
│   ├── index.md
│   ├── ai-jason-youtube.md
│   ├── x-accounts.md
│   └── ...
└── .../
```

### `/library/recommended` — External Resources We Endorse

```
library/recommended/
├── skills/
│   ├── index.md
│   ├── anthropic-skills.md
│   └── awesome-claude-skills.md
├── agents/
│   └── index.md
├── mcps/
│   ├── index.md
│   └── mcp-servers.md
├── articles/
│   ├── index.md
│   ├── context-engineering-anthropic.md
│   └── manus-context-engineering.md
└── repos/
    ├── index.md
    └── openprose.md
```

---

## `/staging` — Content Processing Area

```
staging/
├── README.md                  # How staging works
├── digests/                   # Individual item digests
│   └── [YYYY-MM-DD]-[source]-[item].md
├── synthesis/                 # Cross-item synthesis
│   └── theme-[topic].md
└── pending-integration/       # Ready for human review
    └── [level]-additions.md
```

---

## `/contexts` — Contemporary Context (Teaser)

*Vision for where this is going. Eventually separate repo.*

```
contexts/
├── README.md                  # What this will become
├── ai-landscape/              # One worked example
│   ├── CONTEXT.md
│   └── sources.md
└── template/                  # Template for new contexts
    ├── CONTEXT.md
    └── sources.md
```

---

## `/configs` — Ready-to-Use Configurations

```
configs/
├── minimal/                   # Just L0 + basic skills
│   ├── CLAUDE.md
│   └── README.md
├── builder/                   # L0 + L1 + meta skills
│   ├── CLAUDE.md
│   └── README.md
├── ideator/                   # L0-L3 + ideation skills
│   ├── CLAUDE.md
│   └── README.md
└── composition-specs/         # Fu composition recipes
    ├── builder-plus-simulator.yaml
    └── ideation-cybernetic.yaml
```

---

## `/.claude` — Claude Code Integration

```
.claude/
├── CLAUDE.md                  # Instructions for Claude in this repo
├── settings.json              # Hooks configuration
└── skills/ → ../skills/       # Symlink to skills (if needed)
```

---

## Status Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | Ready for use |
| 🔨 | In development |
| 📋 | Stub/placeholder |
| 🔮 | Vision/future |

---

## Quick Navigation

**I want to...**

| Goal | Go To |
|------|-------|
| Understand what this is | [README.md](README.md) |
| Get set up | `/skills/bootstrap/orientation/` |
| Load practical awareness | `/fu/stacks/builder.md` |
| Use meta-cognitive patterns | `/skills/meta/` |
| Add a source | `/skills/maintain/sources/add-source/` |
| See what sources we use | `/library/source-registry/whitelist/` |
| Find recommended tools | `/library/recommended/` |
| Contribute | [CONTRIBUTING.md](CONTRIBUTING.md) |
