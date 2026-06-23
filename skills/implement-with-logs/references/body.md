# Implement With Logs Body

## What This Produces

Completed implementation work from a provided plan, plus an append-only log named `implement-logs-<execution-start-timestamp>.log` in the workspace root.

## Process

1. Create the execution log in the workspace root before editing files.
2. Use one filename-safe timestamp captured once at execution start.
3. Keep the absolute log path in memory for the turn.
4. Select one command reference from the validated append command family.
5. Select PowerShell when both PowerShell and POSIX shell are available.
6. Select POSIX shell only when PowerShell is unavailable.
7. Read `references/commands/powershell.md` only when PowerShell is available and selected.
8. Read `references/commands/unix.md` only when POSIX shell is available and selected.
9. Do not read command reference files for unavailable or unselected shells.
10. Append log entries with the selected shell command. Do not read, tail, summarize, parse, or inspect the log file at any time.
11. Add a log entry immediately whenever you encounter a contradiction, undefined requirement, assumption, risky interpretation, blocked step, missing dependency, skipped plan item, test limitation, or user-visible behavioral choice.
12. Include enough context in each log entry to reconstruct the decision without needing the assistant transcript.
13. Continue implementation after logging when a conservative assumption is safe.
14. Ask the user only when the issue blocks implementation or a safe assumption would likely produce the wrong result.
15. Verify the implementation with the narrowest useful checks.
16. In the final response, report the log file path and whether verification passed. Do not include log contents unless requested.

## Entry Types

- `CONTRADICTION`: Two plan instructions cannot both be true.
- `UNDEFINED`: The plan omits a required detail.
- `ASSUMPTION`: You choose a default to keep work moving.
- `RISK`: The chosen action may affect behavior outside the plan.
- `BLOCKED`: Work cannot continue without user input or external state.
- `SKIPPED`: A plan item is intentionally not implemented.
- `VERIFY`: A verification command cannot run or gives incomplete coverage.
- `DECISION`: A user-visible choice is made from multiple valid options.

## Gotcha List

- Do not read the log file at any time.
- Do not read command reference files before validating that their shell family is available.
- Do not spend final-response tokens reproducing log entries.
- Do not overwrite an existing execution log; the timestamp must make each run distinct.
- Do not log every normal implementation step; only log uncertainty, conflict, assumption, risk, blockage, skipped scope, and verification limits.
