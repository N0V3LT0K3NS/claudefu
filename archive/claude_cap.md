# Claude Code Documentation Links

> **Comprehensive Reference:** See [CLAUDE_CODE_GROK.md](./CLAUDE_CODE_GROK.md) for complete operational awareness - technical details + meta-understanding for Claude and human collaborators.

## Official Documentation (code.claude.com)

| Topic | URL |
|-------|-----|
| **Full Index (LLM-friendly)** | https://code.claude.com/docs/llms.txt |
| Overview | https://code.claude.com/docs/en/overview |
| **Features Overview (When to Use What)** | https://code.claude.com/docs/en/features-overview |
| **Sub-Agents** | https://code.claude.com/docs/en/sub-agents |
| **Skills** | https://code.claude.com/docs/en/skills |
| **Hooks** | https://code.claude.com/docs/en/hooks |
| Hooks Guide | https://code.claude.com/docs/en/hooks-guide |
| **MCP** | https://code.claude.com/docs/en/mcp |
| **Plugins** | https://code.claude.com/docs/en/plugins |
| Plugins Reference | https://code.claude.com/docs/en/plugins-reference |
| Memory | https://code.claude.com/docs/en/memory |
| Settings | https://code.claude.com/docs/en/settings |
| Best Practices | https://code.claude.com/docs/en/best-practices |
| CLI Reference | https://code.claude.com/docs/en/cli-reference |
| Headless/SDK | https://code.claude.com/docs/en/headless |
| IDE Integrations | https://code.claude.com/docs/en/ide-integrations |
| GitHub Actions | https://code.claude.com/docs/en/github-actions |
| Security | https://code.claude.com/docs/en/security |
| SDK | https://code.claude.com/docs/en/sdk |

## GitHub Resources

| Resource | URL |
|----------|-----|
| Claude Code Repo | https://github.com/anthropics/claude-code |
| Changelog | https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md |
| Official Skills Library | https://github.com/anthropics/skills |
| MCP Servers | https://github.com/modelcontextprotocol/servers |
| MCP Protocol | https://modelcontextprotocol.io |

## Community Resources

| Resource | URL |
|----------|-----|
| claude-code-docs (ericbuess) | https://github.com/ericbuess/claude-code-docs |
| **everything-claude-code** | https://github.com/affaan-m/everything-claude-code |
| Skills Best Practices | https://github.com/Dicklesworthstone/meta_skill/blob/main/BEST_PRACTICES_FOR_WRITING_AND_USING_SKILLS_MD_FILES.md |

### everything-claude-code: Bootstrap Template

**What it is:** A production-ready plugin from 10+ months of intensive daily use. Software engineering focused but **patterns are domain-agnostic**.

**Contains:**
- **Agents:** planner, architect, code-reviewer, security-reviewer, tdd-guide, e2e-runner
- **Skills:** coding-standards, backend-patterns, frontend-patterns, tdd-workflow, continuous-learning-v2
- **Commands:** /tdd, /plan, /code-review, /skill-create
- **Rules:** security.md, coding-style.md, testing.md, git-workflow.md
- **Hooks:** Session lifecycle, compaction handling, auto-formatting, validation

**Key Patterns to Learn:**

| Pattern | What It Does |
|---------|--------------|
| **Rules** | Mandatory constraints (distinct from CLAUDE.md guidance) |
| **Continuous Learning** | Instincts with confidence scores (0.3-0.9) that evolve into skills |
| **Iterative Retrieval** | Subagents progressively refine context (broad → narrow) |
| **Skill-Create** | Generate skills from git history (`/skill-create`) |

**How to Fork for Other Domains:**
1. Clone the repo
2. Map software roles → your domain roles (architect → strategist, reviewer → assessor)
3. Replace knowledge content, keep structural patterns
4. Use `/skill-create` on your existing work to bootstrap
5. Let the continuous learning system evolve your instincts

See **Part 9** of [CLAUDE_CODE_GROK.md](./CLAUDE_CODE_GROK.md) for detailed forking framework.

## Blog Posts & Articles

| Article | URL |
|---------|-----|
| Agent Skills (Anthropic Engineering) | https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills |
| Claude Skills (Simon Willison) | https://simonwillison.net/2025/Oct/16/claude-skills/ |
| Claude Skills Guide (Sid Bharath) | https://sidbharath.com/blog/claude-skills/ |

---

## Local Reference Documents

This repository contains comprehensive reference documents:

| Document | Purpose |
|----------|---------|
| **[CLAUDE_CODE_GROK.md](./CLAUDE_CODE_GROK.md)** | Complete operational awareness - the "I know kung fu" document for Claude and humans |
| [CLAUDE_CODE_TECHNICAL_CAPABILITIES.md](./CLAUDE_CODE_TECHNICAL_CAPABILITIES.md) | Pure technical reference with configuration formats |
| [LIVING_DOCUMENT_COMPLETE.md](./LIVING_DOCUMENT_COMPLETE.md) | Full synthesis with practitioner wisdom |
| [TECHNICAL_REFERENCE.md](./TECHNICAL_REFERENCE.md) | Architecture and patterns |
| [PRACTITIONER_WISDOM.md](./PRACTITIONER_WISDOM.md) | What people on the ground are discovering |

**Start here:** [CLAUDE_CODE_GROK.md](./CLAUDE_CODE_GROK.md)

---

## Agent Examples

See `~/.claude/agents/` for 100+ subagent definitions including:
- `agent-architect.md` — Design new agents
- `web-researcher.md` — Deep web research
- `code-simplifier.md` — Code simplification
- Various domain specialists

## Skill Examples

See `~/.claude/skills/` for skill packages:
- `comprehensive-lease-reviewing/` — Multi-agent legal analysis
- Various domain-specific skills

---

## Key Insight

> "Skills are potentially more significant than MCP... LLMs already excel at invoking CLI tools. Skills leverage this capability more elegantly." — Simon Willison

The real power is **composition**: Skills + SubAgents + MCP + Hooks working together, with Claude able to create and improve these mechanisms itself.
