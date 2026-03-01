---
description: Onboard a new AAIF member contact (full D1-D5 flow)
argument-hint: [org-name] [contact-email]
---

Run the complete AAIF member onboarding flow for the given organization and contact.

If the user provided an org name or contact email, use those. Otherwise ask for them.

Follow these steps in order:

1. **Validate membership tier** — Call `validate_membership_tier` with the org ID. Confirm the tier, entitlements, and contract expiry with the user.

2. **Compliance check** — Call `get_compliance_report` to verify sanctions screening (Descartes) and tax-exempt status are clear. If any issues are flagged, stop and alert the user.

3. **Check current mailing list status** — Call `check_mailing_list_membership` for the contact email. Show which lists they're currently on vs. what they should be on.

4. **Provision mailing lists (dry run first)** — Call `provision_mailing_lists` with `dry_run=True`. Show the planned actions and ask the user to confirm before executing with `dry_run=False`.

5. **Run onboarding checklist (dry run first)** — Call `run_onboarding_checklist` with `dry_run=True`. Show the D1-D5 deliverables and steps. Ask user to confirm before executing.

6. **Verify** — Call `reconcile_silos` to confirm everything is in sync.

Present a summary at the end showing what was completed, what needs manual follow-up, and any issues found.
