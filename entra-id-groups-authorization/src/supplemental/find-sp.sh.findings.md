# Findings for `find-sp.sh`

## Summary
- 1 actionable finding.
- Highest severity: Low.

## Findings

### 1. OData filters embed the raw identifier without escaping
- **Severity:** Low
- **Lines:** `find-sp.sh:49-58`, `find-sp.sh:73-81`
- **Why it matters:** When the input is an identifier URI rather than a GUID, the value is interpolated directly into single-quoted OData filters. An apostrophe in the URI breaks the query and can change filter semantics, which makes the helper fragile for non-default identifiers.
- **Recommendation:** Escape single quotes for OData literals or URL-encode the filter value before issuing the request.
