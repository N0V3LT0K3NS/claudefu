# Staging — Content Processing Pipeline

Where source content gets processed before integration into fu docs.

---

## Structure

```
staging/
├── digests/              # Individual item digests
├── synthesis/            # Cross-item synthesis
└── pending-integration/  # Ready for human review
```

---

## The Flow

```
Source Content
    ↓
[Digest] — Extract key information, format consistently
    ↓
[Synthesis] — Find patterns across digests
    ↓
[Pending Integration] — Ready for human review
    ↓
Fu Integration — Add to appropriate fu doc
```

---

## Digest Format

```markdown
# Digest: [Item Title]

**Source:** [name]
**URL:** [link]
**Processed:** YYYY-MM-DD
**Level:** L[0-5]

## Summary
[Brief summary]

## Key Points
- Point 1
- Point 2

## Patterns
[Reusable patterns identified]

## Integration Recommendation
[Where this should go in fu docs]

## Raw Notes
[Detailed extraction]
```

---

## Naming Convention

Digests: `YYYY-MM-DD-[source]-[item-slug].md`
Synthesis: `theme-[topic].md`
Pending: `L[0-5]-additions-YYYY-MM.md`
