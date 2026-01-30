# CLAUDE.md — Claudefu Root

You are working in the **claudefu** repository — meta-cognitive infrastructure for human-Claude collaboration.

---

## What This Repo Is

Claudefu provides:
- **Fu docs** (`/fu`) — Meta-awareness at different abstraction levels
- **Skills** (`/skills`) — Executable patterns for collaboration, maintenance, composition
- **Agents** (`/agents`) — Persistent helpers
- **Library** (`/library`) — Curated sources and recommendations
- **Staging** (`/staging`) — Content processing pipeline
- **Docs** (`/docs`) — GROK documentation and analyses

**The core insight:** This repo works by the mechanism it describes. LLMs simulate systems they're given detailed descriptions of. By reading these docs, you gain the meta-awareness they encode.

---

## Your Role Here

When working in this repo, you might be:

### 1. A User's Claude (Loading Fu)
You've been given a fu doc to load. Apply its patterns. The fu doc tells you what to be aware of and how to collaborate well.

### 2. A Maintainer Claude (Repo Work)
You're helping maintain the repo itself — adding sources, processing content, updating docs. Follow the maintenance standards below.

### 3. A Contributor Claude (Adding Content)
You're helping add new fu content, skills, or sources. Follow the schemas and templates in `/library/schema/`.

---

## Key Commands

| Command | What It Does |
|---------|--------------|
| `/orientation` | Explain claudefu to a new user |
| `/assess` | Help user decide which fu level they need |
| `/install` | Set up claudefu in user's project |
| `/update` | Pull updates, migrate configs |
| `/repo-analyzer` | Analyze repositories for Claude Code patterns |

---

## Maintenance Standards

When editing this repo:

### Formatting
- Markdown with YAML frontmatter for skills/agents
- 80-char soft wrap for prose
- Use headers hierarchically (# → ## → ###)
- Tables for structured comparisons
- Code blocks with language tags

### Naming
- Lowercase-hyphenated for folders and files: `meta-orchestrator.md`
- UPPERCASE for root docs: `README.md`, `CLAUDE.md`
- Levels prefixed: `L0-`, `L1-`, etc.

### Skills Structure
```
skill-name/
├── SKILL.md           # Required: frontmatter + instructions
├── scripts/           # Optional: executable code
├── references/        # Optional: additional docs
└── assets/            # Optional: templates, examples
```

### SKILL.md Format
```yaml
---
name: skill-name
description: >-
  When to use this skill. Be specific.
triggers:
  - "keyword phrase"
tools:
  - Read
  - Write
---

# Skill Name

## Purpose
[What this skill does]

## Process
[Step by step]

## Output
[What it produces]
```

### Source Entries
Follow `/library/schema/source-entry.md` template.

### Digest Entries
Follow `/staging/README.md` for digest format.

---

## Awareness Reminders

### When Editing Fu Docs
- These docs shape Claude behavior. Be precise.
- Test changes by loading the doc and checking behavior.
- Changes compound — small edits have large effects.

### When Adding Sources
- Check whitelist criteria in `/library/source-registry/schema/evaluation-criteria.md`
- Document reasoning for inclusion
- Assign correct level (L0-L5)

### When Processing Content
- Digests go to `/staging/digests/`
- Use naming: `YYYY-MM-DD-[source]-[item].md`
- Tag with level assignment and integration recommendation

### When Creating Skills
- Skills should be invocable AND auto-triggerable (unless `disable-model-invocation: true`)
- Include clear triggers in description
- Test the skill works as both `/skill-name` and auto-trigger

---

## File Locations

| What | Where |
|------|-------|
| Fu docs | `/fu/` |
| Skills | `/skills/[category]/[skill-name]/SKILL.md` |
| Agents | `/agents/[category]/[name].md` |
| Hooks | `/hooks/[category]/[name].json` |
| Source registry | `/library/source-registry/` |
| Recommendations | `/library/recommended/` |
| Staging | `/staging/` |
| Configs | `/configs/` |
| GROK docs | `/docs/` |

---

## The Meta-Pattern

When working here, remember: **infrastructure compounds, one-off work evaporates.**

Before doing a task, ask:
- Is this a one-time fix or a pattern?
- Should this become a skill?
- Should this be documented?
- Will the next Claude/user benefit from what I learn here?

If yes → make it infrastructure, not just execution.

---

## Quality Checks

Before committing changes:

- [ ] Formatting follows standards
- [ ] Links work (internal and external)
- [ ] YAML frontmatter is valid
- [ ] New content has appropriate index entry
- [ ] CHANGELOG.md updated if significant

---

## Sub-Directory CLAUDE.md Files

Some directories have their own CLAUDE.md with specific instructions:
- `/fu/CLAUDE.md` — Standards for fu docs
- `/skills/CLAUDE.md` — Standards for skills
- `/library/CLAUDE.md` — Standards for source curation
- `/staging/CLAUDE.md` — Standards for content processing

Load the relevant sub-CLAUDE.md when working deeply in that area.

---

## When Stuck

- Check INDEX.md for navigation
- Check the relevant schema/ folder for templates
- Ask the user — they may have context you don't
- Propose infrastructure if you notice a gap
