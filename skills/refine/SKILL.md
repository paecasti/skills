---
name: refine
description: Generate or process a staged refinement.md for provided documentation by asking about business requirements and contradictions, strategic architecture, then detailed tactical design. Use only when explicitly invoked as $refine with a primary document path. Work on one level per run and record answered refinements in the primary document.
---

# Refine

## Validation

1. Require an explicit primary document path.
2. Accept optional supporting document paths after the primary path.
3. Confirm every provided document exists and is readable.
4. Resolve `refinement.md` in the primary document directory.
5. When processing answers, require `refinement.md` to exist and the primary document to be writable.
6. When generating or updating questions, require the primary document directory to be writable.
7. If any check fails, stop and report every failure; otherwise read `references/body.md` and follow it.
