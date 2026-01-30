# Fu Authoring Standards

Standards for creating and maintaining fu docs.

---

## What Fu Docs Are

Fu docs are meta-awareness packages that shape Claude's behavior. They work by the simulation principle: Claude simulates systems it's given detailed descriptions of.

**Every word matters.** Fu docs directly influence how Claude reasons, what it notices, and what it proposes.

---

## Principles

### 1. Precision Over Volume

A few precise patterns beat many vague guidelines.

Bad: "Be aware of context limitations"
Good: "Monitor context usage. Above 75%, actively offload to files and suggest session rotation."

### 2. Instructive Over Descriptive

Tell Claude what to do, not just what exists.

Bad: "There are different levels of freedom"
Good: "Match instruction specificity to task fragility. High freedom for creative tasks, low for error-prone operations."

### 3. Actionable

Every section should translate to behavior.

Ask: "If Claude reads this, what will change?"

If the answer is "nothing specific," revise or remove.

### 4. Testable

You should be able to verify the doc works.

After editing, load the fu doc and check:
- Does Claude behave as intended?
- Does it surface the patterns when relevant?
- Does it avoid over-triggering?

---

## Structure

### Level Documents (L0-L5)

```markdown
# L[N]-[name].md

Brief description of what this level covers.

---

## Core Concepts

[The main patterns at this level]

---

## In Practice

[How to apply these patterns]

---

## When This Matters

[Specific situations where this level helps]

---

## Sources

[Where this content comes from]
```

### Token Budget

| Level | Target | Maximum |
|-------|--------|---------|
| L0 | 2500 | 4000 |
| L1 | 2500 | 4000 |
| L2 | 1500 | 2500 |
| L3 | 1500 | 2500 |
| L4 | 1500 | 2500 |
| L5 | 1500 | 2500 |
| Stack | Sum of levels | - |

Higher levels can be shorter — their concepts are more abstract.

---

## Tone by Level

| Level | Tone | Example |
|-------|------|---------|
| L0 | Technical, concrete | "Skills load in two phases: descriptions first, body on trigger" |
| L1 | Practical, advisory | "Prefer skills over CLAUDE.md for reference material" |
| L2 | Analytical | "Claude's attention distribution affects which details get noticed" |
| L3 | Theoretical | "The simulator produces responses by simulating the described system" |
| L4 | Systems-oriented | "Human-AI collaboration exhibits feedback dynamics" |
| L5 | Speculative | "What does it mean for an LLM to 'understand'?" |

---

## Content Guidelines

### Include

- **Patterns:** What to do, when, why
- **Examples:** Concrete situations
- **Decision points:** When to choose X vs Y
- **Warnings:** Common mistakes
- **Sources:** Where knowledge comes from

### Exclude

- **Fluff:** "AI is powerful and can do many things"
- **Obvious:** "Write code carefully"
- **Undifferentiated:** Content that could be in any AI doc
- **Outdated:** Features that have changed

### Formatting

- Use headers hierarchically (# → ## → ###)
- Tables for comparisons and quick reference
- Code blocks for examples
- Bold for key terms on first use
- Short paragraphs (3-5 sentences max)

---

## Stacks

Stacks combine levels. When creating stacks:

1. **Include section headers** showing where each level starts
2. **Compress overlap** — don't duplicate between levels
3. **Test combined length** — stacks should be loadable
4. **Maintain coherence** — the combined doc should read smoothly

Example structure:
```markdown
# Builder Stack (L0 + L1)

## L0 — Mechanical
[L0 content]

## L1 — Emergent
[L1 content]
```

---

## Testing Changes

### Before Publishing

1. Load the fu doc in a fresh session
2. Give tasks that should trigger the patterns
3. Verify Claude's behavior matches intent
4. Check for over-triggering (patterns appearing when irrelevant)
5. Verify token cost is within budget

### Test Prompts

Keep a set of test prompts for each level:

**L0 test:** "What tools can I use?" → Should describe skills, agents, MCP, etc.

**L1 test:** "I keep explaining the same thing" → Should suggest CLAUDE.md or skill

**L2 test:** "Why did Claude make this error?" → Should reason about cognitive patterns

---

## Versioning

Fu docs are versioned with the repo. When making significant changes:

1. Document in CHANGELOG.md
2. Note what behavior changed
3. Consider backward compatibility for users who've built on the old patterns

---

## Review Process

Changes to fu docs require two maintainer reviews because:
- They directly shape Claude behavior
- Small changes have large effects
- Compound over many users

See CONTRIBUTING.md for full process.
