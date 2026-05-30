# Findings for `Delete-1PServicePrincipal.ps1`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. The destructive delete path has no confirmation or `ShouldProcess` support
- **Severity:** Medium
- **Lines:** `Delete-1PServicePrincipal.ps1:1-46`
- **Why it matters:** Once the script resolves the service principal, it deletes it immediately. In PowerShell, administrators expect destructive tools to support `-WhatIf`/`-Confirm`; without that safety net, a typo or accidental invocation can remove the wrong enterprise app with no pause.
- **Recommendation:** Add `SupportsShouldProcess`, honor `-WhatIf`/`-Confirm`, and require an explicit confirmation before the delete call.
