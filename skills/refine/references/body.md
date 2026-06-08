# Refine Body

## What this produces

A `refinement.md` file next to the primary document, plus an iterative refinement loop that records answered refinements in the primary document and generates the next set of questions until none remain.

## Generate refinement process

1. Read the primary document and any supporting documents.
2. Identify unresolved issues that can be answered by the user:
   - inconsistencies
   - contradictions
   - undefined terms
   - missing decisions
   - ambiguous ownership, scope, dates, success criteria, constraints, or dependencies
   - assumptions that would affect later implementation, planning, or review
3. Rank issues by downstream risk.
4. Write every meaningful question to `refinement.md` in the same directory as the primary document.
5. Include 2 to 5 concrete answer options for each question.
6. Include an empty `Answer:` field for each question.
7. Write `- None` under `Supporting documents:` when no supporting documents were provided.
8. Preserve existing unanswered questions and unprocessed answers in `refinement.md` when updating an existing refinement file.
9. Tell the user to answer the `Answer:` fields in `refinement.md` and invoke the skill again after answering.

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
- **YYYY-MM-DD - <short topic>:** <decision>. Context: <why this was asked or what ambiguity it resolves>.
```

7. Preserve existing document structure and wording outside the resolution entries unless the user explicitly requests integration into the body.
8. Do not append duplicate resolutions for answers already represented in `## Refinement resolutions`.
9. Re-read the updated primary document and supporting documents.
10. Run the generate refinement process again.
11. Replace answered questions in `refinement.md` with newly found unresolved questions and still-unanswered prior questions.
12. If no unresolved questions remain, write a completion note in `refinement.md` and tell the user refinement is complete.
13. Tell the user which answered questions were recorded and which questions remain unanswered or newly added.

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

Question: <one concise question>

Why it matters: <what ambiguity this resolves>

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
- After processing answers, always regenerate `refinement.md` before ending.
- Treat answer options as suggestions, not an exhaustive set.

**Editing:**
- Create `refinement.md` only in the primary document directory.
- Do not overwrite existing answers in `refinement.md` before recording them in the primary document.
- Remove or mark processed answered questions so the next iteration only asks unresolved questions.
- Do not rewrite the primary document as a proposal, plan, or implementation.
- Do not edit supporting documents unless the user explicitly names them as editable outputs.
- Keep every resolution traceable to a user answer.

**Assessment:**
- Prefer questions whose answers change scope, acceptance criteria, sequencing, ownership, risk, or implementation choices.
- If the document contradicts itself, ask the user to choose the intended interpretation instead of reconciling it silently.
- If a missing detail can be safely inferred without affecting decisions, do not ask about it.
