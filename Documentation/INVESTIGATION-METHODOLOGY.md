# IAM Investigation Methodology

## Purpose

Use a consistent, evidence-led process to investigate identity and access issues in the Microsoft Entra ID lab.

The investigator should select commands based on the question being answered. This document intentionally does not prescribe a fixed list of commands.

## Investigation stages

### 1. Understand the ticket

Record:
- Reported symptom
- Requestor or reporting team (use fictional labels)
- Affected user or workload identity (synthetic identifier only)
- Target application or resource
- Business impact
- Time of occurrence and relevant time zone, when known
- What is known, unknown, and still needs confirmation

Do not assume the reported symptom identifies the technical cause.

### 2. Establish the identity facts

Determine whether the target identity is the correct object and whether its state and relevant attributes are consistent with the reported access requirement.

Potential questions:
- Is the identity present?
- Is the account enabled?
- Are relevant attributes populated correctly?
- Is the object a member user, guest, or workload identity?

Record the exact properties inspected and what each result establishes.

### 3. Examine group access

Determine:
- Which relevant groups contain the identity?
- Is the membership direct or nested/transitive?
- Is a group assigned to the target application?
- Is membership assigned manually or calculated dynamically?
- If dynamic, what is the membership rule and has processing completed?

Do not treat a matching dynamic membership rule as proof that membership processing has completed. Do not treat a direct-membership query as proof of transitive membership.

### 4. Examine the application and assignments

Identify the correct enterprise application (service principal) and distinguish it from the app registration (application object).

Determine:
- Whether the intended enterprise application exists
- Whether the user or a group has an assignment
- Whether the assignment is direct or group-derived
- Which app role, if any, is assigned
- Whether the target application requires assignment

An assignment alone does not prove that authentication or authorization succeeded.

### 5. Review authentication and operational evidence

When relevant and available, inspect:
- Sign-in activity and failure details
- Conditional Access evaluation
- Authentication requirements
- Provisioning activity and errors
- Directory audit events around the reported time

Use a time window appropriate to the ticket. Record missing permissions or unavailable logs as investigation limitations; do not infer their contents.

### 6. Build an evidence-based conclusion

For each finding, record:
- Observation
- Evidence source (command/API area and relevant output)
- What the evidence proves
- What it does not prove
- Whether the finding is confirmed, probable, or unverified

Do not promote an assumption to a root cause.

### 7. Recommend or perform remediation

Start read-only. Recommend a change only after the evidence supports it.

Before any write operation, establish:
- The exact object and property to change
- Why the change is necessary
- Expected impact and potential side effects
- Required authorization and least-privilege permission
- Rollback or recovery approach, where applicable

No write operation should be performed in a lab exercise without explicit authorization in the exercise.

### 8. Validate

Define the expected result before making a change. After an authorized change, collect new evidence that verifies the target state. Where applicable, confirm the user can complete the intended access flow; do not equate a successful directory write with successful application access.

## Investigation checklist

- [ ] Ticket and business impact understood
- [ ] Correct identity confirmed
- [ ] Account state and relevant attributes checked
- [ ] Relevant group membership checked
- [ ] Group type and membership processing understood
- [ ] Correct enterprise application identified
- [ ] Direct and group-based assignments checked
- [ ] App role / authorization requirements checked
- [ ] Sign-in and policy evidence reviewed where relevant
- [ ] Provisioning and audit evidence reviewed where relevant
- [ ] Findings separated from assumptions
- [ ] Root cause supported by evidence
- [ ] Remediation authorized and scoped
- [ ] Outcome validated
- [ ] Public evidence sanitized

## Quality rule

A good investigation is not measured by the number of commands executed. It is measured by whether the investigator asked the right questions, collected relevant evidence, understood the limits of that evidence, and reached a defensible conclusion.
