---
description: Onboard a new AAIF member contact (full D1-D5 flow)
argument-hint: [org-name] [contact-email]
---

Run the complete AAIF member onboarding flow for the given organization and contact.

If the user provided an org name or contact email, use those. Otherwise ask for them.

Follow these steps in order:

1. **Validate membership tier** — Call `validate_membership_tier` with the org ID. Confirm the tier, entitlements, and contract expiry with the user.

2. **Compliance check** — Call `get_compliance_report` to verify sanctions screening (Descartes) and tax-exempt status are clear. If any issues are flagged, stop and alert the user.

3. **Check contacts** — Call `list_contacts` for the org. Show existing contacts and their roles. If the contact being onboarded isn't listed, offer to call `add_contact` to add them.

4. **Check current mailing list status** — Call `check_mailing_list_membership` for the contact email. Show which lists they're currently on vs. what they should be on.

5. **Provision mailing lists (dry run first)** — Call `provision_mailing_lists` with `dry_run=True`. Show the planned actions and ask the user to confirm before executing with `dry_run=False`.

6. **Provision calendar invites (dry run first)** — Call `provision_calendar_invites` with `dry_run=True`. Show the calendar invites that will be sent, confirm, then execute.

7. **Working group enrollment** — Call `list_available_working_groups` to show available WGs. If the user wants to enroll the contact in any WGs, call `check_wg_eligibility` first, then `enroll_in_working_group` with `dry_run=True`.

8. **Schedule onboarding call** — Call `schedule_onboarding_call` to book an orientation call with the contact and LF staff.

9. **Press release & logo** — Call `draft_press_release` to generate a member announcement. Call `request_logo_upload` to get a secure URL for logo submission.

10. **Run full onboarding checklist (dry run first)** — Call `run_onboarding_checklist` with `dry_run=True`. Show the D1-D5 deliverables and steps. Ask user to confirm before executing.

11. **Verify** — Call `reconcile_silos` to confirm everything is in sync.

Present a summary at the end showing what was completed, what needs manual follow-up, and any issues found.
