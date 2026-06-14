---
name: refine
description: Generate or process a local refinement.md for a primary document and record answered refinements in that document. Use only when explicitly invoked as $refine with a primary document path.
---

# Refine

## Mid-tier model hierarchy

1. `sonnet-4.6`
2. `codex-5.4`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit primary document path before working.
2. Accept optional supporting document paths after the primary path.
3. Confirm the primary document exists.
4. Confirm each supporting document exists before using it.
5. Resolve the refinement file path as `refinement.md` in the same directory as the primary document.
6. If the user says the refinement was answered, completed, filled, ready to process, or asks to process without new questions, require the refinement file to exist and confirm the primary document is writable.
7. If the user does not say the refinement was answered, confirm the primary document directory is writable.
8. If validation passes, read `references/body.md` and follow it.
