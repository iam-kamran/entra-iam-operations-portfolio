# Five-Ticket Microsoft Graph PowerShell Practice Track

## Purpose

Build practical Entra IAM investigation skills by applying the 15 Microsoft Graph PowerShell commands in the companion command reference to the same non-production lab objects.

The first four tickets introduce focused command groups. Ticket 005 is the capstone and requires all 15 commands together.

**Investigation method:** Microsoft Graph PowerShell only. Do not use the Entra admin center portal as the investigation method for these tickets.

**Safety:** These are simulated lab exercises. Use read-only investigation. Do not change directory or application configuration without explicit authorization. Do not publish real UPNs, object IDs, tenant IDs, IP addresses, access tokens, or other sensitive information.

## Lab object set

Use the existing lab objects and their exact naming conventions:

| Object type | Lab object |
|---|---|
| User | `IAMLAB-David Brown` |
| Finance group | `IAMLAB-Finance` |
| General employee group | `IAMLAB-AllEmployees` |
| Finance enterprise application | `IAMLAB-Finance-Portal` |
| HR enterprise application | `IAMLAB-HR-Portal` |

The HR application is included as a comparison object only when relevant. Do not create new users, groups, or applications for these exercises.

## Command allocation

| Ticket | Focus | Commands | Count |
|---|---|---|---:|
| 001 | User identity, direct membership, and direct app assignment | 1–5 | 5 |
| 002 | Group configuration, members, and group app-role assignment | 6–8 | 3 |
| 003 | Enterprise application, assignments, and app registration | 9–11 | 3 |
| 004 | Sign-in, audit, licensing, and ownership review | 12–15 | 4 |
| 005 | End-to-end Finance Portal access investigation | 1–15 | 15 |

Tickets 001–004 collectively cover all 15 commands once. Ticket 005 repeats them in an integrated investigation.

---

# Ticket 001 — Finance user identity and direct access review

**Priority:** Medium  
**Category:** Identity and access investigation  
**Affected identity:** `IAMLAB-David Brown`  
**Relevant groups:** `IAMLAB-Finance`, `IAMLAB-AllEmployees`  
**Target application:** `IAMLAB-Finance-Portal`

## Reported issue

Application Support reports that the Finance user is unable to access the Finance Portal. The support team asks IAM to verify the user's identity record and determine what direct group membership and direct application-role assignments are present.

No root cause is known.

## Your assignment

Investigate the user's Graph authentication context, confirm the identity and account attributes, inspect the user's direct group memberships, and determine whether the user has any direct application-role assignments.

## Assigned commands

1. `Connect-MgGraph`
2. `Get-MgContext`
3. `Get-MgUser`
4. `Get-MgUserMemberOfAsGroup`
5. `Get-MgUserAppRoleAssignment`

## Expected deliverable

Document the verified identity facts, direct memberships, direct application-role assignments, and any gaps or limitations. Do not assume that direct assignment results include access inherited through groups.

---

# Ticket 002 — Finance group access configuration review

**Priority:** Medium  
**Category:** Group membership and application access  
**Relevant user:** `IAMLAB-David Brown`  
**Groups:** `IAMLAB-Finance`, `IAMLAB-AllEmployees`  
**Target application:** `IAMLAB-Finance-Portal`

## Reported issue

The application support team states that Finance Portal access is expected to be granted through the `IAMLAB-Finance` group. They are unable to confirm whether the group contains the intended members and whether the group has the expected application-role assignment.

## Your assignment

Inspect both groups' configuration, verify their direct membership, and determine whether the Finance group has an application-role assignment. Identify what the evidence establishes and what it does not establish about David's effective access.

## Assigned commands

6. `Get-MgGroup`
7. `Get-MgGroupMember`
8. `Get-MgGroupAppRoleAssignment`

## Expected deliverable

Document each group's type and relevant configuration, the relevant membership evidence, and any application-role assignment made by the group. Do not treat group membership or an assignment alone as proof of successful sign-in.

---

# Ticket 003 — Finance Portal enterprise application review

**Priority:** Medium  
**Category:** Enterprise application and app registration  
**Target enterprise application:** `IAMLAB-Finance-Portal`  
**Comparison application:** `IAMLAB-HR-Portal`

## Reported issue

The IAM team needs to verify that the Finance Portal enterprise application is the correct tenant-local application object, identify its assigned principals, and correlate it with the relevant app registration. The team also wants to understand whether the application requires assignment and which app roles are exposed.

## Your assignment

Investigate the Finance Portal service principal, inspect its assigned principals and app roles, and identify the corresponding application registration using the application/client ID. Use the HR Portal only as a comparison if needed to resolve ambiguity.

## Assigned commands

9. `Get-MgServicePrincipal`
10. `Get-MgServicePrincipalAppRoleAssignedTo`
11. `Get-MgApplication`

## Expected deliverable

Document the service principal identity, application/client ID, enabled and assignment-required state, assigned principals, available app roles, and the matching app registration. Keep the service principal object ID distinct from the application object ID and AppId.

---

# Ticket 004 — Finance user activity, change, licensing, and ownership review

**Priority:** Medium  
**Category:** Access review and identity lifecycle  
**User under review:** `IAMLAB-David Brown`  
**Relevant group:** `IAMLAB-Finance`  
**Relevant application:** `IAMLAB-Finance-Portal`

## Reported issue

The IAM team has been asked to review David's recent access activity and directory state before a proposed Finance role change. The reviewer needs to understand whether the user has recently signed in, whether relevant directory changes were recorded, what licenses and service plans are assigned, and whether the user owns directory objects that may require attention during a role transition.

No change has been authorized.

## Your assignment

Review available sign-in records and relevant directory audit events. Inspect license and service-plan assignments, then identify directory objects owned by the user. Establish the limits of each evidence source and identify any ownership or lifecycle follow-up that should be reviewed before a change is approved.

## Assigned commands

12. `Get-MgAuditLogSignIn`
13. `Get-MgAuditLogDirectoryAudit`
14. `Get-MgUserLicenseDetail`
15. `Get-MgUserOwnedObject`

## Expected deliverable

Document sign-in evidence for the relevant application and time window, relevant audit events, assigned licenses and service-plan states, and owned directory objects. Do not interpret a license or ownership record as proof of application access.

---

# Ticket 005 — Capstone: Finance Portal access investigation

**Priority:** High  
**Category:** End-to-end IAM incident investigation  
**Affected identity:** `IAMLAB-David Brown`  
**Department:** Finance  
**Target application:** `IAMLAB-Finance-Portal`  
**Relevant groups:** `IAMLAB-Finance`, `IAMLAB-AllEmployees`

## Reported issue

David Brown reports that he cannot access `IAMLAB-Finance-Portal`. Application Support asks IAM to determine whether the issue is related to the identity, group configuration, application assignment, application registration, sign-in history, directory changes, licensing, or directory-object ownership.

No error details or root cause are provided.

## Your assignment

Conduct a complete read-only investigation. Use all 15 commands to trace the relationship between the user, groups, enterprise application, application registration, sign-in evidence, audit history, licensing, and owned objects.

Do not assume that every area will contain a fault. Follow the evidence and avoid collecting unnecessary data.

## Required commands — all 15

1. `Connect-MgGraph`
2. `Get-MgContext`
3. `Get-MgUser`
4. `Get-MgUserMemberOfAsGroup`
5. `Get-MgUserAppRoleAssignment`
6. `Get-MgGroup`
7. `Get-MgGroupMember`
8. `Get-MgGroupAppRoleAssignment`
9. `Get-MgServicePrincipal`
10. `Get-MgServicePrincipalAppRoleAssignedTo`
11. `Get-MgApplication`
12. `Get-MgAuditLogSignIn`
13. `Get-MgAuditLogDirectoryAudit`
14. `Get-MgUserLicenseDetail`
15. `Get-MgUserOwnedObject`

## Required RCA deliverable

Your final report must include:

1. Incident summary and business impact.
2. Identity verification and account state.
3. Direct group memberships and relevant group configuration.
4. Direct user and group-based application assignments.
5. Enterprise application and app registration correlation.
6. Relevant app-role information.
7. Sign-in and Conditional Access evidence, where available.
8. Relevant directory audit evidence.
9. License and service-plan findings, where relevant.
10. Owned-object findings and any lifecycle considerations.
11. Confirmed root cause, supported by evidence — or a clear statement that the root cause remains unconfirmed.
12. Recommended remediation, required authorization, and validation approach.

## Rules for all five tickets

- Use only the 15 Graph PowerShell commands listed in the companion reference for directory investigation.
- Standard PowerShell formatting and property selection may be used to inspect the returned data.
- Do not introduce unrelated Graph cmdlets or switch to portal-based investigation.
- Begin read-only. Do not perform write operations without explicit authorization.
- Use server-side filters when supported and appropriate; do not retrieve an entire tenant unnecessarily.
- Distinguish direct membership from transitive membership.
- Distinguish direct user assignment from group-based assignment.
- Distinguish the application object from the service principal.
- Treat sign-in and audit logs as time-bounded and permission-dependent.
- Record what the evidence proves and what it does not prove.
- Do not invent output or claim that an action succeeded without verification.
- Sanitize all evidence before committing it to the public portfolio.

## Scope note: SSO configuration

This 15-command set is an investigation reference. It does not include the write commands required to configure or modify SSO. SSO implementation will be a separate, explicitly scoped lab exercise after the read-only application and access investigations are complete.
