# claudefu Repository Instructions

This repository contains Claude Code infrastructure patterns, documentation, and tools.

## Repository Purpose

1. **Document** Claude Code capabilities via the GROK guides
2. **Analyze** other repositories for patterns via repo-analyzer skill
3. **Extend** Claude's capabilities through reusable skills
4. **Archive** research and exploration from the living document project

## Directory Structure

```
claudefu/
├── .claude/                  # Claude Code infrastructure
│   ├── CLAUDE.md            # Meta-context for infrastructure
│   ├── SKILL_REGISTRY.md    # Index of available skills
│   └── skills/              # Reusable skill definitions
├── docs/                    # Primary documentation
│   ├── CLAUDE_CODE_GROK*.md # Operational awareness guides
│   └── analyses/            # Repository analysis outputs
└── archive/                 # Historical research documents
```

## Maintenance Tasks

### Adding Analysis Results

When running `/repo-analyzer` on a new repository:
1. Save the analysis report to `docs/analyses/[repo-name].md`
2. Save the GROK delta to `docs/analyses/[repo-name]-grok-delta.md`
3. Review delta suggestions and apply valuable ones to `CLAUDE_CODE_GROK_ENRICHED.md`
4. Update the analyses table in README.md

### Updating GROK Documentation

When adding patterns to GROK_ENRICHED.md:
1. Place content in the appropriate Part (0-10)
2. Maintain consistent formatting with existing content
3. Include source attribution (which repo/file the pattern came from)
4. Update "Last Updated" date at the bottom

### Adding New Skills

When creating a new skill:
1. Create directory under `.claude/skills/[skill-name]/`
2. Write SKILL.md with proper frontmatter (name, description, triggers, tools)
3. Add supporting files (checklists, frameworks, templates) as needed
4. Register in `.claude/SKILL_REGISTRY.md`
5. Add to README.md index

## Conventions

### File Naming
- Skills: lowercase-hyphenated (`repo-analyzer`)
- Documents: UPPER_SNAKE_CASE for primary docs (`CLAUDE_CODE_GROK.md`)
- Analyses: lowercase-hyphenated matching repo name

### Commit Messages
- `feat(skill): add [skill-name]` - New skill
- `docs(grok): add [pattern-name]` - GROK additions
- `analysis([repo]): add analysis` - New analysis
- `chore: [description]` - Maintenance

### GROK Delta Review

Before applying GROK delta suggestions:
1. Check for redundancy with existing content
2. Verify code examples are accurate
3. Maintain consistent tone
4. Prefer concrete examples over abstract descriptions

## Key Files

| File | Purpose | When to Edit |
|------|---------|--------------|
| `README.md` | Public index | When adding skills/analyses |
| `CLAUDE.md` | These instructions | When changing conventions |
| `.claude/SKILL_REGISTRY.md` | Skill index | When adding/modifying skills |
| `docs/CLAUDE_CODE_GROK_ENRICHED.md` | Main documentation | When adding patterns |

## Learned Rules

- 2026-01-27: Created repo-analyzer skill and analyzed compound-engineering-plugin
- 2026-01-27: Added Part 10 (Curated Resources) to GROK_ENRICHED.md
