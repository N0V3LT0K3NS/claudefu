# Infrastructure Audit Checklist

Use this checklist when analyzing a repository for Claude Code patterns.

## 1. CLAUDE.md Analysis

### Location Check
- [ ] Root `CLAUDE.md` exists
- [ ] Subdirectory `CLAUDE.md` files (domain-specific)
- [ ] Global reference (`~/.claude/CLAUDE.md` referenced)

### Content Analysis
- [ ] **Build/Run Commands** - How to build, test, run the project
- [ ] **Code Conventions** - Style, patterns, naming
- [ ] **Known Issues** - Gotchas, workarounds
- [ ] **Learned Rules** - Timestamped lessons from experience
- [ ] **Domain Context** - Project-specific knowledge
- [ ] **Tool Restrictions** - What not to do

### Quality Indicators
- [ ] Concise (under 500 lines recommended)
- [ ] Well-organized sections
- [ ] Append-only learning section
- [ ] No redundant content (offloaded to skills)

---

## 2. Skills Analysis

### Location Check
- [ ] `.claude/skills/*/SKILL.md` (project-level)
- [ ] `~/.claude/skills/*/SKILL.md` (global)
- [ ] Alternative patterns (`*.skill.md`, `skills/` without `.claude`)

### Frontmatter Analysis
For each skill, check:
- [ ] `name` - Unique, lowercase-hyphenated
- [ ] `description` - Clear "when to use" guidance
- [ ] `triggers` - Keywords for auto-activation
- [ ] `tools` - Appropriate restrictions
- [ ] `model` - Specified when needed (opus/sonnet/haiku)
- [ ] `context: fork` - Used for isolation when appropriate

### Structure Analysis
- [ ] Clear methodology/workflow
- [ ] Step-by-step instructions
- [ ] Expected outputs defined
- [ ] Supporting files (scripts, references, assets)

### Quality Indicators
- [ ] Progressive disclosure (description vs full content)
- [ ] Appropriate degrees of freedom
- [ ] Workflow patterns (checklist, feedback loop, conditional)
- [ ] Domain knowledge encoded

---

## 3. Agents Analysis

### Location Check
- [ ] `.claude/agents/*.md` (project-level)
- [ ] `~/.claude/agents/*.md` (global)
- [ ] Agent definitions in other locations

### Definition Analysis
For each agent, check:
- [ ] `name` - Clear specialization identity
- [ ] `description` - When/why to use (include examples)
- [ ] `tools` - Restricted to what's needed
- [ ] `model` - Cost/capability appropriate
- [ ] `skills` - Preloaded skills if needed

### Content Analysis
- [ ] Clear persona/role definition
- [ ] Specific instructions for the specialization
- [ ] Output format expectations
- [ ] Interaction patterns defined

### Quality Indicators
- [ ] Not overly broad (focused specialization)
- [ ] Tools minimized (principle of least privilege)
- [ ] Good examples in description
- [ ] Clear handoff expectations

---

## 4. Hooks Analysis

### Location Check
- [ ] `.claude/settings.json` (project-level)
- [ ] `~/.claude/settings.json` (global)
- [ ] `hooks/` directories with scripts

### Configuration Analysis
For each hook, check:
- [ ] Event type (PreToolUse, PostToolUse, Stop, etc.)
- [ ] Matcher pattern (regex or exact)
- [ ] Command being executed
- [ ] Decision logic (proceed, block, ask)

### Quality Indicators
- [ ] Clear purpose for each hook
- [ ] Not overly broad matchers
- [ ] Appropriate `once` usage
- [ ] Error handling in hook scripts

---

## 5. MCP Analysis

### Location Check
- [ ] `.mcp.json` (project-level)
- [ ] `~/.claude/settings.json` (global mcpServers)

### Configuration Analysis
For each server, check:
- [ ] Server type (stdio, SSE, HTTP)
- [ ] Command/URL configuration
- [ ] Environment variables handling
- [ ] Authentication patterns

### Quality Indicators
- [ ] Minimal exposed tools (only what's needed)
- [ ] Secure credential handling
- [ ] Clear purpose documentation

---

## 6. Commands Analysis

### Location Check
- [ ] `.claude/commands/*.md` (project-level)
- [ ] `~/.claude/commands/*.md` (global)

### Definition Analysis
For each command, check:
- [ ] Clear name (invoked as /name)
- [ ] Arguments defined if needed
- [ ] Workflow documented
- [ ] Output expectations

### Quality Indicators
- [ ] Namespace prefixing to avoid collisions
- [ ] Clear invocation examples
- [ ] Appropriate scope (not too broad)

---

## 7. Plugin Analysis

### Location Check
- [ ] `.claude-plugin/plugin.json` manifest
- [ ] Bundled components (skills/, agents/, commands/)

### Manifest Analysis
- [ ] Name and version
- [ ] Description
- [ ] Author information
- [ ] Component inventory

### Quality Indicators
- [ ] Proper namespacing
- [ ] Complete manifest
- [ ] All components documented

---

## 8. Pattern Detection

### Workflow Patterns
- [ ] **Sequential** - Step-by-step workflows
- [ ] **Parallel** - Multiple agents working simultaneously
- [ ] **Collaborative** - Handoffs between specialists
- [ ] **Feedback Loop** - Validate → fix → re-validate
- [ ] **Conditional** - Branching based on input

### Orchestration Patterns
- [ ] **Meta-orchestration** - Context-sharing before work
- [ ] **Progressive disclosure** - Load on demand
- [ ] **State management** - Files as persistence
- [ ] **Context hygiene** - Deliberate resets

### Learning Patterns
- [ ] **Append-only logs** - Timestamped learnings
- [ ] **Confidence scoring** - Tentative → core
- [ ] **Pattern extraction** - History → skills
- [ ] **Self-improvement** - Hooks that improve system

---

## 9. Anti-Pattern Detection

### CLAUDE.md Anti-Patterns
- [ ] Too long (>500 lines)
- [ ] Reference material that should be skills
- [ ] Outdated instructions
- [ ] Conflicting rules

### Skill Anti-Patterns
- [ ] Missing triggers
- [ ] Overly vague descriptions
- [ ] No workflow structure
- [ ] Unrestricted tools

### Agent Anti-Patterns
- [ ] Too broad specialization
- [ ] All tools enabled
- [ ] No clear handoff expectations
- [ ] Missing examples in description

### Hook Anti-Patterns
- [ ] Overly broad matchers (catch-all)
- [ ] No clear purpose
- [ ] Heavy processing that blocks
- [ ] Missing error handling

---

## 10. Summary Metrics

After audit, record:

| Metric | Count |
|--------|-------|
| CLAUDE.md files | |
| Skills | |
| Agents | |
| Hooks | |
| MCP servers | |
| Commands | |
| Plugins | |

| Quality | Rating |
|---------|--------|
| Overall sophistication | /5 |
| Documentation quality | /5 |
| Pattern maturity | /5 |
| Novel contributions | /5 |
