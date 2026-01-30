# .claude — Claude Code Integration

This directory integrates claudefu with Claude Code.

---

## What Lives Here

| File | Purpose |
|------|---------|
| `CLAUDE.md` | This file — context for Claude in this directory |
| `SKILL_REGISTRY.md` | Index of all skills |
| `TODO.md` | Tracking incomplete work |
| `skills/repo-analyzer/` | Legacy location (migrated to `/skills/maintain/`) |

---

## Relationship to Repo Structure

The main skill and agent definitions now live at the repo root:

| Component | Location |
|-----------|----------|
| Skills | `/skills/[category]/[name]/SKILL.md` |
| Agents | `/agents/[category]/[name].md` |
| Fu docs | `/fu/L[0-5]-*.md` |
| Library | `/library/` |
| Staging | `/staging/` |

This `.claude/` directory retains:
- Registry files (for Claude Code discovery)
- TODO tracking
- The original repo-analyzer (also copied to `/skills/maintain/`)

---

## See Also

- `/CLAUDE.md` — Root repo instructions
- `/INDEX.md` — Full navigation
- `/skills/CLAUDE.md` — Skill authoring standards
- `/fu/CLAUDE.md` — Fu authoring standards
