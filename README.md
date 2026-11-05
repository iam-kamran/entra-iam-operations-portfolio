# Entra IAM Operations Portfolio

A hands-on portfolio of Microsoft Entra ID identity and access management investigations performed in a non-production lab.

This repository documents practical IAM troubleshooting: how an issue is assessed, what evidence is collected, how Microsoft Graph PowerShell is used, how findings are evaluated, and how a resolution is validated.

> **Environment:** Non-production learning lab. Scenarios and identities are simulated. This repository is not a record of production incidents or production access.

## What this portfolio demonstrates

- Structured identity and access troubleshooting
- Microsoft Entra ID investigation using Microsoft Graph PowerShell
- Analysis of users, attributes, group membership, enterprise applications, app-role assignments, sign-in activity, and audit events
- Evidence-based root-cause analysis
- Least-privilege and read-only-first investigation habits
- Remediation planning and post-change validation

## Investigation library

| ID | Scenario | Status |
|---|---|---|
| 001 | Finance employee cannot access the Payroll application | Planned |

Each investigation will be added as its own folder under [Investigations](./Investigations/).

## Investigation approach

1. Understand the reported issue and business impact.
2. Confirm the identity and relevant account attributes.
3. Examine group membership and group configuration.
4. Inspect the enterprise application and its assignments.
5. Review relevant authentication, sign-in, provisioning, and policy evidence.
6. Separate verified facts from assumptions.
7. State the root cause only when supported by evidence.
8. Recommend an appropriately authorized remediation.
9. Validate the outcome and document remaining limitations.

The checklist is a guide, not a command sequence. The investigation should follow the evidence available in each scenario.

## Repository structure

```text
.
├── README.md
├── Investigations/
│   └── 001-finance-user-cannot-access-payroll/
│       ├── README.md
│       ├── investigation.md
│       └── evidence/
├── Documentation/
│   ├── INVESTIGATION-METHODOLOGY.md
│   └── EVIDENCE-AND-SAFETY-STANDARDS.md
└── Scripts/
    └── README.md
```

## Evidence and public-sharing standards

- Use synthetic identities and sanitized outputs.
- Never commit passwords, access tokens, client secrets, certificates, private keys, or other credentials.
- Do not publish real tenant or organization data, personal information, or confidential configuration.
- Capture only the output needed to support a finding.
- Redact identifiers and sensitive values before publishing screenshots or logs.
- Label simulated results clearly.
- Do not describe a command as successful unless its output confirms success.
- Do not claim that an assignment proves successful authentication or that a matching dynamic-group rule proves membership has already been processed.

See [Evidence and Safety Standards](./Documentation/EVIDENCE-AND-SAFETY-STANDARDS.md).

## Related learning repository

Reusable Microsoft Graph PowerShell command notes and scripts are maintained separately:

[graph-powershell-commands](https://github.com/iam-kamran/graph-powershell-commands)

## Disclaimer

This is an educational portfolio of lab-based exercises. It is intended to demonstrate investigation methods and technical learning, not to disclose any employer's systems, data, or internal procedures.
