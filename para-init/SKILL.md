---
name: para-init
description: >
  Initialize the PARA workflow structure in the current project. Triggers on:
  "initialize PARA", "set up PARA workflow", "init para", "set up context directory",
  "initialize context structure", "start PARA in this project".
---

# Skill: para-init

Initialize the PARA-Programming workflow structure in the current project.

## Usage

```
para-init
para-init --template=basic    # Minimal project CLAUDE.md (default)
para-init --template=full     # Comprehensive project CLAUDE.md
```

## What to Do

1. **Set up global methodology file** at `~/.claude/CLAUDE.md`:
   - Read the methodology content from `para-init/assets/METHODOLOGY.md` (in this skills repo)
   - If `~/.claude/CLAUDE.md` does not exist, create it with that content
   - If it already exists, do NOT overwrite it — inform the user it was left intact

2. **Create context directory structure** in the current project:
   ```bash
   mkdir -p context/{data,plans,summaries,archives,servers}
   ```

3. **Create `context/context.md`** with initial structure:
   ````markdown
   # Current Work Summary

   Ready to start first task.

   ---
   ```json
   {
     "active_context": [],
     "completed_summaries": [],
     "last_updated": "TIMESTAMP"
   }
   ```
   ````
   Replace `TIMESTAMP` with the current ISO 8601 datetime.

4. **Create project `CLAUDE.md`** (if missing) from the appropriate template:
   - `--template=basic` (default): use `para-init/assets/templates/claude-basic-template.md`
   - `--template=full`: use `para-init/assets/templates/claude-full-template.md`
   - Replace `{PROJECT_NAME}` placeholder with the current directory name
   - If `CLAUDE.md` already exists, do NOT overwrite it — inform the user

5. **Display success output:**

```
PARA-Programming Structure Initialized

context/
├── archives/     # Historical context snapshots
├── data/         # Input files, payloads, datasets
├── plans/        # Pre-work planning documents
├── servers/      # MCP tool wrappers
├── summaries/    # Post-work reports
└── context.md    # Active session context

Files created/updated:
- ~/.claude/CLAUDE.md (global methodology, if it didn't exist)
- context/context.md (fresh context file)
- CLAUDE.md (project-specific context, if it didn't exist)

Next steps:
1. Edit CLAUDE.md with your project-specific context
2. Create your first plan: para-plan <task-description>
3. Get help with the PARA workflow: refer to ~/.claude/CLAUDE.md
```

## Notes

- The `context/` directory should be added to `.gitignore` — it contains local-only work state
- The `~/.claude/CLAUDE.md` file is global and shared across all projects
- Templates in `para-init/assets/templates/` are reference files read by this skill; they are not auto-installed into the project
