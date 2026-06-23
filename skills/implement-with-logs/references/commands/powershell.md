# PowerShell Log Commands

Use these commands only after validating that PowerShell is available.

## Initialize

```powershell
$timestamp = Get-Date -Format "yyyyMMdd-HHmmss"
$logPath = Join-Path (Get-Location) "implement-logs-$timestamp.log"
New-Item -ItemType File -LiteralPath $logPath -Force | Out-Null
Add-Content -LiteralPath $logPath -Value "[$(Get-Date -Format o)] START plan implementation"
```

## Append

```powershell
Add-Content -LiteralPath $logPath -Value "[$(Get-Date -Format o)] ASSUMPTION <short title> :: <specific context> :: <chosen action>"
```

If tool calls run in separate shell processes, replace `$logPath` with the remembered absolute log path in every later append command.
