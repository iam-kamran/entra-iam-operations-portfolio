# Evidence and Public-Sharing Standards

This repository is public. Treat every file, screenshot, log, command output, and commit as information that anyone can read.

## Never publish

- Passwords, access tokens, refresh tokens, client secrets, API keys, private keys, or certificate material
- Real user names, email addresses, phone numbers, employee IDs, or personal information
- Real tenant-specific or employer-specific information unless explicitly approved for public disclosure
- Confidential application names, internal URLs, IP addresses, network diagrams, or security configurations
- Unredacted sign-in, audit, provisioning, or diagnostic logs

## Use synthetic examples

Use clearly fictional user identifiers, application names, group names, and tenant context. Where command output comes from a lab, review it before publishing and replace identifiers that should not be public.

## Evidence quality

For each evidence item, explain:
1. What question was being investigated?
2. What command or source produced the evidence?
3. What relevant result was observed?
4. What conclusion does it support?
5. What does it not establish?

Prefer small, focused evidence extracts over large raw dumps.

## Accuracy

- Preserve the actual command used and the relevant output.
- Do not invent results or reconstruct output as though it were collected.
- Mark examples as illustrative when they are not actual captured evidence.
- Distinguish confirmed findings, probable explanations, and unresolved questions.
- Record the date of the lab exercise and relevant SDK/environment context when useful.
- If a permission prevented a check, state that limitation.

## Permissions and change safety

- Use read-only permissions for investigation wherever possible.
- Do not request broad Graph permissions without a justified need.
- Never store credentials in scripts, screenshots, transcript files, or repository secrets.
- Treat write operations as separate, explicitly authorized change steps.
- Record pre-change state, intended change, result, and validation for any authorized write.

## Before every public commit

- [ ] Search for secrets and tokens.
- [ ] Review identifiers and log data.
- [ ] Remove personal and organization-specific data.
- [ ] Confirm screenshots are readable and sanitized.
- [ ] Verify statements match the actual evidence.
- [ ] Confirm lab scenarios are labelled as simulated.
