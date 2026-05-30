# Findings for `adme-entra-migration.sh`

## Summary
- 2 actionable findings.
- Highest severity: High.

## Findings

### 1. Runtime state loading executes arbitrary shell from `sim-state.env`
- **Severity:** High
- **Lines:** `adme-entra-migration.sh:580-586`
- **Why it matters:** `--state-dir` is documented as an operator input, but the file is loaded with `source`, so any shell payload in `sim-state.env` executes in the current process. A tampered state directory can therefore run arbitrary commands before the migration logic starts.
- **Recommendation:** Parse the env file as data instead of sourcing it, or tightly validate allowed keys and values before import.

### 2. App-role assignment checks only inspect the first Graph page
- **Severity:** Medium
- **Lines:** `adme-entra-migration.sh:1208-1238`
- **Why it matters:** `find_matching_app_role_assignment_id` and `count_matching_app_role_assignments` fetch `/servicePrincipals/{id}/appRoleAssignedTo` once and then filter client-side. In larger tenants, Graph paginates that collection, so an existing assignment on a later page is invisible. That can lead to duplicate-create attempts, false negatives during verification, or unnecessary failures.
- **Recommendation:** Reuse the inventory script’s paginated Graph helper or follow `@odata.nextLink` here before deciding whether an assignment exists.
