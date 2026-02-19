---
name: para-execute
description: >
  Execute the active PARA plan by creating a branch and working through todos with spec-driven TDD.
  Triggers on: "execute the plan", "implement the plan", "para execute", "start implementing",
  "begin execution", "run the plan", "let's implement".
---

# Skill: para-execute

Execute the active plan by creating a branch and tracking todos with spec-driven TDD. Supports both simple and phased plans.

## Usage

```
para-execute                    # Auto-detect plan; prompts for phase if phased
para-execute --phase=N          # Execute specific phase
para-execute --branch=name      # Custom branch name (simple plans only)
para-execute --no-branch        # Skip branch creation
```

## What to Do

1. Read the active plan from `context/context.md`
2. Detect simple vs phased plan (presence of `phased_execution` in JSON)
3. For phased plans:
   - If `--phase=N` is specified, verify all previous phases are complete
   - If not specified, prompt user which phase to execute
4. Create a git branch: `para/{task-name}` or `para/{task-name}-phase-N`
5. Extract implementation steps from the plan as todos
6. Update `context/context.md` with execution tracking format
7. Work through todos one by one following the Spec-Driven TDD cycle

## Prerequisites

- `context/context.md` must exist with an active plan
- If no active plan: "No active plan found. Run `para-plan` first."
- If dirty git state: warn user and offer to continue or stash first
- If target branch already exists: ask — continue on it or create with suffix?

## Context Update Format

Replace `context/context.md` with execution tracking format:

````markdown
# Current Work Summary

Executing: {Task Name}

**Branch:** `para/{task-name}`
**Plan:** context/plans/{plan-filename}

## To-Do List

- [ ] {Step 1 from plan}
- [ ] {Step 2 from plan}
- [ ] {Step 3 from plan}

## Progress Notes

_Update this section as you complete items._

---

```json
{
  "active_context": ["context/plans/{plan-filename}"],
  "completed_summaries": [],
  "execution_branch": "para/{task-name}",
  "execution_started": "{ISO timestamp}",
  "last_updated": "{ISO timestamp}"
}
```
````

For phased plans, also include `phased_execution` block with phase statuses and `current_phase: N`.

## Spec-Driven TDD Cycle (Mandatory for Every Todo)

**Committing after each todo is mandatory. Each todo follows a spec-first, tests-first cycle.**

Before starting any todo, verify that the active plan references a spec file (`context/data/*-spec.yaml` or equivalent contract). If missing, prompt the user to create the spec before proceeding.

For each todo:

1. **Confirm spec + stubs exist** — locate the stub source file(s) for this step. If stubs are missing (planning was skipped), create them now from the spec before writing tests.

2. **Write tests first** — based on the plan's `Tests:` annotation and the spec. Tests import the stub and assert expected behavior. Tests should **initially fail**.

3. **Implement** — replace stub bodies with real logic to make tests pass. Write the minimum code needed.

4. **Verify** — run the test suite to confirm **all** tests pass.

5. **Mark complete and commit:**
   - Mark the todo `[x]` in `context/context.md`
   - Stage changes: `git add -A`
   - Commit immediately with the todo text as the message

**Exception:** If a todo has no meaningful automated tests (e.g., config changes, documentation, template updates), note this in the commit and skip steps 1–4.

When all todos are complete, run `para-summarize`.

## Edge Cases

- **No implementation steps in plan:** Prompt user to provide todos manually
- **Multiple active plans:** Ask user which one to execute
- **Branch already exists:** Ask — continue on existing branch, create with suffix, or cancel?
- **Todo too large:** Break it into smaller sub-items before implementing

## Notes

- Branch naming follows `para/{task-name}` for easy identification
- For phased plans, each phase branches from `main` (assuming previous phases are merged)
- Run `para-status` anytime to see current progress
- The spec-driven TDD cycle ensures implementation is grounded in an agreed-upon contract before any code is written
