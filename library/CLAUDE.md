# Library Curation Standards

Standards for managing sources and recommendations.

---

## Source Registry

### Whitelist Criteria

Sources on the whitelist must meet:

1. **Quality:** Accurate, well-written, up-to-date
2. **Relevance:** Directly applicable to Claude Code
3. **Stability:** Likely to remain available
4. **Uniqueness:** Provides value not covered elsewhere

### Blacklist Reasons

Sources are blacklisted for:

1. **Inaccuracy:** Contains significant errors
2. **Staleness:** Outdated with no updates
3. **Redundancy:** Fully covered by better sources
4. **Quality:** Poorly written or misleading

### Level Assignment

| Level | Source Type |
|-------|-------------|
| L0 | Official docs, mechanics |
| L1 | Practitioner blogs, tutorials |
| L2 | Research papers, analysis |
| L3 | Theory, philosophy |
| L4 | Systems theory, cybernetics |
| L5 | Speculative, frontier |

---

## Source Entry Format

```markdown
# Source Name

**URL:** [link]
**Level:** L0-L5
**Status:** Active | Inactive | Watch
**Added:** YYYY-MM-DD
**Last Checked:** YYYY-MM-DD

## What It Provides
[Key content we extract]

## Quality Notes
[Assessment of reliability, update frequency]

## Extraction Notes
[How to process this source]
```

---

## Recommended Resources

Recommendations are external resources we endorse but don't process into fu.

Format:
```markdown
# Resource Name

**URL:** [link]
**Category:** Skills | Agents | MCPs | Articles | Repos
**Why:** [Brief reason for recommendation]
```
