# Deslop Plan PRs Body

## What this produces

A sequential PR execution plan under `<flow-folder>/plan/` with `PLAN.md`, PR folders, PR READMEs, and atomic task files.

## Planning process

1. Use the completed proposal from context when already available; otherwise read only the selected proposal file.
2. Use `documentation.md` content from context when already available; otherwise read the file.
3. Use `acceptance-criteria.md` content from context when already available; otherwise read the file.
4. Read source project files only when needed to avoid an impossible or vague task breakdown.
5. Detect objectives, constraints, risks, dependencies, affected surfaces, and validation commands.
6. Split the work into small sequential PRs with low coupling.
7. Split each PR into atomic tasks that a simple agent can execute without broad design decisions.
8. Create the plan folder:

```txt
<flow-folder>/plan/
```

9. Write this minimum structure:

```txt
<flow-folder>/plan/
  PLAN.md
  pr-1-<slug>/
    README.md
    task-01-<slug>.md
    task-02-<slug>.md
  pr-2-<slug>/
    README.md
    task-01-<slug>.md
```

10. Include in `PLAN.md`:
- Overall objective.
- Folder, filename, and numbering conventions.
- Ordered PR map with objective, risk, and relative complexity.
- Execution rules for the implementing agent.
- Validation commands between PRs, adapted to the project stack.

11. Include in each PR `README.md`:
- PR objective.
- Preconditions.
- Frozen decisions, when applicable.
- Ordered task list with relative task complexity.
- Acceptance criteria.
- `No hacer`.

12. Include in each `task-NN-<slug>.md`:
- Clear atomic title.
- Minimal context.
- Preconditions, when applicable.
- Files to read, create, and modify.
- Concrete sequential verifiable steps.
- TDD instructions when the task creates or changes testable logic.
- Relative complexity: `S`, `M`, or `L`.
- Verifiable milestone.
- Done criterion.
- `No hacer`.

13. Review numbering, filenames, internal references, and PR order before ending.
14. Return a summary with the generated folder, number of PRs, total task count, and important assumptions.
15. Tell the user the plan is ready for implementation PR by PR.

## Gotcha list

**Input:**
- Do not read proposal, documentation, or acceptance criteria files when their contents are already available in current context.
- Do not read every proposal file when the selected proposal is already explicit.
- Do not use the `background/` folder to create the plan.
- Treat unresolved items in `questions.md` as blockers unless the user explicitly chooses to continue.

**Output:**
- Write real files under `<flow-folder>/plan/`; do not only answer in chat.
- Do not invent an additional parent folder under `plan/`.
- Use Markdown and kebab-case filenames.
- Do not add empty sections.

**Planning:**
- Do not create implementation code.
- Do not create broad tasks that require design decisions from the executor.
- Preserve existing behavior unless the proposal explicitly asks for a bugfix or functional change.
- Document non-blocking assumptions briefly in the relevant plan file.
- Ask before writing files when an ambiguity blocks task decomposition.

**Tasks:**
- Each task must have a verifiable milestone independent of later tasks.
- Include TDD when a task creates or modifies testable logic.
- Omit TDD only for pure infrastructure or configuration tasks and say so explicitly.
- Split a task when it touches too many responsibilities.
