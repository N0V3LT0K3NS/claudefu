# Source Registry

Central registry for sources that inform claudefu content.

---

## Structure

```
source-registry/
├── whitelist/           # Approved sources
│   ├── index.md         # Master list
│   └── L0-L5/           # By level
├── blacklist/           # Excluded sources
│   ├── index.md         # List with reasons
│   └── entries/         # Detailed exclusions
├── pending/             # Under evaluation
│   ├── index.md         # Pending list
│   └── entries/         # Evaluation in progress
└── schema/              # Templates and criteria
```

---

## How It Works

1. **Propose:** Add to `pending/` with evaluation
2. **Evaluate:** Review against criteria
3. **Decide:** Move to `whitelist/` or `blacklist/`
4. **Track:** Update status over time

---

## Using Sources

Sources inform fu content but aren't included directly. The flow:

```
Source → Digest → Synthesis → Fu Integration
```

See `/staging/` for processing pipeline.
