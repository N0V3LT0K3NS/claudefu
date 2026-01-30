# Skill Registry

Index of available skills in claudefu.

---

## Skill Categories

### Bootstrap (`/skills/bootstrap/`)
Setup and onboarding skills. Used once or rarely.

| Skill | Status | Description |
|-------|--------|-------------|
| `orientation` | ✅ Ready | Explain claudefu to new users |
| `assess` | 📋 Stub | Help determine needed fu level |
| `install` | 📋 Stub | Set up claudefu in a project |
| `update` | 📋 Stub | Update claudefu installation |
| `customize` | 📋 Stub | Customize claudefu setup |

### Meta (`/skills/meta/`)
Meta-cognitive patterns. The actual value.

#### Before-Work
| Skill | Status | Description |
|-------|--------|-------------|
| `verification-design` | 📋 Stub | Define success criteria before building |
| `assumption-audit` | 📋 Stub | Surface implicit assumptions |
| `scope-negotiation` | 📋 Stub | Decide minimal vs infrastructure |
| `decomposition-check` | 📋 Stub | One agent or many? |

#### During-Work
| Skill | Status | Description |
|-------|--------|-------------|
| `confidence-signal` | 📋 Stub | Flag uncertainty levels |
| `knowledge-gap-signal` | 📋 Stub | Surface knowledge gaps |
| `stuck-escalation` | 📋 Stub | Options after N failures |
| `parallel-opportunity` | 📋 Stub | Notice parallel potential |

#### After-Work
| Skill | Status | Description |
|-------|--------|-------------|
| `failure-autopsy` | 📋 Stub | Understand and prevent errors |
| `pattern-harvest` | 📋 Stub | Extract what's worth keeping |
| `solution-generalizer` | 📋 Stub | Generalize solutions |

#### Session
| Skill | Status | Description |
|-------|--------|-------------|
| `context-health` | 📋 Stub | Monitor context capacity |
| `session-retrospective` | 📋 Stub | Capture session learnings |
| `handoff-protocol` | 📋 Stub | Prepare for continuation |

#### Ideation
| Skill | Status | Description |
|-------|--------|-------------|
| `divergent-expansion` | 📋 Stub | Explore possibility space |
| `constraint-surfacing` | 📋 Stub | Make constraints explicit |
| `perspective-shift` | 📋 Stub | Try different angles |
| `synthesis-check` | 📋 Stub | Prevent early convergence |
| `decision-scaffold` | 📋 Stub | Structure decisions |

### Maintain (`/skills/maintain/`)
Repository infrastructure. Users don't invoke directly.

#### Sources
| Skill | Status | Description |
|-------|--------|-------------|
| `add-source` | 📋 Stub | Add new source to registry |
| `evaluate-pending` | 📋 Stub | Review pending sources |
| `blacklist-source` | 📋 Stub | Remove source with reasoning |
| `audit-sources` | 📋 Stub | Periodic quality review |

#### Digest
| Skill | Status | Description |
|-------|--------|-------------|
| `exhaustive-ingest` | 📋 Stub | Process whole corpus |
| `corpus-synthesize` | 📋 Stub | Find patterns across digests |
| `bootstrap-fu` | 📋 Stub | Generate fu from synthesis |
| `feed-check` | 📋 Stub | Check for new content |
| `incremental-ingest` | 📋 Stub | Process single item |
| `integrate-new` | 📋 Stub | Add to fu structure |
| `digest-report` | 📋 Stub | Report on processed content |

#### Format
| Skill | Status | Description |
|-------|--------|-------------|
| `doc-formatter` | 📋 Stub | Standardize formatting |
| `link-checker` | 📋 Stub | Verify links |
| `index-rebuilder` | 📋 Stub | Update indexes |

#### Changelog
| Skill | Status | Description |
|-------|--------|-------------|
| `changelog-updater` | 📋 Stub | Update changelog |

#### Analysis
| Skill | Status | Description |
|-------|--------|-------------|
| `repo-analyzer` | ✅ Ready | Analyze repos for patterns |

### Compose (`/skills/compose/`)
Fu generation and mixing.

| Skill | Status | Description |
|-------|--------|-------------|
| `fu-mixer` | 📋 Stub | Combine fu levels |
| `fu-from-sources` | 📋 Stub | Generate fu from sources |
| `custom-fu-builder` | 📋 Stub | Interactive fu creation |
| `fu-diff` | 📋 Stub | Compare fu variants |

---

## Quick Reference

### Ready to Use
| Skill | Invocation | Use |
|-------|------------|-----|
| orientation | `/orientation` | New user introduction |
| repo-analyzer | `/repo-analyzer [path/url]` | Analyze repos for patterns |

### Key Meta Skills (when implemented)
| Skill | Invocation | Use |
|-------|------------|-----|
| verification-design | `/verification-design` | Before starting work |
| failure-autopsy | `/failure-autopsy` | After errors |
| pattern-harvest | `/pattern-harvest` | After success |
| divergent-expansion | `/divergent-expansion` | During ideation |

---

## Status Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | Ready for use |
| 📋 | Stub (structure only) |

---

## Adding Skills

See `/skills/CLAUDE.md` for authoring standards.

When adding a skill:
1. Create directory: `/skills/[category]/[name]/`
2. Write SKILL.md with frontmatter
3. Add to this registry
4. Test invocation and triggers

---

*Last Updated: 2026-01-27*
