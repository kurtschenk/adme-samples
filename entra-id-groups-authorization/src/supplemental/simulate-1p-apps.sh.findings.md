# Findings for `simulate-1p-apps.sh`

## Summary
- 1 actionable finding.
- Highest severity: High.

## Findings

### 1. State-file loading still executes arbitrary shell
- **Severity:** High
- **Lines:** `simulate-1p-apps.sh:190-198`
- **Why it matters:** `source_shell_file` syntax-checks the file with `bash -n`, then immediately `source`s it. Syntax validation does not prevent command execution, so a tampered state file can still run arbitrary shell in the current process.
- **Recommendation:** Parse the state file as data, or at minimum restrict it to a validated allowlist of variable assignments before importing it.
