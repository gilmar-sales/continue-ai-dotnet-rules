---
globs: "**/*"
description: Strict Progress Tracking Protocol using PLAN.md
alwaysApply: true
---

# Progress Tracking Protocol (PLAN.md)

This ruleset enforces the maintenance of a `PLAN.md` file to track project progress, manage context, and ensure sequential execution of tasks.

## 1. The Single Source of Truth: `PLAN.md`
* **Existence:** A file named `PLAN.md` must exist in the root of the solution at all times.
* **Format:** The file must contain a Markdown checklist of all project phases and their sub-tasks.
* **State:** The state of the project is defined *solely* by the checked (`[x]`) or unchecked (`[ ]`) status of items in this file.

## 2. Execution Workflow
* **Read-First:** Before generating any code or commands, read `PLAN.md` to determine the current active task.
* **Sequential Execution:** Do not skip steps. Complete the current unchecked item before moving to the next.
* **Atomic Updates:** Update `PLAN.md` immediately after completing a task or a logical group of tasks within a response.

## 3. Response Structure
Every response involving code generation or project modification must follow this structure:

### A. Context Assessment
1.  **Current Phase:** State clearly which phase/task is currently being addressed.
2.  **Plan Status:** Briefly reference the pending item from `PLAN.md`.

### B. Implementation
1.  **Code/Commands:** Provide the necessary CLI commands or source code.
2.  **Verification:** Ensure the code compiles and aligns with the Clean Architecture constraints.

### C. Protocol & Context Update (Mandatory Footer)
At the very end of the response, include a section titled **"## Protocol & Context Update"** containing:

1.  **Updated `PLAN.md`:** Display the full content of `PLAN.md` with the just-completed tasks marked as `[x]`.
2.  **Context Management:**
    * **Keep:** List files/concepts critical for the *next* step (e.g., "Keep `KanbanItem` entity for Repository implementation").
    * **Drop:** List files/concepts that are stable and can be unloaded to save tokens (e.g., "Drop `dotnet new` commands", "Drop `PLAN.md` initialization history").
3.  **Next Action:** Explicitly state the next immediate task from the checklist.

## 4. Initialization Template
If `PLAN.md` does not exist, initialize it with the following structure (customized for the specific project):

```markdown
# Project Plan: [Project Name]

## Phase 1: Project Scaffolding
- [ ] Initialize Solution (.sln)
- [ ] Create Projects (Domain, Infra, API)
- [ ] [Specific Task...]

## Phase 2: Domain Modeling
- [ ] [Specific Task...]

...