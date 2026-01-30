# L2 — Metacognitive

**Status:** 📋 Stub — Content coming soon

Understanding Claude's cognition. When debugging, going deep, or building robust systems.

---

## What This Level Covers

L2 provides meta-awareness of how Claude thinks:

- **Attention patterns** — What Claude notices, what it misses
- **Reasoning limitations** — Where Claude is likely to make errors
- **Uncertainty modeling** — How Claude calibrates confidence
- **Error classes** — Common failure modes and their signatures
- **Cognitive load** — How context size affects quality

---

## Intended Content

### Attention Dynamics
How Claude distributes attention across context. What gets noticed early vs late in context. How to position important information.

### Reasoning Patterns
Where Claude reasons well (pattern matching, synthesis) vs poorly (precise counting, long chains of logic). How to structure tasks to play to strengths.

### Confidence Calibration
When Claude's confidence matches reality vs when it's overconfident. Signatures of uncertainty. When to probe further.

### Error Taxonomy
Common error classes: hallucination, confusion, omission, premature closure. How to detect and prevent each.

### Context Effects
How context length affects quality. Degradation patterns. When to rotate. How to maintain state across rotations.

---

## When To Load This Level

- Debugging unexpected Claude behavior
- Building systems that need to handle Claude errors gracefully
- Understanding why a particular approach failed
- Designing robust workflows

---

## Sources (To Be Integrated)

- Anthropic research papers on LLM behavior
- Empirical testing and case studies
- Constitutional AI papers
- Attention mechanism research

---

## Contributing

This level needs content. If you have:
- Empirical observations about Claude's reasoning patterns
- Research on LLM cognition
- Case studies of failures and their root causes

See CONTRIBUTING.md for how to propose additions.
