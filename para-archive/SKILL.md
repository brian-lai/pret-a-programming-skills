---
name: para-archive
description: >
  Archive the current PARA context and create a clean slate for the next task. Triggers on:
  "archive context", "start fresh", "reset para context", "para archive",
  "archive and start over", "clean up context", "wrap up and archive".
---

# Skill: para-archive

Archive the current context to create a clean slate for the next task.

## Usage

```
para-archive                 # Archive and create fresh context (default)
para-archive --fresh         # Completely empty context (no summary references)
para-archive --seed          # Carry forward relevant context from current session
```

## What to Do

1. **Check prerequisites:** Work should be summarized before archiving. If `active_context` is non-empty and no summary exists for the current task, warn the user: "It looks like this work hasn't been summarized yet. Run `para-summarize` first, or proceed anyway?"

2. **Get current timestamp** in `YYYY-MM-DD-HHMM` format (e.g., `2025-11-24-1430`)

3. **Move `context/context.md`** to `context/archives/YYYY-MM-DD-HHMM-context.md`

4. **Create a fresh `context/context.md`:**

   Default and `--fresh` behavior:
   ````markdown
   # Current Work Summary

   Ready for next task.

   ---
   ```json
   {
     "active_context": [],
     "completed_summaries": [
       "context/summaries/YYYY-MM-DD-*.md"
     ],
     "last_updated": "TIMESTAMP"
   }
   ```
   ````

   With `--seed`: carry forward the `completed_summaries` list and add a brief note about what was just completed.

   With `--fresh`: omit `completed_summaries` entirely (truly blank slate).

5. **Display confirmation:**
   ```
   Context archived to context/archives/YYYY-MM-DD-HHMM-context.md
   Fresh context.md created.
   Ready for next task — run para-plan to begin.
   ```

## When to Archive

- Work is complete and summarized
- All tests pass and changes are committed
- Ready to start a new, unrelated task

Do NOT archive if work is still in progress or you need the current context for continued work.

## Recovery

To restore a previous context:
```bash
ls -lt context/archives/           # List archives by date
cp context/archives/YYYY-MM-DD-HHMM-context.md context/context.md
```

## Notes

- Never delete archives — they are your project memory
- Archives are searchable: `grep -r "keyword" context/archives/`
- The `context/` directory should be in `.gitignore` — archives are local-only
