# Skill Registry

Index of available skills in this repository.

## Available Skills

### repo-analyzer

**Location**: `.claude/skills/repo-analyzer/`

**Description**: Analyzes repositories for Claude Code infrastructure patterns and lessons. Use when: "analyze this repo", "extract patterns", "what can we learn from this", "Claude Code infrastructure analysis".

**Invocation**: `/repo-analyzer [path or GitHub URL]`

**Triggers**:
- "analyze repo"
- "repo patterns"
- "infrastructure analysis"
- "learn from this repo"
- "extract claude patterns"

**Tools**: Read, Glob, Grep, Bash, WebFetch, Task

**Model**: opus

**Outputs**:
| Output | Description |
|--------|-------------|
| Analysis Report | Structured inventory of infrastructure + pattern analysis |
| GROK Delta | Suggested additions to GROK documentation |

**Supporting Files**:
| File | Purpose |
|------|---------|
| `checklists/infrastructure-audit.md` | What to look for during analysis |
| `frameworks/pattern-taxonomy.json` | How to classify discovered patterns |
| `frameworks/grok-mapping.json` | Where findings map to GROK sections |
| `templates/analysis-report.md` | Output structure for reports |
| `templates/grok-delta.md` | Output structure for GROK suggestions |

**Workflow**:
1. **Acquisition**: Accept local path or GitHub URL, clone if needed
2. **Detection**: Run parallel scanners for each component type
3. **Extraction**: Identify novel patterns, classify by taxonomy
4. **Mapping**: Map findings to GROK sections
5. **Synthesis**: Generate report and GROK delta

---

## Adding to This Registry

When adding a new skill, include:

```markdown
### skill-name

**Location**: `.claude/skills/skill-name/`

**Description**: [When and why to use this skill]

**Invocation**: `/skill-name [arguments]`

**Triggers**:
- "trigger phrase 1"
- "trigger phrase 2"

**Tools**: [List of allowed tools]

**Model**: [opus/sonnet/haiku]

**Outputs**:
| Output | Description |
|--------|-------------|

**Supporting Files**:
| File | Purpose |
|------|---------|

**Workflow**:
1. Step 1
2. Step 2
```

---

## Skill Categories

### Analysis & Research
- **repo-analyzer** - Repository infrastructure analysis

### (Future Categories)
- Documentation
- Code Generation
- Review & Validation
- Workflow Automation

---

## Quick Reference

| Skill | Trigger | Primary Use |
|-------|---------|-------------|
| repo-analyzer | `/repo-analyzer` | Analyze repos for Claude Code patterns |

---

*Last updated: 2026-01-27*
