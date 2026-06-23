---
name: implement-with-logs
description: Implement an existing plan while appending contradictions, undefined points, assumptions, and blockers to an execution log. Use when the user asks to implement a plan with lightweight append-only logging.
---

# Implement With Logs

## Validation

Run these checks before implementation:

1. Confirm the user is asking to implement an existing plan, not create or review one.
2. Locate the plan in the prompt, an attached file, a named local path, or prior thread context.
3. If the plan source is missing, ask for it before making changes.
4. Identify the workspace root.
5. Validate that at least one supported append command family is available: PowerShell or POSIX shell.
6. Treat PowerShell as available when the active shell is PowerShell or `powershell`/`pwsh` can run.
7. Treat POSIX shell as available when `sh`, `date`, and `printf` can run.
8. If no supported append command family is available, stop and tell the user that append-only logging cannot be initialized.
9. Confirm requested actions do not require destructive operations unless the user explicitly asked for them.

If validation passes, read `references/body.md` and follow it.
