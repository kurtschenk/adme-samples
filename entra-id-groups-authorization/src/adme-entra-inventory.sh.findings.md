# Findings for `adme-entra-inventory.sh`

## Summary
- 1 actionable finding.
- Highest severity: High.

## Findings

### 1. Runtime overrides execute arbitrary shell from `sim-state.env`
- **Severity:** High
- **Lines:** `adme-entra-inventory.sh:489-497`
- **Why it matters:** When `STATE_DIR` is set, the script loads `sim-state.env` with `source`. That turns an operator-supplied state file into executable code. A poisoned state directory can therefore execute arbitrary shell before inventory discovery runs.
- **Recommendation:** Replace `source` with a parser that reads only expected `KEY=VALUE` pairs, or validate the file contents before import.
