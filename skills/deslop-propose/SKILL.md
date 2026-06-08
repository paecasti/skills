---
name: deslop-propose
description: Create one decision-ready proposal from an explicit flow folder after deslop-understand has produced documentation. Use only when explicitly invoked as $deslop-propose with a flow folder; honor user proposal direction when provided.
---

# Deslop Propose

## Validation process

1. Require an explicit flow folder path before working:

```txt
<project>/<flows-container>/<flow-name>
```

2. Capture any extra user directive from the invocation as proposal direction.
3. If the user gives no proposal direction, do not ask for one; choose the best solution direction during analysis.
4. Treat the flow folder as the unit of work, not the project root.
5. Require documentation from current context or this file:

```txt
<flow-folder>/docs/documentation.md
```

6. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the flow folder first and stop.
7. Read the questionnaire only when present and not already known from context:

```txt
<flow-folder>/docs/questions.md
```

8. If `questions.md` contains unresolved questions, warn the user that open questions remain and ask whether to continue anyway.
9. If the user does not explicitly choose to continue, stop without creating a proposal.
10. If validation passes, read `references/body.md` and follow it.
