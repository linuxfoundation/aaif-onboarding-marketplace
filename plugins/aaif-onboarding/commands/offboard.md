---
description: Offboard an AAIF member contact
argument-hint: [org-name] [contact-email] [reason]
---

Run the AAIF contact offboarding flow.

If the user provided an org name, contact email, and reason, use those. Otherwise ask for them. Valid reasons are: membership_cancelled, tier_downgrade, contact_inactive.

Follow these steps:

1. **Check current access** — Call `check_mailing_list_membership` for the contact email. Show what they're currently subscribed to.

2. **Preview offboarding** — Call `run_offboarding_checklist` with `dry_run=True`. Show the automated actions (list removals) and manual follow-ups (Discord, GitHub, calendar, CRM).

3. **Confirm with user** — Ask the user to confirm they want to proceed. Only after explicit confirmation, execute with `dry_run=False`.

4. **Verify** — Call `check_mailing_list_membership` again to confirm the contact has been removed from all lists.

Present a summary of what was done and what manual steps remain.
