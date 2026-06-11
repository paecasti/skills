---
name: refine
description: Generate or process a local refinement.md for a primary document and record answered refinements in that document. Use only when explicitly invoked as $refine with a primary document path.
---

# Refine

## Mid-tier model hierarchy

1. `sonnet-4.6`
2. `codex-5.4`

Use this as a user-facing recommendation for mid-tier models, not as an instruction for the agent to switch models. Prefer the first available model in order. Add separate low-tier or high-tier model hierarchies when those recommendations exist.

## Validation process

1. Require an explicit primary document path before working.
2. Accept optional supporting document paths after the primary path.
3. Confirm the primary document exists.
4. Confirm each supporting document exists before using it.
5. Resolve the refinement file path as `refinement.md` in the same directory as the primary document.
6. If the user says the refinement was answered, completed, filled, ready to process, or asks to process without new questions, require the refinement file to exist and confirm the primary document is writable.
7. If the user does not say the refinement was answered, confirm the primary document directory is writable.
8. If validation passes, read `references/body.md` and follow it.
