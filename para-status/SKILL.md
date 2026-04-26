---
name: para-status
description: >
  Display the current PARA workflow state and suggest the next action. Triggers on:
  "what's the para status", "show workflow state", "para status",
  "where are we in the workflow", "what's our current task", "show me the context".
---

# Skill: para-status

Display the current state of PARA context and workflow progress.

## Usage

```
para-status                  # Show current workflow state
para-status --verbose        # Include preview of active plan file contents
para-status --files          # List all context files with dates
```

## What to Do

1. **Check if `context/context.md` exists.** If not, output:
   ```
   No PARA context found.
   Next: Run para-init to initialize PARA in this project.
   ```
   Then stop.

2. **Read and parse `context/context.md`:**
   - Human-readable summary section (above the JSON block)
   - JSON block: `active_context`, `completed_summaries`, `research_docs`, `last_updated`, `phased_execution`, `workflow` (if present)

3. **Check git status** for uncommitted changes (run `git status --short`)

4. **Determine workflow state** and next action:
   - **Idle** (`active_context` is empty, no `research_docs`) -> suggest `para-research` or `para-plan`
   - **Researching** (`research_docs` present, `active_context` is empty) -> "Research complete. Run `para-plan` to create an implementation plan using the research."
   - **Planning** (`active_context` has a plan, no `execution_branch`) -> "Run `para-review --plan` for Staff+ review, then `para-execute`"
   - **Executing** (`execution_branch` present, todos in context) -> "Continue working through todos, or run `para-summarize` when done"
   - **Workflow Active** (`workflow` object present) -> "Workflow in progress: phase {current_phase}, step {current_step}. Run `para-workflow` to resume."
   - **Summarized** (`completed_summaries` updated, `active_context` empty) -> suggest `para-archive`

5. **Display output:**

```
PARA Status

Current Work:
   {human-readable summary from context.md}

Active Plans:
   {list of active_context entries, or "None"}

Research Docs:
   {list of research_docs, or "None"}

Completed Summaries:
   {list of completed_summaries, or "None"}

Last Updated: {last_updated timestamp}

{If workflow present:}
Workflow:
   Mode: {mode}
   Phase {current_phase}, Step: {current_step}
   Completed: {phases_completed}

{If phased_execution present:}
Phase Progress:
   Phase 1: complete
   Phase 2: in_progress  ← current

Uncommitted Changes: {Yes/No — file count if yes}

Next Action:
   {Suggested next step}
```

## Flags

- `--verbose`: After the status block, print the first 20 lines of each active plan file
- `--files`: List all files in `context/plans/`, `context/summaries/`, and `context/archives/` with modification dates

## Notes

- This skill is read-only -- it never modifies any files
- Run this anytime to reorient yourself in the workflow
