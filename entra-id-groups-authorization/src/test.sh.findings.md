# Findings for `test.sh`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. The bearer token is exposed on the process command line
- **Severity:** Medium
- **Lines:** `test.sh:170-201`
- **Why it matters:** The script fetches an access token and then passes it back to `az rest` via `--headers "Authorization=******"`. On multi-user systems, command-line arguments can be visible through process inspection tools, which leaks a live token to other local users or monitoring agents.
- **Recommendation:** Use a request path that does not put the token in argv, or pass the header through stdin/temp file with restricted permissions instead of the command line.
