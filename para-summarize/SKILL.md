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
4. **Create the summary file** using `summary-template.md` (co-located in this skill directory) with these sections:
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

## Standalone vs Workflow Invocation

**Standalone** (invoked manually by the user outside of `para-workflow`):
- After writing the summary, guide the user on next steps: push the branch, create a PR, run `para-review --pr` for Staff+ review
- Include push/PR guidance in the output

**Workflow** (invoked by `para-workflow` as part of the orchestrated cycle):
- The PR has already been created by the workflow orchestrator (Step 2)
- Skip the push/PR guidance -- `para-workflow` handles PR creation and review
- Just write the summary and update `context/context.md`

To detect which mode: check whether `context/context.md` contains a `workflow` object in its JSON metadata. If present, this is a workflow invocation.

## After Summarizing

Run `para-archive` to clean up context and start fresh for the next task.

## Notes

- Use actual git output to populate "Changes Made" — do not guess file names
- For phased plans, only summarize the current phase's changes (use branch diff from phase start)
- If `--phase=N` is specified, verify it matches the active phase in `context/context.md`
