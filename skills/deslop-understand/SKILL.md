---
name: deslop-understand
description: Build documented understanding from an explicit flow folder for later Deslop proposal work. Use only when explicitly invoked as $deslop-understand with a flow folder; do not propose, plan, or implement.
---

# Deslop Understand

## Validation process

1. Require an explicit flow folder path before working:

```txt
<project>/<flows-container>/<flow-name>
```

2. Treat the flow folder as the unit of work, not the project root.
3. Require background material from current context or this folder:

```txt
<flow-folder>/background/
```

4. If background material is not in context and `background/` is missing, tell the user and stop.
5. If validation passes, read `references/body.md` and follow it.
