# Findings for `Get-1PAppDetails.ps1`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. Multi-page Graph collections are reported as if they were complete
- **Severity:** Medium
- **Lines:** `Get-1PAppDetails.ps1:118-160`
- **Why it matters:** The script fetches `appRoleAssignedTo`, `oauth2PermissionGrants`, and `owners` only once each. Graph paginates those collections, so tenants with enough entries get partial output with no warning that later pages were ignored.
- **Recommendation:** Follow `@odata.nextLink` for each collection or make the first-page-only limitation explicit.
