---
name: deslop-plan-prs
description: Create a PR-by-PR execution plan from a completed Deslop proposal, documentation, and acceptance criteria. Use only when explicitly invoked as $deslop-plan-prs with a flow folder; write files under flow-folder/plan.
---

# Deslop Plan PRs

## Validation process

1. Require an explicit flow folder path before working:

```txt
<project>/<flows-container>/<flow-name>
```

2. Treat the flow folder as the unit of work, not the project root.
3. Require a completed proposal from current context or an explicit proposal file under:

```txt
<flow-folder>/proposals/
```

4. If no completed proposal is in context and no explicit proposal file is provided, ask the user which proposal to plan and stop.
5. Require documentation from current context or this file:

```txt
<flow-folder>/docs/documentation.md
```

6. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` first and stop.
7. Require acceptance criteria from current context or this file:

```txt
<flow-folder>/docs/acceptance-criteria.md
```

8. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to run `$deslop-generate-acceptance-criteria` first and stop.
9. Read the questionnaire only when present and not already known from context:

```txt
<flow-folder>/docs/questions.md
```

10. If `questions.md` contains unresolved questions, warn the user that open questions remain and ask whether to continue anyway.
11. If the user does not explicitly choose to continue, stop without creating the plan.
12. If validation passes, read `references/body.md` and follow it.
