# Changelog

All notable changes to claudefu will be documented in this file.

Format based on [Keep a Changelog](https://keepachangelog.com/).

---

## [Unreleased]

### Planned
- L2-L5 fu docs (drafts in progress)
- Source registry automation
- Feed watching and incremental digestion
- Fu composition system

---

## [0.1.0] — 2026-01-27

### Added

**Core Structure**
- Repository architecture established
- INDEX.md with complete file navigation
- Root CLAUDE.md with maintenance standards
- CONTRIBUTING.md with contribution guidelines

**Fu Docs**
- `/fu/L0-mechanical.md` — Technical mechanics of Claude Code
- `/fu/L1-emergent.md` — Practitioner patterns and emergent use
- `/fu/stacks/builder.md` — L0+L1 combined stack
- `/fu/index.md` — Level descriptions and guidance
- `/fu/CLAUDE.md` — Standards for fu doc authoring

**Skills Architecture**
- Bootstrap skills structure (`orientation`, `assess`, `install`, `update`)
- Meta skills structure (before-work, during-work, after-work, session, ideation)
- Maintain skills structure (sources, digest, format)
- Compose skills structure (fu-mixer, custom-fu-builder)
- `/skills/CLAUDE.md` — Standards for skill authoring

**Agents Architecture**
- Bootstrap agents (`guide`)
- Meta agents (`meta-orchestrator`, `ideation-partner`, `critic`, `integrator`)
- Maintain agents (`source-curator`, `feed-watcher`, `corpus-processor`, `synthesis-engine`)
- Compose agents (`fu-architect`)

**Library**
- Source registry structure (whitelist, blacklist, pending)
- Source entry schema
- Evaluation criteria template
- Recommended resources structure
- `/library/CLAUDE.md` — Standards for source curation

**Staging**
- Digests structure
- Synthesis structure
- Pending integration structure
- `/staging/CLAUDE.md` — Standards for content processing

**Configs**
- Minimal config template
- Builder config template
- Ideator config template

**Contexts (Teaser)**
- AI landscape example context
- Context template for future expansion

### Notes
This is the initial architecture release. Many skills and agents are structural placeholders awaiting implementation. Fu docs L0 and L1 are functional; L2-L5 are stubs.

---

## Version Format

- **Major** (X.0.0): Breaking changes to fu docs or skill interfaces
- **Minor** (0.X.0): New fu levels, significant skills, major content additions
- **Patch** (0.0.X): Bug fixes, clarifications, minor content updates

---

## Upgrading

When upgrading claudefu:

1. Check this changelog for breaking changes
2. Run `/update` skill if available
3. Review changes to any configs you've customized
4. Test that your setup still works

---

## Contributing to Changelog

When submitting PRs:
- Add entry under `[Unreleased]`
- Use format: `- [Type] Description (@contributor)`
- Types: Added, Changed, Fixed, Removed, Deprecated, Security
