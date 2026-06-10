# Deslop Generate Acceptance Criteria Body

## What this produces

A testable acceptance criteria document at `<flow-folder>/docs/acceptance-criteria.md` derived from `<flow-folder>/docs/documentation.md`.

## Analysis process

1. Use `documentation.md` content from context when already available; otherwise read the file.
2. Extract user-visible outcomes, domain rules, constraints, edge cases, and non-goals from `documentation.md`.
3. Write acceptance criteria to:

```txt
<flow-folder>/docs/acceptance-criteria.md
```

4. Use this structure:

```md
# Acceptance Criteria

## Scope

## Criteria

### AC-001: <short outcome name>
Given <initial context>
When <action or event>
Then <observable result>

## Edge Cases

## Out of Scope
```

5. Number criteria sequentially as `AC-001`, `AC-002`, `AC-003`.
6. Keep each criterion independently testable by a human, automated test, or review checklist.
7. Return a completion summary that names `acceptance-criteria.md`.
8. Suggest running `$deslop-propose` to create one decision-ready proposal.
9. Suggest running `$deslop-brainstorm-proposals` when the user wants several lightweight solution options before choosing a proposal.

## Gotcha list

**Input:**
- Do not use the `background/` folder to create acceptance criteria.
- Do not continue when documentation is neither in context nor available in `documentation.md`.
- Do not read `documentation.md` before the validation process passes.
- Do not read `documentation.md` when its contents are already available in current context.
- Do not use `assumptions.md`; it is a trace document, not acceptance criteria input.

**Criteria:**
- Do not write implementation tasks, UI copy, architecture decisions, or solution proposals as acceptance criteria.
- Do not invent behavior that is not supported by `documentation.md`.
- Do not combine unrelated behaviors in one criterion.
- Do not use vague pass conditions such as "works correctly", "is user friendly", or "handles errors well".

**Output:**
- Include `Out of Scope` when `documentation.md` states exclusions or non-goals.
- Point the user to `$deslop-propose` and `$deslop-brainstorm-proposals` as valid next Deslop skills after acceptance criteria are complete.
