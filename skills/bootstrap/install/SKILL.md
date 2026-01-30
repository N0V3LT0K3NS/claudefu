---
name: install
description: >-
  Sets up claudefu in a user's project. Creates necessary files,
  configures settings, and verifies installation.
triggers:
  - "install claudefu"
  - "set up claudefu"
  - "configure claudefu"
tools:
  - Read
  - Write
  - Bash
---

# Install

**Status:** 📋 Stub — Implementation coming soon

## Purpose

Install claudefu into a user's project with appropriate configuration.

## Intended Behavior

1. Check target project structure
2. Determine appropriate fu level (or use /assess)
3. Copy selected fu stack to project's .claude/
4. Update project's CLAUDE.md to reference claudefu
5. Verify installation works
6. Explain what was installed and how to use it

## Output

Configured claudefu installation in target project.
