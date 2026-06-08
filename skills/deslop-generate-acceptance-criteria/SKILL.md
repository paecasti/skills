---
name: deslop-generate-acceptance-criteria
description: Generate acceptance criteria from a deslop-understand documentation.md file. Use only when explicitly invoked as $deslop-generate-acceptance-criteria with a flow folder; do not implement or propose solutions.
---

# Deslop Generate Acceptance Criteria

## Validation process

1. Require an explicit flow folder path before working:

```txt
<project>/<flows-container>/<flow-name>
```

2. Treat the flow folder as the unit of work, not the project root.
3. Require documentation from current context or this file:

```txt
<flow-folder>/docs/documentation.md
```

4. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the flow folder first and stop.
5. Read the questionnaire only when present and not already known from context:

```txt
<flow-folder>/docs/questions.md
```

6. If `questions.md` is missing or contains no unresolved questions, continue.
7. If `questions.md` contains unresolved questions, warn the user that open questions remain and ask whether to continue anyway.
8. If the user does not explicitly choose to continue, stop without creating acceptance criteria.
9. If validation passes, read `references/body.md` and follow it.
