# Phase {PHASE_NUMBER}: {PHASE_NAME}

**Parent Plan:** `context/plans/{DATE}-{TASK_NAME}.md`
**Date:** {DATE}
**Status:** Pending
**Dependencies:** {DEPENDENCIES}

---

## Phase Objective

[Clear, specific statement of what this phase accomplishes. Should be independently valuable and testable.]

---

## Scope

### In Scope

[What IS included in this phase]

- [Item 1]
- [Item 2]
- [Item 3]

### Out of Scope

[What is NOT included - will be handled in later phases]

- [Item 1]
- [Item 2]

---

## Implementation Steps

[Each step follows spec-driven TDD: confirm spec → write tests → implement → verify → commit.]

### Step 1: [Step Name]

[Description of what this step does]

- [Sub-task A]
- [Sub-task B]
- **Tests:** [Specific tests for this step]

### Step 2: [Step Name]

[Description of what this step does]

- [Sub-task A]
- [Sub-task B]
- **Tests:** [Specific tests for this step]

### Step 3: [Step Name]

[Description of what this step does]

- [Sub-task A]
- [Sub-task B]
- **Tests:** [Specific tests for this step]

[Add more steps as needed]

---

## Files to be Created/Modified

**New files:**
- `[path/to/new/file.ts]` - [Purpose]

**Modified files:**
- `[path/to/existing/file.ts]` - [What changes and why]

---

## Dependencies

### Prerequisites

[What must be complete before starting this phase]

- [Prerequisite 1]
- [Prerequisite 2]

### Enables Future Phases

[What this phase provides for later phases]

- [Item 1]
- [Item 2]

---

## Phase-Specific Risks

- **Risk 1:** [Description]
  - *Mitigation:* [How to handle]

- **Risk 2:** [Description]
  - *Mitigation:* [How to handle]

---

## Success Criteria

This phase is complete when:

- [ ] All implementation steps completed
- [ ] All new files created and properly structured
- [ ] Unit tests written and passing
- [ ] Manual testing completed successfully
- [ ] Code follows project conventions
- [ ] Ready for code review

---

**Next Step:** Once reviewed and approved, run `para-execute --phase={PHASE_NUMBER}` to begin implementation.
