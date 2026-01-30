# Researcher Stack (L0 + L1 + L2)

For understanding the substrate. Includes metacognitive awareness.

---

# L0 — Mechanical

[See L0-mechanical.md for full content]

**Quick Reference:**

| Mechanism | Purpose |
|-----------|---------|
| CLAUDE.md | Persistent instructions |
| Skills | On-demand capabilities |
| SubAgents | Isolated workers |
| MCP | External connections |
| Hooks | Automatic triggers |
| Plugins | Bundled distribution |

---

# L1 — Emergent

[See L1-emergent.md for full content]

**Quick Reference:**

- **Meta-pattern:** Build infrastructure before executing
- **Verification:** Feedback loops = quality multiplier
- **Context:** State in files, not memory
- **Signs to go meta:** Repetition, errors, inconsistency

---

# L2 — Metacognitive

**Status:** Content in development — loading stub

Understanding Claude's cognition for debugging and robust systems.

## Core Concepts (Preview)

### Attention Patterns
Claude distributes attention unevenly across context. Position affects noticing.

### Reasoning Limitations
Strong: pattern matching, synthesis
Weak: precise counting, long logic chains

### Error Classes
- **Hallucination:** Confident about nonexistent things
- **Confusion:** Mixing up similar concepts
- **Omission:** Missing relevant information
- **Premature closure:** Stopping before complete

### Context Effects
Quality degrades with length. Symptoms:
- Repetition
- Contradiction
- Missing earlier context
- Increased errors

### When Claude Is Likely Wrong

Watch for:
- Very long chains of reasoning
- Precise numerical work
- Claims about specific facts
- High confidence without verification
- Novel combinations of concepts

### Defensive Strategies

1. **Verify outputs** — Don't trust, verify
2. **Break long chains** — Decompose reasoning
3. **Use tools for precision** — Bash for math, Read for facts
4. **Monitor confidence** — Probe when Claude seems certain
5. **Fresh context** — Rotate when degrading

---

## When This Stack Helps

- Debugging unexpected behavior
- Understanding why something failed
- Building robust systems
- Designing workflows that handle errors gracefully

---

## Sources

- Official Anthropic documentation
- Practitioner patterns
- Research on LLM behavior (to be integrated)
