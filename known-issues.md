# Known Issues — molecule-skill-cross-vendor-review

---

## Active Issues

*(None currently open. This section is updated when issues are filed.)*

---

## Recently Resolved

*(No recently resolved issues.)*

---

## How to Update This File

When a new issue is identified:
1. Add it under **Active Issues** using the template below
2. Include: symptom, cause (if known), workaround
3. When fixed, move to **Recently Resolved** and note the fix version

### Issue Template

```markdown
## [TICKET-NUMBER] <Short Title>

**Severity:** P0 / P1 / P2 / P3
**Status:** Workaround / Fix in progress / Fix available
**Affected versions:** All / vX.Y.Z+

**Symptoms:**
**Cause:**
**Workaround:**
**Fix (if available):**
```

---

## Severity Definitions

| Level | Description |
|---|---|
| P0 | Cross-vendor review silently skipped; no output |
| P1 | API key exposed in logs or error messages |
| P2 | Disagreements not surfaced to agent |
| P3 | Cosmetic or documentation issue |

---

## Reporting

Use the Molecule-AI/internal issue tracker. Tag with `plugin-molecule-skill-cross-vendor-review`.
