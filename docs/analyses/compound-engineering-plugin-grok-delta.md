# GROK Delta: compound-engineering-plugin

**Generated:** 2026-01-27
**Source Repo:** https://github.com/EveryInc/compound-engineering-plugin

This document contains suggested additions to CLAUDE_CODE_GROK_ENRICHED.md based on analysis of the repository.

---

## Summary of Additions

| Section | Additions | Type |
|---------|-----------|------|
| Part 2: Mechanisms | 4 | Pattern additions |
| Part 5: Generative | 1 | New subsection |
| Part 6: Operational | 2 | New principles |
| Part 9: Bootstrapping | 3 | New subsections |
| Part 10: Resources | 1 | Repository reference |

---

## Part 2: The Six Mechanisms in Depth

### Section 2.1 (CLAUDE.md) - Hierarchical Organization

**Type:** Add example

**Location:** After "Best Practice" code block

**Content:**

```markdown
**Hierarchical CLAUDE.md for Monorepos:**

When managing multiple plugins or complex projects, use hierarchical CLAUDE.md files:

```
/CLAUDE.md                    # Marketplace/monorepo-wide constraints
/plugins/my-plugin/
  CLAUDE.md                   # Plugin-specific conventions
```

The root CLAUDE.md handles:
- Cross-plugin synchronization rules
- Component counting verification
- Marketplace metadata constraints

The plugin CLAUDE.md handles:
- Versioning requirements
- Command naming conventions
- Pre-commit checklists

This separation enables inheritance while maintaining focused scope.
```

**Rationale:** The compound-engineering-plugin demonstrates a sophisticated hierarchical approach that scales better than monolithic CLAUDE.md files for large projects.

**Source:** Repository structure analysis

---

### Section 2.2 (Skills) - Validation Gates

**Type:** Add pattern

**Location:** Under "Workflow Patterns in Skills"

**Content:**

```markdown
#### Validation Gates Pattern

For workflows where data integrity is critical, implement explicit blocking gates:

```markdown
<validation_gate name="yaml-schema" blocking="true">
Validate that YAML frontmatter matches schema before creating file.
If validation fails, STOP and report the error.
</validation_gate>
```

This pattern:
- Makes failure points explicit in the skill definition
- Prevents heuristic-based completion detection
- Ensures data integrity without relying on Claude's judgment
- Documents exactly where workflows can fail
```

**Rationale:** This pattern from compound-docs skill provides stronger guarantees than narrative instructions for error-prone operations.

**Source:** `plugins/compound-engineering/skills/compound-docs/SKILL.md`

---

### Section 2.2 (Skills) - Decision Menus

**Type:** Add pattern

**Location:** Under "Workflow Patterns in Skills"

**Content:**

```markdown
#### Decision Menu Pattern

Transform linear skills into branching workflows by presenting structured options after completion:

```markdown
## After Main Workflow

Present these options to the user:
1. Continue with current work
2. Promote to critical patterns library
3. Link to related GitHub issues
4. Add findings to existing skill
5. Create new skill from pattern
6. View all related documentation

Use AskUserQuestion to capture selection.
```

Benefits:
- Single skills serve multiple purposes
- Users direct next actions based on context
- Reusable infrastructure for different outcomes
```

**Rationale:** This pattern enables skills to handle branching user intent rather than requiring separate skills for each path.

**Source:** `plugins/compound-engineering/skills/compound-docs/SKILL.md`

---

### Section 2.3 (SubAgents) - Domain Organization

**Type:** Add pattern

**Location:** Under "Agent Definition Format"

**Content:**

```markdown
**Domain-Organized Agent Directories:**

For large agent collections (10+), organize by domain:

```
agents/
├── research/           # External knowledge gathering
│   ├── best-practices-researcher.md
│   └── framework-docs-researcher.md
├── design/             # Design-to-code bridge
│   ├── figma-design-sync.md
│   └── design-iterator.md
├── review/             # Multi-dimensional code quality
│   ├── security-sentinel.md
│   └── performance-oracle.md
└── workflow/           # Operational tasks
    ├── lint.md
    └── pr-comment-resolver.md
```

Benefits:
- Makes large collections navigable
- Clarifies agent purpose by location
- Enables targeted discovery
- Suggests natural groupings for parallel work
```

**Rationale:** With 28 agents, flat organization becomes unmanageable. Domain subdirectories scale better.

**Source:** `plugins/compound-engineering/agents/`

---

### Section 2.3 (SubAgents) - Personified Experts

**Type:** Add pattern

**Location:** Under "Architecture Patterns"

**Content:**

```markdown
#### Personified Expert Pattern

Name agents after the experts/philosophies they embody:

```yaml
---
name: dhh-rails-reviewer
description: |
  Reviews code from DHH/37signals perspective.
  Enforces Rails conventions, rejects JavaScript patterns.
---
You are a code reviewer channeling David Heinemeier Hansson's philosophy...
```

Examples:
- `dhh-rails-reviewer` - Rails conventions purist
- `kieran-typescript-reviewer` - Strict type safety advocate
- `julik-frontend-races-reviewer` - Race condition specialist

Benefits:
- Instant clarity on agent philosophy
- Consistent, opinionated feedback
- Natural language for invocation ("get DHH's opinion")
- Memorable naming
```

**Rationale:** Personified agents provide more consistent, opinionated reviews than generic "code-reviewer" agents.

**Source:** `plugins/compound-engineering/agents/review/`

---

## Part 5: Generative Capabilities

### Extreme Parallelization

**Type:** New subsection

**Location:** After "Emergent Patterns from Composition"

**Content:**

```markdown
### Extreme Parallelization Pattern

When throughput matters more than context efficiency, spawn many agents simultaneously:

```markdown
## Phase 2: Parallel Research

For EACH section in the plan, spawn in parallel:
- Task best-practices-researcher("[section topic]")
- Task framework-docs-researcher("[relevant frameworks]")
- Task learnings-researcher("[section topic]")
- [All discovered skills]
- [All relevant review agents]

Do NOT wait between spawns - launch all simultaneously.
```

**When to use:**
- Research phases (many independent queries)
- Code review (multiple dimensions to analyze)
- Plan deepening (many sections to enrich)
- TODO resolution (each item is independent)

**Scale guidance:**
- 5-10 agents: Normal parallel work
- 20-40 agents: Aggressive research/review phases
- 40+ agents: Maximum throughput mode

**Considerations:**
- Each agent has isolated context (memory efficient)
- Results return asynchronously (synthesize after all complete)
- Cost scales linearly with agent count
- Wall-clock time dramatically reduced
```

**Rationale:** The compound-engineering-plugin routinely spawns 20-40+ agents, demonstrating that aggressive parallelization is viable and valuable.

**Source:** `plugins/compound-engineering/commands/deepen-plan.md`

---

## Part 6: Operational Principles

### Principle 10: Namespace Commands for Scale

**Type:** New principle

**Content:**

```markdown
### 10. Namespace Commands for Scale
Use prefixes like `workflows:` to organize commands and prevent collisions with built-ins:

```
commands/
├── test.md                   # Might conflict with built-in
└── workflows/
    └── test.md               # Invoked as /workflows:test - no conflict
```

Benefits:
- Clear ownership and purpose
- Prevents shadowing built-in functionality
- Scales to large command sets
- Enables command discovery by namespace
```

**Rationale:** As plugins grow, unprefixed commands inevitably collide. The `workflows:` pattern from compound-engineering-plugin prevents this elegantly.

**Source:** `plugins/compound-engineering/CLAUDE.md`

---

### Principle 11: Timestamp Your Learnings

**Type:** New principle

**Content:**

```markdown
### 11. Timestamp Your Learnings
Add dated entries to CLAUDE.md when discovering important patterns:

```markdown
## Key Learnings

- **2024-11-22**: Component counts were wrong in plugin.json.
  Learning: Always count actual files before updating descriptions.

- **2024-10-09**: Marketplace.json had non-spec fields.
  Learning: Stick to official specs to avoid compatibility issues.
```

Benefits:
- Creates institutional memory
- Prevents repeating mistakes
- Shows evolution of understanding
- Provides context for why rules exist
```

**Rationale:** Timestamped learnings from compound-engineering-plugin demonstrate how CLAUDE.md can capture hard-won lessons.

**Source:** `/CLAUDE.md`

---

## Part 9: Adaptive Bootstrapping

### Namespace Prefixing Pattern

**Type:** New subsection

**Location:** Under "Advanced Patterns Worth Understanding"

**Content:**

```markdown
#### 5. Namespace Prefixing for Commands

As plugin complexity grows, command name collisions become inevitable. Use namespace prefixes:

```
commands/
├── changelog.md              # Root utility commands
├── deploy-docs.md
└── workflows/                # Namespaced workflow commands
    ├── plan.md               # Invoked as /workflows:plan
    ├── work.md               # Invoked as /workflows:work
    └── review.md             # Invoked as /workflows:review
```

**Key insight:** The directory structure becomes the namespace. `workflows/plan.md` is invoked as `/workflows:plan`.

**When to use:**
- Plugin has 10+ commands
- Commands might shadow built-ins
- Clear categorization exists (workflows vs utilities)
- Multiple contributors add commands

**Alternative namespaces:**
- `db:` for database operations
- `deploy:` for deployment workflows
- `test:` for testing commands
- `docs:` for documentation generation
```

**Rationale:** compound-engineering-plugin's 24 commands stay organized through this pattern.

**Source:** `plugins/compound-engineering/CLAUDE.md`, `plugins/compound-engineering/commands/workflows/`

---

### Compounding Knowledge Workflow

**Type:** New subsection

**Location:** Under "Advanced Patterns Worth Understanding"

**Content:**

```markdown
#### 6. Compounding Knowledge Workflow

Create a closed loop where every solved problem becomes searchable institutional knowledge:

```
Problem Solved
     ↓
/workflows:compound           # Document the solution
     ↓
docs/solutions/[category]/    # Stored with YAML frontmatter
     ↓
learnings-researcher          # Future queries can find it
     ↓
/workflows:plan              # Auto-discovers relevant solutions
```

**Implementation:**

1. **Solution documentation skill** (`compound-docs`):
   - Auto-triggers on completion phrases ("that worked", "it's fixed")
   - Extracts context, solution, prevention strategies
   - Stores with category and tags in YAML frontmatter

2. **Learnings researcher agent**:
   - Searches `docs/solutions/` directory
   - Filters by frontmatter metadata
   - Returns relevant past solutions

3. **Plan workflow integration**:
   - Spawns learnings-researcher in parallel
   - Incorporates past solutions into new plans

**Key insight:** The loop is closed - solutions feed back into planning, reducing repeated problem-solving.
```

**Rationale:** This is the "compounding" in compound-engineering - every solved problem makes future work easier.

**Source:** Multiple files across the plugin

---

### Multi-Agent Review Architecture

**Type:** New subsection

**Location:** Under "Advanced Patterns Worth Understanding"

**Content:**

```markdown
#### 7. Multi-Agent Review Architecture

For comprehensive code review, spawn specialized agents in parallel rather than relying on a single generalist:

```
/workflows:review
     ↓
Parallel spawn (13+ agents):
├── kieran-rails-reviewer      # Language-specific quality
├── dhh-rails-reviewer         # Philosophy enforcement
├── security-sentinel          # OWASP, injection, secrets
├── performance-oracle         # Big O, N+1, memory
├── architecture-strategist    # SOLID, boundaries
├── code-simplicity-reviewer   # YAGNI, abstraction removal
├── data-integrity-guardian    # Migration safety, ACID
├── pattern-recognition        # Design patterns, anti-patterns
└── [5 more specialists]
     ↓
Conditional agents (if migration):
├── data-migration-expert
└── deployment-verification-agent
     ↓
Synthesis into prioritized findings (P1/P2/P3)
```

**Benefits:**
- Each agent has focused expertise
- Parallel execution minimizes wall-clock time
- Findings naturally categorized by domain
- Conditional agents avoid unnecessary work

**Severity mapping:**
- P1 (Critical): Blocks merge
- P2 (Important): Should fix before merge
- P3 (Nice-to-have): Consider for future
```

**Rationale:** The 14-agent review architecture demonstrates how parallel specialization beats single-agent generalization.

**Source:** `plugins/compound-engineering/commands/workflows/review.md`

---

## Part 10: Curated Resources

### Repository to Add

| Repository | What It Demonstrates |
|------------|---------------------|
| [compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) | 28 agents, 24 commands, 15 skills - sophisticated multi-domain orchestration with namespace prefixing, extreme parallelization, compounding knowledge workflows |

**Already added to Part 10 in GROK_ENRICHED.md.**

---

## Integration Checklist

- [ ] Review each suggestion for accuracy
- [ ] Check for redundancy with existing content
- [ ] Verify code examples work
- [ ] Maintain consistent tone with GROK document
- [ ] Update table of contents if sections added
- [ ] Update "Last Updated" date

---

## Raw Findings Reference

<details>
<summary>Structured findings data (JSON)</summary>

```json
{
  "repo": "compound-engineering-plugin",
  "analyzed": "2026-01-27",
  "findings": [
    {
      "section": "part_2_mechanisms",
      "subsection": "2.1 CLAUDE.md",
      "finding": "Hierarchical CLAUDE.md organization",
      "integration_type": "add_example",
      "source_file": "Repository structure"
    },
    {
      "section": "part_2_mechanisms",
      "subsection": "2.2 Skills",
      "finding": "Validation gates pattern",
      "integration_type": "add_pattern",
      "source_file": "skills/compound-docs/SKILL.md"
    },
    {
      "section": "part_2_mechanisms",
      "subsection": "2.2 Skills",
      "finding": "Decision menus pattern",
      "integration_type": "add_pattern",
      "source_file": "skills/compound-docs/SKILL.md"
    },
    {
      "section": "part_2_mechanisms",
      "subsection": "2.3 SubAgents",
      "finding": "Domain-organized agent directories",
      "integration_type": "add_pattern",
      "source_file": "agents/"
    },
    {
      "section": "part_2_mechanisms",
      "subsection": "2.3 SubAgents",
      "finding": "Personified expert agents",
      "integration_type": "add_pattern",
      "source_file": "agents/review/"
    },
    {
      "section": "part_5_generative",
      "subsection": "New",
      "finding": "Extreme parallelization pattern",
      "integration_type": "new_subsection",
      "source_file": "commands/deepen-plan.md"
    },
    {
      "section": "part_6_operational",
      "subsection": "New Principle 10",
      "finding": "Namespace commands for scale",
      "integration_type": "new_principle",
      "source_file": "CLAUDE.md"
    },
    {
      "section": "part_6_operational",
      "subsection": "New Principle 11",
      "finding": "Timestamp your learnings",
      "integration_type": "new_principle",
      "source_file": "CLAUDE.md"
    },
    {
      "section": "part_9_bootstrapping",
      "subsection": "Pattern 5",
      "finding": "Namespace prefixing for commands",
      "integration_type": "new_subsection",
      "source_file": "commands/workflows/"
    },
    {
      "section": "part_9_bootstrapping",
      "subsection": "Pattern 6",
      "finding": "Compounding knowledge workflow",
      "integration_type": "new_subsection",
      "source_file": "Multiple files"
    },
    {
      "section": "part_9_bootstrapping",
      "subsection": "Pattern 7",
      "finding": "Multi-agent review architecture",
      "integration_type": "new_subsection",
      "source_file": "commands/workflows/review.md"
    }
  ]
}
```

</details>

---

*Generated by repo-analyzer skill*
*Apply these suggestions by editing CLAUDE_CODE_GROK_ENRICHED.md manually after review*
