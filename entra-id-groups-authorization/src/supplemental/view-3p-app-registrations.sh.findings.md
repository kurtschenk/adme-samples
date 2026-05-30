# Findings for `view-3p-app-registrations.sh`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. Resource-centric sections silently truncate on Graph pagination
- **Severity:** Medium
- **Lines:** `view-3p-app-registrations.sh:90-143`
- **Why it matters:** The initial application scan follows `@odata.nextLink`, but the later `appRoleAssignedTo` and `oauth2PermissionGrants` fetches do not. In larger tenants, those sections can omit granted clients, and the downstream service-principal/app-resolution loop only sees the truncated set.
- **Recommendation:** Apply the same pagination handling used for the application scan to both consent collections before building follow-on reports.
