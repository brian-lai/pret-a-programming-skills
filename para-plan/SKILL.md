---
name: para-plan
description: >
  Create a PARA planning document through collaborative dialogue. Triggers on:
  "create a plan", "plan this task", "para plan", "plan out", "help me plan",
  "let's plan", "make a plan for", "I want to plan".
---

# Skill: para-plan

Create a planning document through collaborative dialogue, with support for multi-phase plans.

## Usage

```
para-plan [task-description]
```

If no task description is provided, ask for one.

## Collaborative Planning Process

**Planning is a dialogue, not a one-shot generation.**

### Step 1: Clarify

Identify ambiguities in the task description — scope, approach, constraints, preferences.

Ask **1-4 clarifying questions** before doing anything else:
- Present options with trade-offs clearly explained
- Reference existing codebase patterns when relevant ("I see you use X elsewhere, should we follow that?")
- Skip only if ALL of these are true: task is very narrow, only one reasonable approach exists, no risk of breaking changes, user gave extremely detailed requirements

### Step 2: Explore the codebase

With clarifications in hand, explore the project:
- Identify existing patterns, conventions, affected components, and complexity
- Find test patterns: framework, test file locations, naming conventions

### Step 3: Draft spec + stubs

Create a spec file in `context/data/YYYY-MM-DD-task-name-spec.yaml`:
- For HTTP APIs: OpenAPI/Swagger YAML
- For UI components, modules, scripts: TypeScript interface file or markdown contract

Create stub source files in the project tree with signatures matching the spec but no implementation (return `null`, `{}`, or `501 Not Implemented` as appropriate).

Reference the spec and stub file paths in the plan.

### Step 4: Determine plan type

- **Simple plan** (single file) for straightforward tasks
- **Phased plan** (master + sub-plans) when work spans >5-10 files, crosses architectural boundaries, or has natural dependency ordering
- If proposing a phased plan, confirm with the user first

### Step 5: Draft the plan

Create the plan file(s) using the templates in `para-init/assets/templates/`:
- Simple plan: `context/plans/YYYY-MM-DD-task-name.md` (use `plan-template.md`)
- Phased plan: `context/plans/YYYY-MM-DD-task-name.md` + phase sub-plans (use `phased-plan-master-template.md` and `phased-plan-sub-template.md`)

**Every implementation step MUST include a `Tests:` annotation** specifying what tests to write.

Include a Testing Strategy section with concrete, specific tests (not generic placeholders). Tests should reference actual functions, modules, and behaviors from the codebase.

### Step 6: Update context.md

After creating the plan, update `context/context.md`:
- Add plan file(s) to `active_context` array
- For phased plans, add `phased_execution` metadata:
  ```json
  {
    "phased_execution": {
      "master_plan": "context/plans/YYYY-MM-DD-task-name.md",
      "phases": [
        { "phase": 1, "plan": "context/plans/YYYY-MM-DD-task-name-phase-1.md", "status": "pending" },
        { "phase": 2, "plan": "context/plans/YYYY-MM-DD-task-name-phase-2.md", "status": "pending" }
      ],
      "current_phase": null
    }
  }
  ```
- Update `last_updated` timestamp

### Step 7: Ask to proceed

After the plan is written, ask the user if they'd like to proceed to implementation:
- "Yes, run `para-execute`" — proceed to implementation
- "I'd like to make adjustments first" — continue refining the plan

For phased plans, prompt: "Ready to run `para-execute --phase=1`?"

## Plan Structure

### Simple Plan

File: `context/plans/YYYY-MM-DD-task-name.md`

Sections:
- **Objective** — what needs to be done
- **Spec** — path to spec file and what it covers
- **Stubs** — list of stub source files and their locations
- **Approach** — step-by-step methodology
- **Risks** — potential issues and edge cases
- **Success Criteria** — measurable outcomes
- **Testing Strategy** — unit tests, integration tests, manual verification
- **Implementation Steps** — each step with `Tests:` annotation

### Phased Plan

Files:
- `context/plans/YYYY-MM-DD-task-name.md` — master plan: overall objective, phase breakdown, cross-phase risks, integration strategy
- `context/plans/YYYY-MM-DD-task-name-phase-1.md` — detailed implementation steps, phase-specific risks, success criteria
- `context/plans/YYYY-MM-DD-task-name-phase-2.md`
- etc.

Each phase should be independently reviewable and mergeable. Sub-plan implementation steps must include per-step `Tests:` annotations.

## Notes

- All project work MUST start with a plan (per PARA workflow)
- Master plans should be concise (1-2 pages); sub-plans should be implementation-ready
- Don't ask questions you could answer by reading the codebase
- Bias towards 2-4 focused questions, not 10+ scattered ones
- Default to asking questions — plans created collaboratively succeed more often than plans based on assumptions
