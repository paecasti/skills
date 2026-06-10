---
name: deslop-brainstorm-proposals
description: Brainstorm brief solution proposal ideas from an explicit flow folder. Use only when explicitly invoked as $deslop-brainstorm-proposals with a flow folder; default to 5 ideas unless the user specifies a count.
---

# Deslop Brainstorm Proposals

## Validation process

1. Require an explicit flow folder path before working:

```txt
<project>/<flows-container>/<flow-name>
```

2. Capture any user-specified proposal count from the invocation.
3. If no count is specified, use 5 proposal ideas.
4. Treat the flow folder as the unit of work, not the project root.
5. Require documentation from current context or this file:

```txt
<flow-folder>/docs/documentation.md
```

6. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the flow folder first and stop.
7. If validation passes, read `references/body.md` and follow it.
