# pret-a-programming-skills

PARA workflow methodology as agent skills for any CLI tool that supports the [Agent Skills](https://agentskills.io) open standard. Ready-to-wear structured development.

**PARA:** Research -> Plan -> Review Plan -> Execute -> Review PR -> Summarize -> Archive

---

## What Is This?

The PARA-Programming methodology brings structured, plan-driven development to AI coding sessions. Instead of ad-hoc changes, every non-trivial task starts with research, gets planned collaboratively, undergoes Staff+ review, is executed with commit-per-todo discipline, and ends with a summary.

This repo packages that methodology as agent skills -- one skill per PARA workflow step, compatible with any CLI tool that supports the Agent Skills open standard (Codex CLI, Gemini CLI, etc.).

> **Claude Code user?** The original plugin lives at [para-programming-plugin](https://github.com/brian-lai/para-programming-plugin) and uses Claude Code slash commands.

---

## Skills

| Skill | Trigger Examples | Purpose |
|-------|-----------------|---------|
| `para-init` | "initialize PARA", "set up context directory" | Initialize PARA structure in a project |
| `para-research` | "research this codebase", "deep dive into" | Deep codebase exploration producing a research document |
| `para-plan` | "create a plan", "plan this task", "let's plan" | Create a planning document (collaborative) |
| `para-review` | "review the plan", "review this PR" | Staff+ independent agent review of plan or PR |
| `para-execute` | "execute the plan", "start implementing" | Create branch, extract todos, start execution with spec-driven TDD |
| `para-workflow` | "run the workflow", "orchestrate phases" | Orchestrate full multi-phase cycle automatically |
| `para-summarize` | "summarize work", "wrap up session" | Generate post-work summary document |
| `para-archive` | "archive context", "start fresh" | Archive context and create a clean slate |
| `para-status` | "what's the PARA status", "where are we" | Check current workflow state |
| `para-check` | "should I use PARA for this", "does this need a plan" | Decision helper: PARA or direct answer? |
| `para-help` | "para help", "how do I use PARA" | Show workflow overview and all skills |

---

## Installation

Skills are loaded from two locations:

- **User-global** (`~/.agents/skills/`) -- available in every project
- **Project-local** (`.agents/skills/`) -- available only in that project

### Option 1: User-global (recommended)

```bash
git clone https://github.com/brian-lai/pret-a-programming-skills.git ~/.agents/skills/para
```

This clones the entire repo into a `para/` subfolder inside your user skills directory. Your agent will discover all 11 skills automatically.

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

# 2. Research the codebase (optional but recommended)
para-research Add user authentication

# 3. Plan a task (collaborative -- agent will ask clarifying questions)
para-plan Add user authentication

# 4. Get Staff+ review of the plan
para-review --plan

# 5. Execute the plan
para-execute

# 6. Get Staff+ review of the implementation
para-review --pr

# 7. Summarize and archive
para-summarize
para-archive
```

For large tasks, use phased plans with automatic orchestration:

```
para-plan Add payment system      # -> choose phased plan
para-workflow --auto              # Orchestrates all phases: execute -> PR -> review -> merge
```

---

## File Structure

After `para-init`, your project will have:

```
context/
├── context.md       # Active session context (the master file)
├── plans/           # YYYY-MM-DD-task-name.md
├── summaries/       # YYYY-MM-DD-task-name-summary.md
├── archives/        # YYYY-MM-DD-HHMM-context.md
├── data/            # Input/output files, specs, research docs
└── servers/         # MCP tool wrappers
```

Skills are organized with co-located templates:

```
pret-a-programming-skills/
├── para-init/           # SKILL.md + METHODOLOGY.md + 4 templates
├── para-research/       # SKILL.md + research-template.md
├── para-plan/           # SKILL.md + 3 plan templates
├── para-review/         # SKILL.md
├── para-execute/        # SKILL.md
├── para-workflow/       # SKILL.md
├── para-summarize/      # SKILL.md + summary-template.md
├── para-archive/        # SKILL.md
├── para-status/         # SKILL.md
├── para-check/          # SKILL.md
└── para-help/           # SKILL.md
```

> Add `context/` to `.gitignore` -- it contains local-only work state.

---

## License

MIT
