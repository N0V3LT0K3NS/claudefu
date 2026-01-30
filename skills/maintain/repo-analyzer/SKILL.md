---
name: repo-analyzer
description: |
  Analyzes repositories for Claude Code infrastructure patterns and lessons.
  Use when: "analyze this repo", "extract patterns", "what can we learn from this",
  "Claude Code infrastructure analysis", "show me the skills/agents in this repo".
triggers:
  - "analyze repo"
  - "repo patterns"
  - "infrastructure analysis"
  - "learn from this repo"
  - "extract claude patterns"
tools:
  - Read
  - Glob
  - Grep
  - Bash
  - WebFetch
  - Task
model: opus
---

# Repository Analyzer

Deep analysis of repositories for Claude Code infrastructure patterns, workflows, and learnings.

## Purpose

Extract reusable patterns, methodologies, and infrastructure designs from repositories that have invested in Claude Code tooling. The goal is learning transfer: identifying what works well in mature setups and adapting it for broader use.

## Workflow

### Phase 1: Acquisition

**Accept input as either:**
- Local path: `/path/to/repo`
- GitHub URL: `https://github.com/owner/repo`

**If GitHub URL:**
```bash
# Shallow clone for speed (no history needed for structure analysis)
git clone --depth 1 <url> /tmp/repo-analyzer-<timestamp>
```

**Validate structure exists before proceeding.**

### Phase 2: Infrastructure Detection

Run these scanners in parallel using the Task tool with Explore agents:

| Scanner | Target Pattern | What to Extract |
|---------|----------------|-----------------|
| skill-scanner | `**/SKILL.md`, `**/*.skill.md` | Frontmatter (name, description, triggers, tools, model), workflow steps, methodology |
| agent-scanner | `**/agents/*.md`, `.claude/agents/*.md` | Specializations, tool restrictions, model preferences, inter-agent relationships |
| hook-scanner | `**/settings.json`, `.claude/settings.json` | Event types, matchers, commands, decision logic |
| mcp-scanner | `**/.mcp.json`, `**/mcp*.json` | Server configs, endpoints, authentication patterns |
| command-scanner | `**/commands/*.md`, `.claude/commands/*.md` | Arguments, workflows, restrictions |
| claude-md-scanner | `**/CLAUDE.md` | Rules sections, learned rules, domain conventions |
| plugin-scanner | `**/.claude-plugin/plugin.json` | Plugin manifests, bundled components |

**For each scanner, capture:**
1. File paths found
2. Structured extraction of content
3. Relationships to other components
4. Notable patterns or anti-patterns

### Phase 3: Pattern Extraction

Using the infrastructure-audit checklist, identify:

**Novel Patterns** (things worth learning):
- Unique workflow compositions
- Creative use of mechanisms
- Effective orchestration strategies
- Domain-specific adaptations

**Standard Patterns** (well-implemented basics):
- Proper progressive disclosure
- Good description writing
- Appropriate tool restrictions
- Clean separation of concerns

**Anti-Patterns** (things to avoid):
- Overly broad agent definitions
- Missing triggers on skills
- Hooks without clear purpose
- Context-bloating CLAUDE.md

**Classify each pattern by taxonomy:**
- Workflow type (sequential, parallel, conditional, loop)
- Composition style (solo, collaborative, hierarchical)
- Automation level (manual, semi-auto, fully-automated)

### Phase 4: GROK Mapping

Map findings to GROK_ENRICHED.md sections:

| Finding Type | Maps To |
|--------------|---------|
| Meta-orchestration examples | Part 0 (Meta-Pattern) |
| Architecture decisions | Part 1 (Architecture) |
| Mechanism implementations | Part 2 (Mechanisms) |
| Decision patterns | Part 3 (Decision Matrix) |
| Workflow compositions | Part 5 (Generative) |
| Operational learnings | Part 6 (Principles) |
| Human collaboration patterns | Part 7 (For Human) |
| Template/bootstrap patterns | Part 9 (Adaptive Bootstrapping) |
| Resource references | Part 10 (Curated Resources) |

**For each mapping, specify:**
- What section it belongs to
- What specific insight it adds
- Whether it's a new pattern or an example of existing pattern
- Suggested prose for integration

### Phase 5: Synthesis

Generate two outputs:

**1. Analysis Report** (using analysis-report.md template)
- Executive summary with component counts
- Infrastructure inventory tables
- Pattern analysis with code examples
- Quality assessment
- Notable learnings

**2. GROK Delta** (using grok-delta.md template)
- Suggested additions organized by GROK section
- New patterns to document
- New examples to add
- Potential CLAUDE.md rules to capture

## Execution Notes

**Parallel where possible:**
- Phase 2 scanners run in parallel
- Phase 3 classification can run in parallel with mapping prep

**State management:**
- Create working directory: `/tmp/repo-analyzer-<repo-name>/`
- Save intermediate scanner outputs as JSON
- Final report saved to user-specified location or `analyses/<repo-name>.md`

**Context efficiency:**
- Use subagents for scanning (isolate context)
- Summarize findings before synthesis (don't keep raw files in context)
- Return structured summaries, not raw content

## Quality Criteria

A good analysis:
1. **Comprehensive** - Finds all Claude Code infrastructure
2. **Insightful** - Identifies patterns, not just files
3. **Actionable** - GROK delta contains usable suggestions
4. **Contextual** - Explains why patterns work
5. **Honest** - Notes anti-patterns and limitations

## Example Invocation

```
User: Analyze https://github.com/EveryInc/compound-engineering-plugin

Claude: I'll analyze this repository for Claude Code infrastructure patterns.

[Clones repo]
[Runs parallel scanners]
[Extracts patterns]
[Maps to GROK sections]
[Generates report and delta]

## Analysis Complete

**Summary:** 28 agents, 24 commands, 15 skills - sophisticated orchestration.

**Key patterns found:**
- Namespace prefixing (`workflows:`) to avoid collisions
- Multi-phase planning workflow
- Timestamped learnings in CLAUDE.md

**Report saved to:** analyses/compound-engineering-plugin.md
**GROK additions suggested:** 4 new patterns for Part 9
```

## Files in This Skill

- `checklists/infrastructure-audit.md` - What to look for
- `frameworks/pattern-taxonomy.json` - How to classify patterns
- `frameworks/grok-mapping.json` - Where findings go in GROK
- `templates/analysis-report.md` - Output structure for reports
- `templates/grok-delta.md` - Output structure for GROK suggestions
