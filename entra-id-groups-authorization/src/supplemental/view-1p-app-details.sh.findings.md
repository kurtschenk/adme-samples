# Findings for `view-1p-app-details.sh`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. Large tenants can get incomplete app-role, grant, and owner reports
- **Severity:** Medium
- **Lines:** `view-1p-app-details.sh:113-129`
- **Why it matters:** The script queries `appRoleAssignedTo`, `oauth2PermissionGrants`, and `owners` once each and prints only the first page. In tenants with more than one page of results, the helper reports a partial security picture while appearing complete.
- **Recommendation:** Follow `@odata.nextLink` for each collection or clearly label the output as first-page-only.
