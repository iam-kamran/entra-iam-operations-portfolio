# Investigation 001 — Finance user cannot access IAMLAB-Finance-Portal

**Status:** In progress

## Ticket summary

A Finance employee reports that they cannot access `IAMLAB-Finance-Portal`.

**Environment:** Non-production Microsoft Entra ID learning lab  
**Scenario type:** Simulated IAM support ticket  
**Investigation status:** In progress

## Scope

Identify the actual user from relevant sign-in evidence, then investigate the identity, group membership, application assignment, and authentication evidence as appropriate.

The ticket did not initially provide a user identifier. Do not assume that a user selected from the Finance department is the affected user.

## Related lab objects observed

- `IAMLAB-Finance-Portal`
- `IAMLAB-HR-Portal`
- `IAMLAB-Finance`
- `IAMLAB-AllEmployees`

Only `IAMLAB-Finance-Portal` is in scope for this ticket. The HR portal is not part of this investigation.

## Investigation record

The work-in-progress record is in [investigation.md](./investigation.md).

## Evidence

Add only relevant, sanitized evidence under the `evidence/` directory. Do not publish real UPNs, object IDs, tenant IDs, IP addresses, or other sensitive identifiers.

## Important

This is a simulated lab scenario, not a production incident. Do not add real employee information or confidential organizational data.
