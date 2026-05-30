# Findings for `refresh-1p-app-sp.sh`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. The default state file path is predictable and not hardened
- **Severity:** Medium
- **Lines:** `refresh-1p-app-sp.sh:39-40`, `refresh-1p-app-sp.sh:121-147`
- **Why it matters:** The script stores restore state in `/tmp/entra-sp-refresh-<appId>.json` and writes it with plain shell redirection. That predictable path is vulnerable to local tampering and symlink abuse, which can corrupt cleanup behavior or redirect writes if the script is run in a more privileged context.
- **Recommendation:** Use `mktemp` in a private directory, set restrictive permissions before writing, and refuse to follow pre-existing paths.
