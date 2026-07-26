# Refine Body

## Artifacts

- Maintain `refinement.md` next to the primary document.
- Record processed answers under `## Refinement resolutions` in the primary document.
- Treat supporting documents as read-only unless the user explicitly names them as editable outputs.

## Levels

Process these levels in order:

1. `L1 — Business requirements and contradictions`: goals, scope, actors, terminology, business rules, constraints, ownership, priorities, and acceptance outcomes. Ask only about contradictions or missing decisions at this level.
2. `L2 — Strategic architecture`: system boundaries, major components and responsibilities, integrations, data ownership, deployment model, quality attributes, technology constraints, and guiding principles. Include architectural contradictions; exclude detailed interfaces, schemas, classes, and algorithms.
3. `L3 — Detailed tactical design`: concrete APIs and contracts, schemas, modules, classes, control and state flows, validation, error handling, concurrency, algorithms, and other implementation-level design decisions.

Exactly one level is active unless all levels are complete. A run may generate or process questions only for the level active at its start. It may activate the next level at the end, but must not generate questions for that level until the next run.

If work at a later level exposes an unresolved dependency from an earlier level, reopen the earliest affected level, lock subsequent levels for re-evaluation, preserve recorded resolutions, and stop without asking later-level questions.

## Process

1. Select mode: process answers when the user says they are answered, completed, filled, or ready; otherwise generate or update questions.
2. Read the primary document, every supporting document, existing `## Refinement resolutions`, and `refinement.md` when present.
3. Create or update the document inventory with each path, its primary or supporting role, its title, and its document type when stated or evident. Otherwise use `Unclassified`.
4. Initialize missing progress with `L1` active and `L2` and `L3` locked.
5. For legacy questions without a level, assign each to the earliest matching level without changing its wording or answer, then activate the earliest incomplete level.
6. Operate only on the active level.

## Generate questions

1. Find unresolved decisions and contradictions within the active level only.
2. Skip matters already answered by the documents or recorded resolutions.
3. Turn contradictions into explicit choice questions; do not reconcile them silently.
4. Ask the broadest useful batch for the active level and keep conditional follow-ups within that level.
5. Use level-independent priority:
   - `P0`: blocks completion of the active level.
   - `P1`: materially affects decisions at the active level.
   - `P2`: useful non-blocking clarification.
6. Order questions by priority and dependency.
7. Cite the source documents and sections that caused each question. Use `path#heading` or `path:line` when no heading is available.
8. Give each question 2 to 5 concrete options and an empty `Answer:` field.
9. Preserve unanswered questions and unprocessed answers from the active level.

If no unresolved or new questions remain, mark the active level complete, activate the next level or mark all levels complete, and stop.

## Process answers

1. Process non-empty `Answer:` fields from the active level only.
2. Append non-duplicate resolution bullets under `## Refinement resolutions`:

```md
- **YYYY-MM-DD — <level> — <short topic>:** <decision>. Context: <ambiguity resolved>. Sources: <source locators>.
```

3. Preserve primary document wording outside `## Refinement resolutions` unless the user asks to integrate answers into the body.
4. Remove processed questions from `refinement.md`; preserve unanswered questions.
5. Re-evaluate the same level and generate another same-level batch when needed.
6. If the level has no unresolved or new questions, mark it complete, activate the next level or mark all levels complete, and stop without generating next-level questions.
7. If the user requests no new questions, record the answers, leave the current level active with re-evaluation pending, and do not advance.

## `refinement.md` format

```md
# Refinement

Primary document:
- `<primary-document-path>`

## Documents

- `<path>` — Primary | Supporting — Title: `<title>` — Type: `<type or Unclassified>`

## Level progress

- Active level: L1 | L2 | L3 | Complete
- L1 — Business requirements and contradictions: active | locked | complete
- L2 — Strategic architecture: active | locked | complete
- L3 — Detailed tactical design: active | locked | complete

## Questions

### L1-Q1 — <short topic>

Level: L1 — Business requirements and contradictions

Priority: P0 | P1 | P2

Sources:
- `<path#heading or path:line>`

Question: <one concrete question>

Options:
1. <recommended or conservative option>
2. <alternative option>

Answer:
```

Use `L2-Q1` and `L3-Q1` numbering at their respective levels. Omit `## Questions` when none remain and write:

```md
## Status

<completed level> is complete. <next level> is active and will be evaluated on the next run.
```

When all levels are complete, write:

```md
## Status

All refinement levels are complete.
```

## Gotchas

- Record answered questions before removing them.
- Keep each resolution traceable to its level, user answer, and sources.
- Treat answer options as suggestions, not exhaustive choices.
- When provided documents change or new documents are added, reopen the earliest level affected by the new material.
- Do not rewrite the primary document as a proposal, plan, or implementation.
