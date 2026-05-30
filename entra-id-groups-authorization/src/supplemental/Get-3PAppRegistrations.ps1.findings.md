# Findings for `Get-3PAppRegistrations.ps1`

## Summary
- 1 actionable finding.
- Highest severity: Medium.

## Findings

### 1. Consent-report sections stop at the first Graph page
- **Severity:** Medium
- **Lines:** `Get-3PAppRegistrations.ps1:136-191`
- **Why it matters:** The app-registration scan paginates correctly, but the later `appRoleAssignedTo` and `oauth2PermissionGrants` queries do not. In larger tenants, the consent inventory becomes incomplete and the follow-on service-principal resolution loop only analyzes the truncated result set.
- **Recommendation:** Add pagination for those resource-centric collections before reporting or deriving follow-on lookups.
