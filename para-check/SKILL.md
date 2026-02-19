---
name: para-check
description: >
  Decide whether the current request needs the PARA workflow or can be answered directly. Triggers on:
  "should I use PARA for this", "does this need a plan", "para check",
  "do I need to plan this", "is this a PARA task", "should I run para-plan".
---

# Skill: para-check

Decision helper to determine if the PARA workflow should be used for a given request.

## Usage

```
para-check "Add user authentication to the API"
para-check "Where is the auth middleware defined?"
```

If no request is provided, ask: "What task would you like me to evaluate?"

## Decision Logic

```
Does this request require code or file changes?
├─ YES → USE PARA (Plan → Review → Execute → Summarize → Archive)
└─ NO  → SKIP PARA
         ├─ About project code? → Direct answer with file references
         └─ General question?   → Standard response
```

**Use PARA** for tasks that result in git changes:
- New features or functionality
- Bug fixes that require code changes
- Refactoring or code cleanup
- Configuration file changes
- Database migrations
- Writing or updating tests
- Complex multi-step debugging that will produce fixes

**Skip PARA** for read-only or informational tasks:
- "What does X do?" / "How does Y work?"
- "Show me the auth logic"
- "Explain how caching is implemented"
- "Where is the config file?"
- Quick one-liner fixes (typo in a string, obvious constant change)

## Output Format

Display a short verdict with reasoning:

```
PARA Workflow Check

Request: "Add user authentication to the API"

  ✓ USE PARA WORKFLOW

Reason: This request requires code changes across multiple files.
Next: Run para-plan to create an implementation plan.
```

For skip cases:

```
PARA Workflow Check

Request: "Where is the auth middleware defined?"

  ✗ SKIP PARA — Answer directly

Reason: This is a read-only question with no file changes needed.
```

## Notes

- When in doubt, bias towards using PARA — the overhead of a plan is low, and it prevents wasted work
- If a task starts as informational but leads to fixes, switch to PARA at that point
