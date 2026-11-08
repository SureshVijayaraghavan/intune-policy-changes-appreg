# intune-policy-changes-appreg

**Public intent repo** for the Intune CI/CD App Registration certificate POC.

Describes *what* to change. Does **not** hold Entra secrets or certificates.

## Pairing

| Repo | Visibility | Role |
| --- | --- | --- |
| `intune-policy-changes-appreg` (this repo) | Public | Change requests / trigger |
| [`intune-cicd-appreg-poc`](https://github.com/SureshVijayaraghavan/intune-cicd-appreg-poc) | Private | App Registration cert → Graph |

```text
Public changes/*.json ──repository_dispatch──► Private executor (cert auth) ──► Graph / Intune
```

## Change request shape

```json
{
  "action": "updateCompliancePolicy",
  "platform": "Android",
  "policyId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "patch": {
    "@odata.type": "#microsoft.graph.androidWorkProfileCompliancePolicy",
    "osMinimumVersion": "15.0",
    "minAndroidSecurityPatchLevel": "2026-09-05"
  }
}
```

## One-time setup

1. Fine-grained PAT (or reuse gh token for lab) with **Actions: Read and write** on `intune-cicd-appreg-poc`
2. Secret on this public repo: `EXECUTOR_DISPATCH_TOKEN`
3. Optional variable `EXECUTOR_REPO` (default `SureshVijayaraghavan/intune-cicd-appreg-poc`)
