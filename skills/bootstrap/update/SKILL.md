---
name: update
description: >-
  Updates an existing claudefu installation with latest changes.
  Handles migrations and preserves customizations.
triggers:
  - "update claudefu"
  - "upgrade claudefu"
  - "claudefu has updates"
tools:
  - Read
  - Write
  - Bash
---

# Update

**Status:** 📋 Stub — Implementation coming soon

## Purpose

Update claudefu installation while preserving user customizations.

## Intended Behavior

1. Check current installation version
2. Check for available updates
3. Backup current configuration
4. Apply updates
5. Migrate any changed configurations
6. Preserve user customizations
7. Verify updated installation
8. Report what changed

## Output

Updated claudefu installation with migration notes.
