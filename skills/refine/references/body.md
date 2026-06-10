# Refine Body

## What this produces

A `refinement.md` file next to the primary document, plus an iterative refinement loop that records answered refinements in the primary document, clears processed answers, and generates the next set of questions until none remain.

## Generate refinement process

1. Read the primary document and any supporting documents.
2. Identify every useful unresolved issue whose answer can change later decisions:
   - inconsistencies
   - contradictions
   - undefined terms
   - missing decisions
   - ambiguous ownership, scope, dates, success criteria, constraints, or dependencies
   - assumptions that would affect later implementation, planning, or review
3. Assign each question a priority:
   - `P0`: blocks understanding, scope, acceptance, security/compliance, contradiction resolution, or costly-to-reverse decisions.
   - `P1`: changes architecture, primary UX, data, integrations, planning, testing, or important technical risk.
   - `P2`: clarifies names, implementation details, or non-critical edge cases.
4. Assign each question one category:
   - `Business definition`
   - `Scope / acceptance`
   - `Contradiction`
   - `Security / compliance`
   - `Technical decision`
   - `Data / integration`
   - `Implementation detail`
5. Order questions by priority, then by category in the order listed above.
6. Do not ask implementation-detail questions while unresolved business, scope, acceptance, security, or contradiction questions can still change those implementation details.
7. Do not ask questions about details that can be safely inferred without changing later decisions.
8. Write every meaningful remaining question to `refinement.md` in the same directory as the primary document.
9. Include 2 to 5 concrete answer options for each question.
10. Include an empty `Answer:` field for each question.
11. Write `- None` under `Supporting documents:` when no supporting documents were provided.
12. Preserve existing unanswered questions and unprocessed answers in `refinement.md` when updating an existing refinement file.
13. Tell the user to answer the `Answer:` fields in `refinement.md` and invoke the skill again after answering.

## Process answered refinement process

1. Read the primary document, supporting documents if provided, and `refinement.md`.
2. Extract questions with non-empty `Answer:` fields.
3. Ignore unanswered questions.
4. If no questions are answered, tell the user and do not edit the primary document.
5. Add or update a section in the primary document named exactly:

```md
## Refinement resolutions
```

6. Append one bullet per answered question using this format:

```md
- **YYYY-MM-DD - <short topic>:** <decision>. Context: <ambiguity resolved>.
```

7. Preserve existing document structure and wording outside the resolution entries unless the user explicitly requests integration into the body.
8. Do not append duplicate resolutions for answers already represented in `## Refinement resolutions`.
9. If the user explicitly asks for no new questions, stop after recording the resolutions and do not regenerate `refinement.md`.
10. Otherwise, re-read the updated primary document and supporting documents.
11. Run the generate refinement process again.
12. Replace answered questions in `refinement.md` with newly found unresolved questions and still-unanswered prior questions.
13. If no unresolved questions remain, write a completion note in `refinement.md` and tell the user refinement is complete.
14. Tell the user which answered questions were recorded and which questions remain unanswered or newly added.

## Refinement file format

```md
# Refinement

This is a refinement file for `<primary-document-path>`.

Primary document:
- `<primary-document-path>`

Supporting documents:
- `<supporting-document-path>`

Use `- None` when no supporting documents were provided.

## Questions

### Q1 - <short topic>

Priority: P0
Category: Business definition

Question: <one concrete question>

Options:
1. <recommended or most conservative option>
2. <alternative option>
3. <alternative option>

Answer:
```

When refinement is complete, write:

```md
# Refinement

This is a refinement file for `<primary-document-path>`.

Primary document:
- `<primary-document-path>`

Supporting documents:
- `<supporting-document-path>`

## Status

No unresolved refinement questions remain.
```

## Gotcha list

**Mode selection:**
- Generate `refinement.md` unless the user says the refinement was answered, completed, filled, or ready to process.
- Do not ask interactive refinement questions while generating `refinement.md`.
- After processing answers, regenerate `refinement.md` before ending unless the user explicitly asks for no new questions.
- Treat answer options as suggestions, not an exhaustive set.

**Editing:**
- Create `refinement.md` only in the primary document directory.
- Do not overwrite existing answers in `refinement.md` before recording them in the primary document.
- Remove processed answered questions when regenerating `refinement.md` so the next iteration only asks unresolved questions.
- Do not rewrite the primary document as a proposal, plan, or implementation.
- Do not edit supporting documents unless the user explicitly names them as editable outputs.
- Keep every resolution traceable to a user answer.

**Assessment:**
- Prefer questions whose answers change scope, acceptance criteria, sequencing, ownership, risk, or implementation choices.
- Generate the broadest useful batch of questions in one pass, but discard questions that do not change later decisions.
- Order questions by `P0`, then `P1`, then `P2`.
- Within one priority, order categories as business definition, scope/acceptance, contradiction, security/compliance, technical decision, data/integration, then implementation detail.
- If the document contradicts itself, ask the user to choose the intended interpretation instead of reconciling it silently.
- If a missing detail can be safely inferred without affecting decisions, do not ask about it.
