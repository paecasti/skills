---
name: html-explainer
description: Convert a primary documentation file and optional supporting files into a standalone HTML explainer page. Use when explicitly invoked with a primary document path.
---

# HTML Explainer

## Validation

Run these checks before generating the HTML page:

1. Require an explicit primary document path.
2. Accept optional supporting document paths after the primary path.
3. Confirm the primary document exists.
4. Confirm each supporting document exists before using it.
5. Resolve the output path as `html-explainer/index.html` in the same directory as the primary document.
6. Confirm the primary document directory is writable.
7. If the output file already exists and the user did not explicitly authorize overwrite, stop and ask before replacing it.
8. Treat the primary and supporting documents as read-only.
9. If validation passes, read `references/body.md` and follow it.
