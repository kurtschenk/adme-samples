# Findings for `Invoke-AdmeMigration.ps1`

## Summary
- 1 actionable finding.
- Highest severity: High.

## Findings

### 1. Helper-module discovery trusts the current working directory
- **Severity:** High
- **Lines:** `Invoke-AdmeMigration.ps1:86-113`
- **Why it matters:** `Ensure-HelperModuleLoaded` tries `./AdmeEntraHelper.psm1` and invocation-relative paths before the script-root copy. If the script is launched from an untrusted directory, a malicious sibling module can be imported and executed before the intended helper module.
- **Recommendation:** Import only from a canonical path rooted at `$PSScriptRoot`, or require an explicit trusted module path.
