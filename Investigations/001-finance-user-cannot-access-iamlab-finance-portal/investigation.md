# Investigation 001 — Finance user identity and application-role assignment review

## 1. Ticket information

| Field | Value |
|---|---|
| Scenario | Finance user identity and application-role assignment review |
| Environment | Non-production Entra ID lab |
| Practice identity | `IAMLAB-David Brown` |
| Department | Finance |
| Target application | `IAMLAB-Finance-Portal` |
| Command scope | Commands 1–5 from the 15-command reference |
| Status | Initial evidence reviewed; RCA not yet established |

This five-ticket practice track explicitly designates `IAMLAB-David Brown` as the practice identity. This is a lab exercise designation; it is not evidence of a real production incident or an independently discovered failed sign-in event.

## 2. Reported issue

The practice ticket states that the Finance user cannot access `IAMLAB-Finance-Portal`. Application Support asks IAM to verify the identity, account status, group memberships, and application-role assignments associated with the user.

No technical root cause is supplied.

## 3. Commands executed and evidence

### Command 1 — `Connect-MgGraph`

A Graph connection was established before the investigation. The connection command and output were not included in the submitted evidence.

### Command 2 — `Get-MgContext`

No context output was included in the submitted evidence. The connected account, tenant, authentication type, and granted scopes therefore remain unverified in this record.

### Command 3 — `Get-MgUser`

The investigator ran a user query with `-All`, then used `Where-Object` to filter UPNs containing the IAMLAB prefix.

The investigator identified the practice identity. The actual UPN and object ID are intentionally omitted from this public record. The submitted output returned 12 IAMLAB-prefixed user records; all 12 displayed `AccountEnabled = True`. David's returned row showed `AccountEnabled = True`. His account is therefore confirmed enabled in the lab.

**Efficiency note:** `-All` retrieves all pages before the local `Where-Object` filter is applied. For a large tenant, prefer a supported server-side Graph `-Filter` or retrieve a known user directly by UPN. Do not download the full directory to find one known identity.

### Command 4 — `Get-MgUserMemberOfAsGroup`

The returned direct group memberships were:

| Group | Observed result |
|---|---|
| `IPL-Foreign-Players` | Present |
| `IAMLAB-Finance` | Present |
| `IAMLAB-AllEmployees` | Present |

The group object IDs were reviewed during the exercise but are omitted from this public record.

**Finding:** The practice user is a direct member of `IAMLAB-Finance` and `IAMLAB-AllEmployees`.

### Command 5 — `Get-MgUserAppRoleAssignment`

The submitted output contained one row with the following sanitized evidence:

| Property | Observed value |
|---|---|
| ResourceDisplayName | `IAMLAB-Finance-Portal` |
| AppRoleId | `00000000-0000-0000-0000-000000000000` |
| PrincipalId | Matches the object ID returned for `IAMLAB-Finance` in Command 4 |

The returned `PrincipalId` matches the Finance group object ID from the membership result, rather than the practice user's object ID.

**Interpretation:** The output demonstrates an app-role assignment to `IAMLAB-Finance` for `IAMLAB-Finance-Portal`. This is a group-based assignment associated with the practice user's direct group membership; it is not evidence of an individually assigned app role to the user.

Microsoft Graph's user app-role-assignment endpoint returns assignments granted to the user and to groups of which the user is a direct member. See [Microsoft Learn — List appRoleAssignments granted to a user](https://learn.microsoft.com/en-us/graph/api/user-list-approleassignments?view=graph-rest-1.0).

The all-zero AppRoleId is the default app-role identifier used for a default access assignment when no specific application role is selected. The target service principal's role definitions have not yet been examined in this ticket.

## 4. Findings

### Confirmed from submitted output

1. The designated practice identity was returned by `Get-MgUser`; the submitted result showed `AccountEnabled = True`.
2. The practice user is a direct member of `IAMLAB-Finance` and `IAMLAB-AllEmployees`.
3. The user app-role-assignment query returned an assignment for `IAMLAB-Finance-Portal`.
4. The assignment's `PrincipalId` matches the `IAMLAB-Finance` group object ID from the membership result. The evidence therefore points to a group-based assignment.

### Not yet established

- The Graph authentication context and granted scopes, because `Get-MgContext` output was not shared.
- The connected tenant and granted Graph scopes, because `Get-MgContext` output was not shared.
- Whether the enterprise application is enabled.
- Whether assignment is required by the enterprise application.
- Whether the app-role model and SSO configuration support a successful application sign-in.
- Whether the application successfully authenticates or authorizes the user.

## 5. Preliminary assessment — not a root cause

The submitted evidence does **not** support missing direct membership in `IAMLAB-Finance`, and it does **not** support a missing Finance-group assignment to `IAMLAB-Finance-Portal`. A group-based app-role assignment is present in the returned data.

This does not prove that the user can successfully authenticate to or use the application. Ticket 001 is limited to commands 1–5; further investigation is allocated to subsequent tickets.

## 6. Root cause

Not determined. The current evidence identifies a group-based application assignment but does not establish why the reported access issue occurs.

## 7. Remediation

No change recommended at this stage. Continue with read-only investigation in the subsequent tickets. Any write operation requires explicit authorization.

## 8. Evidence and public-sharing review

Actual UPNs, user and group object IDs, tenant identifiers, and other sensitive values have been omitted from this public record. Only the lab's synthetic object names and the findings necessary to explain the investigation are retained.
