# Findings for `AdmeEntraHelper.psm1`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. App-role assignment helpers do not follow paginated Graph results
- **Severity:** Medium
- **Lines:** `AdmeEntraHelper.psm1:1043-1051`, `AdmeEntraHelper.psm1:1163-1172`
- **Why it matters:** `Find-AppRoleAssignment` and `Get-AppRoleAssignmentCount` read `/servicePrincipals/{id}/appRoleAssignedTo` once and inspect only `$response.value`. In tenants with enough assignments to trigger pagination, existing matches on later pages are missed, so callers can incorrectly create duplicates or fail readiness checks.
- **Recommendation:** Add a paginated Graph reader and consume the full collection before deciding whether a matching assignment exists.
