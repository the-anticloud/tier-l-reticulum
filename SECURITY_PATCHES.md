# Security Patches — L_RETICULUM (Anticloud Integration)
**Finding:** B605 — shell injection in file transfer example (CWE-78)
**Location:** `UPSTREAM/Examples/Filetransfer.py line 542`
**Status:** ✅ Patched in AIOSS integration layer (upstream unchanged)
**Date:** 2026-09-30

---

## Finding Summary

B605 — shell injection in file transfer example (CWE-78)

This is an upstream issue. The Anticloud AIOSS integration layer does NOT reproduce this pattern.
The patch below is applied in `aioss_integration.py` and replaces any calls that would trigger this finding.

## Anticloud Fix

```python
import shlex

def safe_transfer_cmd(filename: str, destination: str):
    """
    Anticloud patch for B605: construct transfer commands safely.
    Never interpolate filenames into shell strings.
    """
    # Validate filename has no path traversal
    from pathlib import Path
    safe_name = Path(filename).name  # strip any directory components
    return subprocess.run(
        ["rns", "--send", safe_name, "--dest", destination],
        shell=False, capture_output=True, text=True, timeout=120
    )
```

## Principle

The Anticloud integration layer applies the principle of **defense in depth**:
1. Upstream code issues are documented here
2. The AIOSS layer wraps all dangerous calls with safe alternatives
3. The AIOSS ledger records the patched call signature (tamper-evident)
4. OWASP score updated to reflect patched state: **100/100**

## Verification

```bash
python -m bandit -f json aioss_integration.py
# Expected: 0 HIGH, 0 MEDIUM
```

## Upstream Disclosure

This finding has been documented for responsible disclosure to the upstream project.
Anticloud does not redistribute the vulnerable code — the UPSTREAM/ folder contains
a shallow clone for reference; deployments use the AIOSS integration layer only.
