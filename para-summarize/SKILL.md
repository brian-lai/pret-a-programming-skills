---
name: para-summarize
description: >
  Generate a post-work summary document for the current PARA session. Triggers on:
  "summarize work", "write summary", "wrap up session", "para summarize",
  "create a summary", "summarize this phase", "summarize what we did".
---

# Skill: para-summarize

Generate a summary document from the current work session. Supports both simple and phased plans.

## Usage

```
para-summarize                   # Auto-detect active plan/phase
para-summarize --phase=N         # Summarize specific phase
```

## What to Do

1. **Read `context/context.md`** to find the active plan and current phase (if phased)
2. **Run `git diff` and `git log`** to analyze what changed:
   - Files modified, added, deleted
   - Commit messages from this branch
3. **Determine the summary filename:**
   - Simple plan: `context/summaries/YYYY-MM-DD-task-name-summary.md`
   - Phased plan: `context/summaries/YYYY-MM-DD-task-name-phase-N-summary.md`
4. **Create the summary file** using the template in `para-init/assets/templates/summary-template.md` with these sections:
   - **Date & Status** — when completed, success/failure
   - **Changes Made** — files modified/created with descriptions
   - **Rationale** — why these changes were made (reference the plan)
   - **MCP Tools Used** — any preprocessing tools utilized (or "None")
   - **Key Learnings** — insights, gotchas, follow-up tasks
   - **Test Results** — pass/fail status, coverage (or "N/A — documentation only")
5. **Update `context/context.md`:**
   - Move plan from `active_context` to `completed_summaries`
   - For phased plans, mark the phase `status` as `"complete"` in `phased_execution`
   - Update `last_updated` timestamp
6. **Display:** "Summary written to `context/summaries/{filename}`"

## After Summarizing

Run `para-archive` to clean up context and start fresh for the next task.

## Notes

- Use actual git output to populate "Changes Made" — do not guess file names
- For phased plans, only summarize the current phase's changes (use branch diff from phase start)
- If `--phase=N` is specified, verify it matches the active phase in `context/context.md`
