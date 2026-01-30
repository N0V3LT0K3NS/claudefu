# Staging Standards

Standards for processing content in staging.

---

## Digest Quality

### What Makes a Good Digest

1. **Complete:** Captures all key information
2. **Concise:** No unnecessary verbosity
3. **Structured:** Uses consistent format
4. **Tagged:** Correct level assignment
5. **Actionable:** Clear integration recommendation

### What to Extract

- Core concepts and definitions
- Patterns (reusable)
- Examples (illustrative)
- Warnings and gotchas
- Connections to other content

### What to Skip

- Redundant information (already in fu)
- Outdated content
- Implementation details that change
- Personal opinions without patterns

---

## Synthesis Quality

### Cross-Digest Synthesis

When synthesizing across digests:

1. Identify common themes
2. Note contradictions
3. Find higher-order patterns
4. Suggest consolidation

### Synthesis Format

```markdown
# Synthesis: [Theme]

**Digests Included:**
- [digest 1]
- [digest 2]

## Common Patterns
[What appears across multiple sources]

## Contradictions
[Where sources disagree]

## Higher-Order Insights
[What emerges from combination]

## Integration Recommendation
[How to incorporate into fu]
```

---

## Processing Commands

- `/digest/exhaustive-ingest` — Process whole corpus
- `/digest/incremental-ingest` — Process single item
- `/digest/corpus-synthesize` — Synthesize across digests
- `/digest/integrate-new` — Add to fu
