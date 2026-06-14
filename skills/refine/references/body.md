# Refine2 Body

## What this produces

A `refinement.md` file next to the primary document and recorded answer decisions in the primary document under `## Refinement resolutions`.

## Process

1. Select mode: process answered refinements when the user says answers are ready; otherwise generate or update `refinement.md`.
2. Read the primary document, supporting documents, and `refinement.md` when needed for the selected mode.

## Generate refinement

1. Ask the broadest useful batch of unresolved questions whose answers change scope, acceptance, sequencing, ownership, risk, implementation, or review; skip safely inferable details.
2. Turn contradictions into choice questions; do not reconcile them silently.
3. Use `P0` for blockers, `P1` for major design/planning risk, and `P2` for non-critical clarification.
4. Order by priority.
5. Include conditional follow-ups when they can be answered before knowing the first answer.
6. Preserve unanswered questions and unprocessed answers from existing `refinement.md`.
7. Write remaining questions with 2 to 5 concrete options and an empty `Answer:` field.

## Process answers

1. Extract non-empty `Answer:` fields.
2. Append non-duplicate resolution bullets under `## Refinement resolutions`:

```md
- **YYYY-MM-DD - <short topic>:** <decision>. Context: <ambiguity resolved>.
```

3. Preserve primary document wording outside `## Refinement resolutions` unless the user asks to integrate answers into the body.
4. Regenerate `refinement.md` unless the user asks for no new questions.
5. After recording answers in `## Refinement resolutions`, remove those answered entries from `refinement.md`.
6. Keep unresolved unanswered questions and write completion status when no unresolved questions remain.

## `refinement.md` format

```md
# Refinement

This is a refinement file for `<primary-document-path>`.

Primary document:
- `<primary-document-path>`

Supporting documents:
- `<supporting-document-path or None>`

## Questions

### Q1 - <short topic>

Priority: P0 | P1 | P2

Question: <one concrete question>

Options:
1. <recommended or conservative option>
2. <alternative option>

Answer:
```

When complete, replace `## Questions` with:

```md
## Status

No unresolved refinement questions remain.
```

## Gotcha list

- Do not overwrite answered questions before recording them.
- Do not leave processed answers in `refinement.md` after recording them.
- Do not edit supporting documents unless the user explicitly names them as editable outputs.
- Keep each recorded resolution traceable to a user answer.
- Treat answer options as suggestions, not exhaustive choices.
- Do not rewrite the primary document as a proposal, plan, or implementation.
