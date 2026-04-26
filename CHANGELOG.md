# Changelog

All notable changes to this project will be documented in this file.

---

## [v1.1.0] - 2026-04-25

Achieves parity with [para-programming-plugin](https://github.com/brian-lai/para-programming-plugin) v2.2.0.

### Added
- **para-research** skill with co-located `research-template.md` -- deep codebase exploration producing structured research documents
- **para-review** skill -- independent Staff+ agent review for plans and PRs with 5-round convergence detection
- **para-workflow** skill -- multi-phase orchestrator with `--auto` mode (execute -> PR -> review -> summarize -> merge -> next phase)
- `context-schema.md` in para-init -- canonical JSON schema reference for `context/context.md` fields
- Self-review loop (2-3 rounds) in para-plan before presenting plans to users
- Staff+ engineering criteria in para-plan (core principles, architecture decisions, interface boundaries, graceful degradation)
- Standalone vs workflow invocation mode in para-summarize
- Template and schema cross-references in para-archive

### Changed
- **Templates co-located per skill** -- moved from centralized `para-init/assets/templates/` to each skill's own directory
- **METHODOLOGY.md flattened** -- moved from `para-init/assets/` to `para-init/`
- **Workflow upgraded to 7 steps** -- Research -> Plan -> Review Plan -> Execute -> Review PR -> Summarize -> Archive (was 5 steps)
- para-plan: added Core Principles, Architecture Decisions, Interface Boundaries, Graceful Degradation to plan structure; sharpened phase-split criteria to 3 concrete triggers; added research doc check
- para-plan templates: plan-template.md, phased-plan-master-template.md, phased-plan-sub-template.md updated with new sections
- para-execute: removed dead `--branch=name` and `--no-branch` flags; aligned TDD cycle to 6 steps (red/green distinction); added context-schema reference
- para-help: updated to show 11 skills and 7-step workflow
- README.md: updated for 11 skills with co-located template structure

### Infrastructure
- Added `LICENSE` (MIT)
- Added `CHANGELOG.md`

---

## [v1.0.0] - 2026-02-19

Initial release -- tool-agnostic translation of the PARA-Programming methodology.

### Added
- 8 skills: para-init, para-plan, para-execute, para-summarize, para-archive, para-status, para-check, para-help
- 7 templates: claude-basic-template, claude-full-template, context-template, plan-template, phased-plan-master-template, phased-plan-sub-template, summary-template
- METHODOLOGY.md with 5-step workflow (Plan -> Review -> Execute -> Summarize -> Archive)
- Branch-based execution workflow (`git checkout -b`)
- README with installation and usage documentation
