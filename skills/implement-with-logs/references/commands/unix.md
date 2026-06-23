# Unix Log Commands

Use these commands only after validating that `sh`, `date`, and `printf` are available.

## Initialize

```sh
timestamp="$(date +%Y%m%d-%H%M%S)"
log_path="$(pwd)/implement-logs-$timestamp.log"
: > "$log_path"
printf '[%s] START plan implementation\n' "$(date -Iseconds)" >> "$log_path"
```

## Append

```sh
printf '[%s] ASSUMPTION %s :: %s :: %s\n' "$(date -Iseconds)" "<short title>" "<specific context>" "<chosen action>" >> "$log_path"
```

If tool calls run in separate shell processes, replace `$log_path` with the remembered absolute log path in every later append command.
