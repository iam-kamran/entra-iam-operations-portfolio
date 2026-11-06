# Investigation 001 — Finance user cannot access IAMLAB-Finance-Portal

## 1. Ticket information

| Field | Value |
|---|---|
| Scenario | Finance user cannot access `IAMLAB-Finance-Portal` |
| Environment | Non-production Entra ID lab |
| Date investigation started | 2026-11-05 |
| Status | In progress |
| Business impact | Finance employee unable to access the Finance portal |

## 2. Reported issue

A Finance employee reports being unable to access `IAMLAB-Finance-Portal`.

The ticket did not provide a user identifier, sign-in timestamp, or error message. The affected identity must be discovered from sign-in evidence rather than selected by assumption.

## 3. Lab objects observed

The user shared a screenshot showing these application names:

- `IAMLAB-Finance-Portal`
- `IAMLAB-HR-Portal`

The investigation is scoped to `IAMLAB-Finance-Portal`. The screenshot alone does not establish the corresponding service principal details or prove that a sign-in attempt occurred.

Relevant group names observed during the candidate-user check:

- `IAMLAB-Finance`
- `IAMLAB-AllEmployees`

## 4. Initial candidate check — not confirmed as affected user

The investigator queried users whose UPN began with `IAM` and whose Department attribute began with `Fi`. A Finance user was selected as a candidate to test group membership.

The investigator later clarified that this user was not identified by the ticket or by a sign-in event. Therefore:

- The candidate is **not confirmed** as the affected user.
- The candidate's group memberships must not be treated as evidence explaining the reported incident.
- The candidate's actual UPN and object ID are intentionally omitted from this public record.

The candidate user's returned direct group membership output included:

| Group | Observed membership |
|---|---|
| `IPL-Foreign-Players` | Present |
| `IAMLAB-Finance` | Present |
| `IAMLAB-AllEmployees` | Present |

These observations apply only to the provisional candidate. They do not establish the affected user's membership or access to `IAMLAB-Finance-Portal`.

## 5. Investigation checklist

| Area | Investigation question | Result / evidence |
|---|---|---|
| Sign-in discovery | Which Finance user attempted to access `IAMLAB-Finance-Portal`? | Pending |
| Sign-in result | Did the attempt fail, succeed, or get interrupted? | Pending |
| Identity | Is the event's user object the correct identity and is the account enabled? | Pending |
| Attributes | Are Department and other relevant attributes correct? | Pending |
| Membership | Which relevant groups contain the identified user? | Pending |
| Group configuration | Are group type, assignment, and any dynamic rule understood? | Pending |
| Application | Is the correct enterprise application/service principal identified? | Pending |
| Assignment | Is the user or a relevant group assigned? | Pending |
| App role | Is the expected application role assigned? | Pending |
| Authentication | What do the sign-in details show? | Pending |
| Policy | Did Conditional Access or another authentication control affect the attempt? | Pending |
| Provisioning | Are provisioning errors relevant to the symptom? | Pending |

## 6. Next investigation action

Use Microsoft Entra sign-in logs to discover the affected user:

1. Open **Entra ID → Monitoring & health → Sign-in logs**.
2. Filter **Application** to `IAMLAB-Finance-Portal`.
3. Filter **Status** to **Failure**.
4. Start with **Interactive user sign-ins**.
5. Use the date range relevant to the reported attempt.
6. Inspect the event's user, application, status, failure reason/error code, Conditional Access result, timestamp, and correlation ID.

If no relevant event appears, validate the date range and sign-in type before widening the search. Consider whether the attempt may be present in another sign-in log type. Do not assume there was a sign-in event until one is found.

## 7. Commands executed

Record only commands actually run.

| Command | Purpose | Relevant output / observation |
|---|---|---|
| Candidate-user query using `Get-MgUser` with local PowerShell filters | Find lab users whose UPN begins with `IAM` and Department begins with `Fi` | Returned candidate Finance user(s); did not identify the affected user |
| `Get-MgUserMemberOfAsGroup` for provisional candidate | Inspect direct group membership | Returned `IPL-Foreign-Players`, `IAMLAB-Finance`, and `IAMLAB-AllEmployees`; candidate is not confirmed as the affected user |

## 8. Findings

### Confirmed facts

- The ticket did not provide a user identifier.
- The lab application names shown are `IAMLAB-Finance-Portal` and `IAMLAB-HR-Portal`.
- `IAMLAB-Finance-Portal` is the application in scope based on the Finance issue.
- A provisional Finance user was selected for an initial membership check, but that user is not linked to a failed sign-in event.

### Assumptions / hypotheses

No root-cause hypothesis is confirmed.

### Investigation limitations

- The affected user has not yet been identified.
- No relevant sign-in event has been inspected.
- The application screenshot does not by itself establish the sign-in event or service principal details.

## 9. Root cause

Not determined.

## 10. Remediation

Not determined. Any write operation requires explicit authorization and a documented change plan.

## 11. Validation

Not performed.

## 12. Lessons learned

To be completed after the investigation.

## 13. Public evidence review

Before publication, sanitize all outputs and confirm that no credentials, personal information, real tenant identifiers, or confidential configuration are included.
