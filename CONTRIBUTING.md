# Contributing to Claudefu

Thank you for helping make human-Claude collaboration better.

---

## Ways to Contribute

| Contribution | Difficulty | Impact |
|--------------|------------|--------|
| Report issues | Easy | High |
| Propose sources | Easy | Medium |
| Improve documentation | Easy | Medium |
| Add skills | Medium | High |
| Improve fu docs | Medium | High |
| Add synthesis/digests | Medium | Medium |
| Core architecture | Hard | High |

---

## Quick Contributions

### Report an Issue

Found something broken or confusing?

1. Check existing issues first
2. Open a new issue with:
   - What you expected
   - What happened
   - Steps to reproduce
   - Relevant file paths

### Propose a Source

Know a good source we should track?

1. Check `/library/source-registry/whitelist/` — is it already there?
2. Check `/library/source-registry/pending/` — is it being evaluated?
3. If not, open an issue or PR with:
   - Source URL
   - Why it's valuable
   - What level it belongs to (L0-L5)
   - What we'd extract from it

### Fix Typos / Improve Clarity

1. Fork the repo
2. Make your changes
3. Submit a PR with clear description

---

## Adding Skills

### Before You Start

1. Check if a similar skill exists
2. Consider: is this a pattern that should be reusable?
3. Read `/skills/CLAUDE.md` for standards

### Process

1. Create skill directory: `/skills/[category]/[skill-name]/`
2. Write `SKILL.md` following the format in `/skills/CLAUDE.md`
3. Test:
   - Does `/skill-name` invoke correctly?
   - Do trigger phrases work?
   - Does it NOT trigger when it shouldn't?
4. Submit PR with:
   - What the skill does
   - Why it's needed
   - Test results

### Skill PR Checklist

- [ ] Follows SKILL.md format
- [ ] Has clear, specific description
- [ ] Has trigger phrases
- [ ] Includes "When NOT to use"
- [ ] Has examples
- [ ] Tested invocation and triggers
- [ ] Under 2000 tokens

---

## Adding Fu Content

### Before You Start

1. Identify which level (L0-L5) your content belongs to
2. Read `/fu/CLAUDE.md` for standards
3. Check existing content — does this duplicate?

### Process

1. Draft your content
2. Test by loading the fu doc — does behavior change as intended?
3. Submit PR with:
   - What you're adding
   - Why it belongs at this level
   - How it integrates with existing content

### Fu PR Checklist

- [ ] Correct level assignment
- [ ] Doesn't duplicate existing content
- [ ] Tone matches the level
- [ ] Tested that it affects behavior
- [ ] Reasonable token cost

---

## Adding Sources and Digests

### Proposing Sources

1. Use the template at `/library/schema/source-entry.md`
2. Add to `/library/source-registry/pending/`
3. Submit PR for review

### Adding Digests

If you've processed a source:

1. Follow digest format in `/staging/CLAUDE.md`
2. Add to `/staging/digests/`
3. Include integration recommendation
4. Submit PR

### Adding Synthesis

If you've synthesized across multiple digests:

1. Follow synthesis format in `/staging/CLAUDE.md`
2. Minimum 3 sources for synthesis
3. Add to `/staging/synthesis/`
4. Submit PR

---

## Review Process

### For Minor Changes (typos, clarity)
- One maintainer review
- Usually merged within a few days

### For Skills
- One maintainer review
- Must test invocation and triggers
- May request changes

### For Fu Content
- Two maintainer reviews (fu docs shape behavior)
- Must test behavioral impact
- Higher scrutiny for L0-L1 (most used)

### For Sources
- One maintainer review
- Evaluated against whitelist criteria
- May stay in pending while evaluating

---

## Style Guide

### Markdown
- Use ATX headers (`#`, `##`, `###`)
- One sentence per line (easier diffs)
- Use tables for structured comparisons
- Code blocks with language tags

### Tone
- Direct, not academic
- Instructive, not descriptive
- Clear over clever

### Naming
- Lowercase-hyphenated: `skill-name.md`
- Descriptive but concise
- Levels prefixed: `L0-`, `L1-`

---

## Development Setup

```bash
# Clone
git clone https://github.com/N0V3LT0K3NS/claudefu
cd claudefu

# Work in a branch
git checkout -b feature/your-feature

# Test your changes in Claude Code
# (load the fu docs, invoke skills, etc.)

# Commit with clear message
git commit -m "Add: [what] / Fix: [what] / Update: [what]"

# Push and PR
git push origin feature/your-feature
```

---

## Code of Conduct

- Be kind
- Assume good intent
- Focus on the work, not the person
- Help others learn

---

## Questions?

- Open an issue tagged `question`
- Check existing issues/discussions first
- Be specific about what you're trying to do

---

## Recognition

Contributors are recognized in:
- CHANGELOG.md (for significant contributions)
- Source entries (if you added the source)
- Skill frontmatter (`author` field)

Thank you for making claudefu better.
