# Repository Analysis: compound-engineering-plugin

**Analyzed:** 2026-01-27
**Source:** https://github.com/EveryInc/compound-engineering-plugin
**Analyzer:** repo-analyzer skill v1.0

---

## Executive Summary

The compound-engineering-plugin represents one of the most sophisticated Claude Code infrastructure implementations discovered to date. It's a monorepo plugin marketplace containing two plugins, with the primary `compound-engineering` plugin demonstrating advanced multi-agent orchestration, sophisticated workflow composition, and mature patterns for knowledge compounding.

| Component | Count | Notable |
|-----------|-------|---------|
| CLAUDE.md files | 2 | Hierarchical (root + plugin), timestamped learnings |
| Skills | 15 | Progressive disclosure, validation gates, decision menus |
| Agents | 28 | Organized by domain (research, design, docs, review, workflow) |
| Hooks | 0 | Not implemented |
| MCP Servers | 1 | Context7 for documentation |
| Commands | 24 | Namespace prefixing (workflows:), extreme parallelization |
| Plugins | 2 | Monorepo marketplace pattern |

**Overall Sophistication:** 5/5
**Documentation Quality:** 5/5
**Pattern Maturity:** 5/5
**Novel Contributions:** 5/5

---

## Infrastructure Inventory

### CLAUDE.md Files

| Location | Lines | Key Sections |
|----------|-------|--------------|
| `/CLAUDE.md` (root) | 381 | Repository overview, compounding philosophy, plugin management, timestamped learnings |
| `/plugins/compound-engineering/CLAUDE.md` | 91 | Versioning requirements, pre-commit checklist, command naming conventions |

**Notable Content:**

The root CLAUDE.md introduces the "Compounding Engineering" philosophy:
- **4-step process:** Plan → Delegate → Assess → Codify
- Multi-location description synchronization (plugin.json, marketplace.json, README.md)
- Component counting verification with bash commands

**Timestamped Learnings:**
- **2024-11-22:** Component count verification - "Always count actual files before updating descriptions across multiple locations"
- **2024-10-09:** Marketplace.json simplification - "Stick to the official spec to avoid confusion"

The plugin-level CLAUDE.md enforces:
- `workflows:` prefix for commands to avoid built-in collisions
- Semver versioning rules
- Third-person description requirement for skills
- 5-item pre-commit verification checklist

---

### Skills (15)

| Name | Triggers | Tools | Notable Pattern |
|------|----------|-------|-----------------|
| agent-browser | "browse website", "fill form" | Bash | Ref-based element selection (@e1, @e2) |
| file-todos | Creating/managing todos | Read, Write, Bash, Grep | YAML validation gates |
| agent-native-architecture | Design architecture | None (reference) | 5 Core Principles framework |
| compound-docs | "that worked", "it's fixed" | Read, Write, Bash, Grep | Auto-invoke on completion phrases |
| rclone | "upload to S3", "sync to cloud" | Bash | Multi-provider cloud sync |
| andrew-kane-gem-writer | "create a gem" | None (reference) | Production Ruby patterns |
| every-style-editor | Reviewing articles | None (reference) | Line-by-line editorial review |
| skill-creator | Creating new skills | None (reference) | Meta-skill for skill authoring |
| create-agent-skills | Working with SKILL.md | None (reference) | Anthropic spec compliance |
| brainstorming | "let's brainstorm" | None (reference) | Phase-based idea refinement |
| git-worktree | Code review workflows | Bash | Isolated parallel development |
| dspy-ruby | Implementing LLM features | None (reference) | Type-safe signatures |
| frontend-design | Build web components | None (reference) | Bold aesthetic guidance |
| gemini-imagegen | "generate image" | Python | Multi-turn refinement |
| dhh-rails-style | Ruby/Rails code | None (reference) | 37signals patterns |

**Skill Patterns Observed:**

1. **Validation Gates:** Skills like `compound-docs` implement `<validation_gate name="yaml-schema" blocking="true">` that explicitly block workflow continuation on failure.

2. **Decision Menus:** Post-workflow decision menus present structured next-step options rather than linear endings.

3. **Intake/Routing Pattern:** Reference skills implement routing tables that direct users to relevant content based on task type.

4. **MUST/MUST NOT Sections:** Binary obligation documentation separates requirements from recommendations.

5. **Environment Verification First:** Tool-dependent skills verify setup before attempting operations.

---

### Agents (28)

**Organization by Domain:**

| Domain | Count | Focus |
|--------|-------|-------|
| Research | 5 | External research, documentation gathering, git history analysis |
| Design | 3 | Figma sync, design verification, iteration |
| Docs | 1 | Ankane-style README writing |
| Review | 14 | Architecture, simplicity, data safety, language-specific, security, performance |
| Workflow | 5 | Bug reproduction, style editing, linting, PR resolution, spec analysis |

**Naming Conventions:**
- **Reviewer pattern:** `[expert-type]-reviewer` (6 agents)
- **Researcher pattern:** `[domain]-researcher` (5 agents)
- **Personified experts:** `dhh-rails-reviewer`, `kieran-[language]-reviewer`, `julik-frontend-races-reviewer`

**Notable Agents:**

| Agent | Unique Specialization |
|-------|----------------------|
| `agent-native-reviewer` | Agent capability parity (tools ≠ UI actions) |
| `julik-frontend-races-reviewer` | UI race conditions with Hotwire knowledge |
| `learnings-researcher` | Institutional knowledge with metadata filtering |
| `data-integrity-guardian` | Migration safety, ACID properties, GDPR |
| `code-simplicity-reviewer` | YAGNI enforcement, abstraction removal |

**Agent Architecture:**
- Most agents inherit model from context
- Only `learnings-researcher` and `lint` explicitly use haiku for lightweight tasks
- Clear inter-agent relationships: Research → Design → Review pipelines

---

### Commands (24)

**Organization:**
- **Root commands:** 19 utility commands, testing, audits
- **Workflow commands:** 5 orchestration commands (prefixed `workflows:`)

**Workflow Commands (Core Pipeline):**

| Command | Purpose | Parallelization |
|---------|---------|-----------------|
| `workflows:brainstorm` | Explore requirements before planning | Minimal |
| `workflows:plan` | Transform ideas into structured plans | 4+ agents |
| `workflows:work` | Execute plans with quality gates | Variable |
| `workflows:review` | Multi-agent code review | 13+ agents |
| `workflows:compound` | Document solved problems | 6+ agents |

**Extreme Parallelization Examples:**
- `deepen-plan`: Spawns 20-40+ parallel agents
- `agent-native-audit`: 8 parallel Explore agents
- `workflows:review`: 13+ parallel review agents
- `resolve_parallel`: One sub-agent per TODO (unlimited)

**Command Organization Patterns:**
- `workflows:` namespace prefix prevents collision with built-in commands
- `$ARGUMENTS` placeholder for dynamic content injection
- YAML frontmatter with `argument-hint` describing expected inputs

---

### MCP Servers (1)

| Name | Type | Purpose |
|------|------|---------|
| context7 | HTTP | Documentation retrieval (`https://mcp.context7.com/mcp`) |

---

### Plugins (2)

| Name | Version | Components |
|------|---------|------------|
| compound-engineering | 2.28.0 | 28 agents, 24 commands, 15 skills, 1 MCP |
| coding-tutor | 1.2.1 | 3 commands, 1 skill |

**Monorepo Pattern:** Central `marketplace.json` at root references plugins via relative paths.

---

## Pattern Analysis

### Novel Patterns Worth Learning

#### 1. Namespace Prefixing for Commands

**What:** Prefix commands with `workflows:` to avoid collisions with built-in Claude Code commands.

**Why it's valuable:** As plugins grow, command name collisions become inevitable. Namespace prefixing provides clear ownership and prevents shadowing built-in functionality.

**Implementation:**
```
commands/
├── test-browser.md           # Root utility commands
├── resolve_parallel.md
└── workflows/
    ├── work.md               # Invoked as /workflows:work
    ├── plan.md               # Invoked as /workflows:plan
    └── review.md             # Invoked as /workflows:review
```

**Source:** `plugins/compound-engineering/CLAUDE.md`

---

#### 2. Validation Gates in Skills

**What:** Explicit blocking gates that prevent workflow continuation on validation failure.

**Why it's valuable:** Ensures data integrity without relying on heuristics. Makes failure points explicit in the skill definition itself.

**Implementation:**
```markdown
<validation_gate name="yaml-schema" blocking="true">
Validate that YAML frontmatter matches schema before creating file.
If validation fails, STOP and report the error.
</validation_gate>
```

**Source:** `plugins/compound-engineering/skills/compound-docs/SKILL.md`

---

#### 3. Decision Menus Post-Workflow

**What:** Present structured decision menus after completing the main workflow, transforming linear flows into branching paths.

**Why it's valuable:** Allows users to direct next actions based on context. Converts single-purpose skills into multi-pathway tools.

**Implementation:**
```markdown
## After Documentation Created

Present these options to the user:
1. Continue with current work
2. Promote to critical patterns library
3. Link to related GitHub issues
4. Add findings to existing skill
5. Create new skill from pattern
6. View all related documentation
```

**Source:** `plugins/compound-engineering/skills/compound-docs/SKILL.md`

---

#### 4. Extreme Parallel Agent Spawning

**What:** Commands that spawn 20-40+ parallel sub-agents for maximum throughput.

**Why it's valuable:** Dramatically reduces wall-clock time for complex tasks. Leverages Claude Code's ability to run many agents simultaneously.

**Implementation:**
```markdown
## Phase 2: Parallel Research (deepen-plan)

For EACH section in the plan, spawn parallel agents:
- Task best-practices-researcher("Research best practices for [section topic]")
- Task framework-docs-researcher("Find documentation for [relevant frameworks]")
- Task learnings-researcher("Search institutional knowledge for [section topic]")
- [All 15+ skills discovered dynamically]
- [All relevant review agents]

Do NOT wait between spawns - launch all in parallel.
```

**Source:** `plugins/compound-engineering/commands/deepen-plan.md`

---

#### 5. Personified Expert Agents

**What:** Name agents after real experts/philosophies they embody (dhh-rails-reviewer, kieran-typescript-reviewer).

**Why it's valuable:** Brings personality and specific philosophy to reviews. Makes agent purpose instantly clear. Enables opinionated, consistent feedback.

**Implementation:**
```yaml
---
name: dhh-rails-reviewer
description: |
  Reviews code from DHH/37signals perspective.
  Enforces Rails conventions, rejects JavaScript patterns,
  prefers server-rendered HTML over SPAs.
---
You are a code reviewer channeling David Heinemeier Hansson's philosophy...
```

**Source:** `plugins/compound-engineering/agents/review/dhh-rails-reviewer.md`

---

#### 6. Hierarchical CLAUDE.md Organization

**What:** Root CLAUDE.md for marketplace-wide constraints, plugin CLAUDE.md for specific conventions.

**Why it's valuable:** Separates concerns between maintainers of multiple plugins and individual plugin developers. Enables inheritance of rules.

**Implementation:**
```
/CLAUDE.md                    # Marketplace-wide: counts, descriptions, JSON structure
/plugins/compound-engineering/
  CLAUDE.md                   # Plugin-specific: versioning, command naming, pre-commit
```

**Source:** Repository structure

---

#### 7. Timestamped Learnings Section

**What:** Append-only section in CLAUDE.md with dated learnings from production use.

**Why it's valuable:** Creates institutional memory. Prevents repeating mistakes. Shows evolution of understanding.

**Implementation:**
```markdown
## Key Learnings

- **2024-11-22**: Added gemini-imagegen skill; discovered component counts were wrong.
  Learning: Always count actual files before updating descriptions across multiple locations.

- **2024-10-09**: Simplified marketplace.json to match official spec.
  Learning: Stick to the official spec to avoid confusion and compatibility issues.
```

**Source:** `/CLAUDE.md`

---

#### 8. Agent Domain Organization

**What:** Organize agents into domain subdirectories (research/, design/, review/, workflow/, docs/).

**Why it's valuable:** Makes large agent collections navigable. Clarifies agent purpose by location. Enables targeted loading.

**Implementation:**
```
agents/
├── research/           # External knowledge gathering
│   ├── best-practices-researcher.md
│   ├── framework-docs-researcher.md
│   └── git-history-analyzer.md
├── design/             # Design-to-code bridge
│   ├── figma-design-sync.md
│   └── design-iterator.md
├── review/             # Multi-dimensional code quality
│   ├── security-sentinel.md
│   ├── performance-oracle.md
│   └── kieran-rails-reviewer.md
└── workflow/           # Operational tasks
    ├── lint.md
    └── pr-comment-resolver.md
```

**Source:** `plugins/compound-engineering/agents/`

---

### Standard Patterns (Well-Implemented)

| Pattern | Implementation | Notes |
|---------|----------------|-------|
| Progressive disclosure | Skill descriptions load first, body on trigger | 15 skills follow this pattern |
| Tool restrictions | Agents specify minimal tool sets | Most agents inherit or specify explicitly |
| Semver versioning | MAJOR/MINOR/PATCH rules documented | Enforced in plugin CLAUDE.md |
| Pre-commit checklists | 5-item verification before commits | Both CLAUDE.md files |
| YAML frontmatter | Commands use name, description, argument-hint | Consistent across 24 commands |

---

### Anti-Patterns Detected

| Anti-Pattern | Location | Recommendation |
|--------------|----------|----------------|
| No hooks defined | Entire plugin | Consider adding PostToolUse hooks for auto-formatting |
| Agent count mismatch | plugin.json vs actual files | Count verification should be automated |
| Some skills lack triggers | Reference-only skills | Add trigger keywords for auto-activation |

---

## Workflow Analysis

### Primary Workflows

**The "Happy Path" for Feature Development:**

```
brainstorm → plan → deepen-plan → work → review → compound
    ↓           ↓         ↓          ↓       ↓         ↓
 Clarity    Structure  Research   Execute  Quality  Document
```

**The `/lfg` (Let's F***ing Go) Command:**
Chains the entire workflow: plan → deepen-plan → work → review → resolve_todo_parallel → test-browser → feature-video

### Orchestration Style

- **Composition:** Hierarchical with extreme parallelization
- **Automation:** Semi-automatic (workflows trigger, then spawn autonomous agents)
- **State Management:** File-based (plans, todos, solutions stored as markdown with YAML frontmatter)

---

## Quality Assessment

### Strengths

1. **Extreme parallelization** - Commands spawn 20-40+ agents for maximum throughput
2. **Domain-organized agents** - Clear specialization and navigability
3. **Compounding knowledge system** - Solutions documented for future reference
4. **Namespace prefixing** - Prevents command collisions
5. **Validation gates in skills** - Explicit failure points ensure data integrity
6. **Personified expert agents** - Opinionated, consistent feedback

### Areas for Improvement

1. **No hooks defined** - Missing opportunity for automatic validation
2. **Agent count verification** - Should be automated, not manual
3. **Some skills lack triggers** - Reference skills could still benefit from keywords

### Unique Contributions

This repository demonstrates the most sophisticated multi-agent orchestration pattern discovered:
- **Parallel-first design:** Everything that can run in parallel does
- **Knowledge compounding:** Every solved problem becomes searchable institutional knowledge
- **Expert personas:** Agents embody specific philosophies for opinionated reviews
- **Validation gates:** Explicit blocking points in skill workflows

---

## GROK Integration Opportunities

| Finding | GROK Section | Integration Type |
|---------|--------------|------------------|
| Namespace prefixing | Part 9 (Bootstrapping) | New subsection |
| Validation gates in skills | Part 2.2 (Skills) | Add pattern |
| Decision menus post-workflow | Part 2.2 (Skills) | Add pattern |
| Extreme parallelization | Part 5 (Generative) | New subsection |
| Personified expert agents | Part 2.3 (SubAgents) | Add pattern |
| Hierarchical CLAUDE.md | Part 2.1 (CLAUDE.md) | Add example |
| Domain-organized agents | Part 2.3 (SubAgents) | Add pattern |
| Compounding knowledge workflow | Part 9 (Bootstrapping) | New subsection |

**Full GROK delta saved to:** `analyses/compound-engineering-plugin-grok-delta.md`

---

## Learnings for CLAUDE.md

Rules worth capturing:

```markdown
## Learned from compound-engineering-plugin

- Use `workflows:` prefix for commands to avoid built-in collisions
- Organize agents into domain subdirectories (research/, design/, review/, workflow/)
- Implement validation gates in skills for explicit failure points
- Spawn agents in parallel aggressively - 20-40+ is acceptable
- Name expert agents after the philosophy they embody
- Add timestamped learnings to CLAUDE.md for institutional memory
- Use decision menus post-workflow to enable branching paths
```

---

## Files Examined

<details>
<summary>Click to expand file list (100+ files)</summary>

**CLAUDE.md files:**
- /CLAUDE.md
- /plugins/compound-engineering/CLAUDE.md

**Skills (15):**
- /plugins/compound-engineering/skills/agent-browser/SKILL.md
- /plugins/compound-engineering/skills/file-todos/SKILL.md
- /plugins/compound-engineering/skills/agent-native-architecture/SKILL.md
- /plugins/compound-engineering/skills/compound-docs/SKILL.md
- /plugins/compound-engineering/skills/rclone/SKILL.md
- /plugins/compound-engineering/skills/andrew-kane-gem-writer/SKILL.md
- /plugins/compound-engineering/skills/every-style-editor/SKILL.md
- /plugins/compound-engineering/skills/skill-creator/SKILL.md
- /plugins/compound-engineering/skills/create-agent-skills/SKILL.md
- /plugins/compound-engineering/skills/brainstorming/SKILL.md
- /plugins/compound-engineering/skills/git-worktree/SKILL.md
- /plugins/compound-engineering/skills/dspy-ruby/SKILL.md
- /plugins/compound-engineering/skills/frontend-design/SKILL.md
- /plugins/compound-engineering/skills/gemini-imagegen/SKILL.md
- /plugins/compound-engineering/skills/dhh-rails-style/SKILL.md

**Agents (28):**
- /plugins/compound-engineering/agents/research/*.md (5)
- /plugins/compound-engineering/agents/design/*.md (3)
- /plugins/compound-engineering/agents/docs/*.md (1)
- /plugins/compound-engineering/agents/review/*.md (14)
- /plugins/compound-engineering/agents/workflow/*.md (5)

**Commands (24):**
- /plugins/compound-engineering/commands/*.md (19)
- /plugins/compound-engineering/commands/workflows/*.md (5)

**Plugin manifests:**
- /plugins/compound-engineering/.claude-plugin/plugin.json
- /plugins/coding-tutor/.claude-plugin/plugin.json
- /.claude-plugin/marketplace.json

</details>

---

*Generated by repo-analyzer skill*
*Report location: /Users/noveltokens/2026/claudeCodeDev/claude-code-living-doc/analyses/compound-engineering-plugin.md*
