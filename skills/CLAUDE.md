# Skill Authoring Standards

Standards for creating and maintaining skills in claudefu.

---

## What Skills Are

Skills are modular capability packages that load when relevant. They provide:
- **Knowledge** — Domain expertise, patterns, references
- **Workflows** — Step-by-step processes invocable via `/skill-name`
- **Auto-triggers** — Patterns that activate without explicit invocation

---

## Directory Structure

```
skill-name/
├── SKILL.md              # Required: frontmatter + instructions
├── scripts/              # Optional: executable code
├── references/           # Optional: additional docs
└── assets/               # Optional: templates, examples
```

Only `SKILL.md` is required. Add other folders as needed.

---

## SKILL.md Format

```yaml
---
name: skill-name
description: >-
  When to use this skill. Be specific about triggers.
  Include what it does AND when to activate.
triggers:
  - "keyword phrase"
  - "another trigger"
tools:
  - Read
  - Write
  - Bash
model: sonnet  # Optional: preferred model
context: fork  # Optional: run in isolated context
disable-model-invocation: true  # Optional: user-only
---

# Skill Name

## Purpose
[What this skill does and why it exists]

## When to Use
[Specific situations that should trigger this skill]

## When NOT to Use
[Situations where this skill is wrong]

## Process
[Step-by-step instructions]

## Output
[What the skill produces]

## Examples
[Concrete examples of usage]
```

---

## Key Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `name` | Yes | Unique identifier, lowercase-hyphenated |
| `description` | Yes | When to use — be specific! |
| `triggers` | Yes | Keywords that auto-activate |
| `tools` | Yes | Allowed tools for this skill |
| `model` | No | Preferred model (sonnet, opus, haiku) |
| `context: fork` | No | Run in isolated subagent context |
| `disable-model-invocation` | No | Hide from Claude until user invokes |

---

## Writing Good Descriptions

The description is critical — it determines when the skill activates.

**Bad:**
```yaml
description: Helps with code
```

**Good:**
```yaml
description: >-
  Reviews code for security vulnerabilities, performance issues,
  and style violations. Use when reviewing PRs, auditing code,
  or checking for common problems.
```

Include:
- What the skill does
- When to use it
- Specific trigger situations

---

## Trigger Design

Triggers auto-activate the skill when keywords appear.

**Guidelines:**
- Use natural phrases users would say
- Be specific enough to avoid false positives
- Test that triggers activate when expected
- Test that triggers DON'T activate incorrectly

**Examples:**
```yaml
triggers:
  - "review this code"
  - "check for security issues"
  - "audit this PR"
```

---

## Token Budget

| Section | Target | Maximum |
|---------|--------|---------|
| Full SKILL.md | 1500 | 3000 |
| Description | 50 | 100 |
| Process | 500 | 1500 |

Skills should be focused. If it's getting too long, consider splitting into multiple skills.

---

## Workflow Patterns

### Checklist Pattern
For multi-step sequential tasks:
```markdown
## Process
1. First do X
2. Then check Y
3. If Y passes, do Z
4. Report results
```

### Feedback Loop Pattern
For quality-critical work:
```markdown
## Process
1. Perform the action
2. Validate the result
3. If validation fails, diagnose and fix
4. Repeat until valid
```

### Conditional Pattern
For different paths based on input:
```markdown
## Process
1. Analyze the input type
2. If type A: follow path A
3. If type B: follow path B
4. Merge results
```

---

## Skill Categories

Skills in claudefu belong to one of four categories:

### `/skills/bootstrap/`
**Users touch once or rarely.** Setup and onboarding.
- orientation, assess, install, update

### `/skills/meta/`
**The actual value.** Meta-cognitive patterns users want.
- before-work, during-work, after-work, session, ideation

### `/skills/maintain/`
**Powers the repo.** Users don't invoke directly.
- sources, digest, format, changelog

### `/skills/compose/`
**Fu generation.** Creating and mixing fu docs.
- fu-mixer, custom-fu-builder

---

## Testing Skills

### Before Publishing

1. **Invocation test:** Does `/skill-name` work?
2. **Trigger test:** Do trigger phrases activate it?
3. **Non-trigger test:** Does it NOT trigger incorrectly?
4. **Behavior test:** Does it do what it should?
5. **Token test:** Is it within budget?

### Test Checklist

- [ ] Frontmatter is valid YAML
- [ ] Name is unique and lowercase-hyphenated
- [ ] Description is specific
- [ ] Triggers are appropriate
- [ ] Process is clear
- [ ] Examples are helpful
- [ ] Under 3000 tokens
- [ ] Tested invocation
- [ ] Tested triggers

---

## Common Mistakes

### Too Vague
```yaml
# Bad
description: Does helpful things

# Good
description: Extracts requirements from user stories and creates test cases
```

### Too Broad
```yaml
# Bad - will trigger on everything
triggers:
  - "help"
  - "do"

# Good - specific to purpose
triggers:
  - "extract requirements"
  - "create test cases from story"
```

### Missing When NOT to Use
Always include situations where the skill shouldn't be used.

### Overly Complex
If the skill is > 3000 tokens, it's doing too much. Split it.

---

## Updating Skills

When modifying existing skills:

1. Test before and after behavior
2. Update CHANGELOG.md if significant
3. Consider backward compatibility
4. Document breaking changes

---

## Review Process

See CONTRIBUTING.md for the full process.

Skills require one maintainer review. Reviewers check:
- Frontmatter validity
- Description quality
- Trigger appropriateness
- Process clarity
- Token budget
- Test results
