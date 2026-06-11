---
name: deslop-propose
description: Create one decision-ready proposal from an explicit flow folder after deslop-understand has produced documentation. Use only when explicitly invoked as $deslop-propose with a flow folder; honor user proposal direction when provided.
---

# Deslop Propose

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use this as a user-facing recommendation for mid-tier models, not as an instruction for the agent to switch models. Prefer the first available model in order. Add separate low-tier or high-tier model hierarchies when those recommendations exist.

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
7. If validation passes, read `references/body.md` and follow it.
