---
name: para-help
description: >
  Show the PARA workflow quick-reference guide with all available skills. Triggers on:
  "para help", "how do I use para", "what are the para commands",
  "show me para skills", "what can para do", "para overview".
---

# Skill: para-help

Display the PARA workflow quick-reference guide.

## Usage

```
para-help
```

## What to Do

Display the following reference guide exactly:

---

# PARA-Programming Quick Reference

**Workflow:** Plan → Review → Execute → Summarize → Archive

## When to Use PARA

**Use PARA** if the task results in git changes (features, bug fixes, refactoring, config, migrations, tests, complex debugging).

**Skip PARA** if the task is read-only or informational (questions, navigation, explanations).

## Skills

| Skill | Purpose |
|-------|---------|
| `para-init` | Initialize PARA structure in a project |
| `para-plan [task]` | Create a planning document (collaborative) |
| `para-execute` | Create branch, extract todos, start execution |
| `para-summarize` | Generate post-work summary |
| `para-archive` | Archive context and start fresh |
| `para-status` | Check current workflow state |
| `para-check` | Decision helper: should I use PARA for this? |
| `para-help` | Show this reference |

## Typical Flow

```
para-plan Add user authentication
  → Review the plan
  → AI implements (commits after each todo)
para-summarize
para-archive
```

For large tasks, use phased plans:
```
para-plan Add payment system   # (propose phased plan)
para-execute --phase=1         # Phase 1 branch → merge
para-execute --phase=2         # Phase 2 branch → merge
para-summarize
para-archive
```

## File Structure

```
context/
├── context.md       # Active session context
├── plans/           # YYYY-MM-DD-task-name.md
├── summaries/       # YYYY-MM-DD-task-name-summary.md
├── archives/        # YYYY-MM-DD-HHMM-context.md
├── data/            # Input/output files, specs
└── servers/         # MCP tool wrappers
```

## Tips

- Run `para-status` to see where you are in the workflow
- Run `para-check` if unsure whether a task needs PARA
- Full methodology details are in `~/.claude/CLAUDE.md`

---

## Notes

- This skill is read-only — it only displays information
- No files are created or modified when running para-help
