# pret-a-programming-skills

PARA workflow methodology as [Codex CLI](https://developers.openai.com/codex/cli/) agent skills. Ready-to-wear structured development.

**PARA:** Plan → Review → Execute → Summarize → Archive

---

## What Is This?

The PARA-Programming methodology brings structured, plan-driven development to AI coding sessions. Instead of ad-hoc changes, every non-trivial task starts with a plan, gets reviewed, is executed with commit-per-todo discipline, and ends with a summary.

This repo packages that methodology as Codex CLI skills — one skill per PARA workflow step.

> **Claude Code user?** The original plugin lives at [para-programming-plugin](https://github.com/brian-lai/para-programming-plugin) and uses Claude Code slash commands.

---

## Skills

| Skill | Trigger Examples | Purpose |
|-------|-----------------|---------|
| `para-init` | "initialize PARA", "set up context directory" | Initialize PARA structure in a project |
| `para-plan` | "create a plan", "plan this task", "let's plan" | Create a planning document (collaborative) |
| `para-execute` | "execute the plan", "start implementing" | Create branch, extract todos, start execution with spec-driven TDD |
| `para-summarize` | "summarize work", "wrap up session" | Generate post-work summary document |
| `para-archive` | "archive context", "start fresh" | Archive context and create a clean slate |
| `para-status` | "what's the PARA status", "where are we" | Check current workflow state |
| `para-check` | "should I use PARA for this", "does this need a plan" | Decision helper: PARA or direct answer? |
| `para-help` | "para help", "how do I use PARA" | Show workflow overview and all skills |

---

## Installation

Skills are loaded from two locations:

- **User-global** (`~/.agents/skills/`) — available in every project
- **Project-local** (`.agents/skills/`) — available only in that project

### Option 1: User-global (recommended)

```bash
git clone https://github.com/brian-lai/pret-a-programming-skills.git ~/.agents/skills/para
```

This clones the entire repo into a `para/` subfolder inside your user skills directory. Codex will discover all 8 skills automatically.

### Option 2: Project-local

```bash
mkdir -p .agents/skills
git clone https://github.com/brian-lai/pret-a-programming-skills.git .agents/skills/para
```

### Updating

```bash
cd ~/.agents/skills/para && git pull
```

---

## Quick Start

```
# 1. Initialize PARA in your project
para-init

# 2. Plan a task (collaborative — Claude will ask clarifying questions)
para-plan Add user authentication

# 3. Review the plan, then execute
para-execute

# 4. Work through todos (Claude commits after each one)

# 5. Summarize and archive
para-summarize
para-archive
```

For large tasks, use phased plans:

```
para-plan Add payment system      # → choose phased plan
para-execute --phase=1            # Phase 1 branch → PR → merge
para-execute --phase=2            # Phase 2 branch → PR → merge
para-summarize
para-archive
```

---

## File Structure Created

After `para-init`, your project will have:

```
context/
├── context.md       # Active session context (the master file)
├── plans/           # YYYY-MM-DD-task-name.md
├── summaries/       # YYYY-MM-DD-task-name-summary.md
├── archives/        # YYYY-MM-DD-HHMM-context.md
├── data/            # Input/output files, specs
└── servers/         # MCP tool wrappers
```

> Add `context/` to `.gitignore` — it contains local-only work state.

---

## License

MIT
