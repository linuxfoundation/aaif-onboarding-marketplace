---
name: aaif-onboarding
description: >
  Use this skill when the user asks about "AAIF member onboarding", "new member setup",
  "membership tier validation", "mailing list provisioning", "compliance screening",
  "silo health", "onboarding checklist", "D1-D5 deliverables", "member offboarding",
  "working group enrollment", "election management", "press release drafting",
  "logo validation", "renewal intelligence", "churn prediction", "engagement scoring",
  "contact role management", "calendar provisioning", "onboarding call scheduling",
  or any task related to managing Linux Foundation AAIF member organizations,
  contacts, and their access across Salesforce, Groups.io, Google Calendar,
  Discord, GitHub, LFX Platform, and HubSpot systems.
version: 0.2.0
---

# AAIF Member Onboarding

Domain knowledge for the AI & Agentic Infrastructure Foundation member onboarding lifecycle.

## Foundation Context

AAIF is a Linux Foundation project hosting MCP (Anthropic), Goose (Block), and AGENTS.md (OpenAI). Members are companies that pay annual dues and receive tiered benefits.

## Membership Tiers

| Tier | GB Seats | Voting | TC Eligible | Max Contacts | Key Lists |
|------|----------|--------|-------------|-------------|-----------|
| Platinum | 2 | Yes | Yes | 10 | governing-board, technical-committee, members-all |
| Gold | 1 | Yes | Yes | 8 | governing-board, members-all |
| Silver | 0 | No | No | 5 | members-all |

## D1-D5 Onboarding Deliverables

Every new member goes through five deliverables:

- **D1 — Agreement & Activation** (3 steps): Tier validation, sanctions/compliance screening (via Descartes in SFDC), tax-exempt verification
- **D2 — Membership Record** (3 steps): CRM record validation, contacts collected by role, member tracker synced
- **D3 — Participation Enablement** (5 steps): Mailing lists, calendar invites, working group enrollment, Discord, GitHub
- **D4 — Orientation** (2 steps): Welcome email, onboarding call
- **D5 — Visibility** (3 steps): Logo collection, press release, website/landscape update

## Contact Roles

Each member organization has contacts assigned to roles:

- **voting_contact** — Represents org on governing board, gets full list access
- **technical_contact** — Participates in technical committee and working groups
- **primary_contact** — Main point of contact, administrative role
- **billing_contact** — Invoicing and payment

## Available MCP Tools

There are 49 tools across 12 domains (48 auto-registered via dynamic registry + 1 health check). Architecture review complete: 14/14 findings resolved. 123 tests passing. Always default to `dry_run=True` for any write operations and confirm with the user before setting `dry_run=False`.

### Domain 1: Mailing List Provisioning (4 tools)
- `provision_mailing_lists(org_id, contact_email, dry_run=True)` — Add contact to tier-appropriate lists
- `remove_from_mailing_lists(org_id, contact_email, dry_run=True)` — Remove from all lists
- `check_mailing_list_membership(contact_email)` — Check subscription status across all lists
- `remediate_mailing_lists(dry_run=True)` — Foundation-wide gap detection and remediation

### Domain 2: Calendar & Meeting Management (3 tools)
- `provision_calendar_invites(org_id, contact_id, dry_run=True)` — Send calendar invites based on tier/role
- `update_meeting_schedule(wg_id, new_time, new_link)` — Update WG recurring meeting time/link
- `get_upcoming_meetings(contact_id)` — Get upcoming meetings for a contact

### Domain 3: Compliance & Sanctions (4 tools)
- `check_sanctions(org_name, country, org_id)` — Look up Descartes screening status from SFDC
- `check_tax_exempt_status(org_id)` — Verify 501(c)(6) compliance
- `get_compliance_report(org_id)` — Full compliance summary
- `flag_compliance_issue(org_id, issue_type, details)` — Create ticket for human review

### Domain 4: Tier Validation (3 tools)
- `validate_membership_tier(org_id)` — Look up org tier, entitlements, contract expiry, anomalies
- `check_tier_entitlements(tier)` — Return the entitlement matrix for platinum/gold/silver
- `detect_tier_anomalies()` — Scan all members for access mismatches

### Domain 5: Contact Role Management (5 tools)
- `list_contacts(org_id)` — List all contacts with roles and downstream access
- `add_contact(org_id, name, email, role, dry_run=True)` — Add contact, trigger downstream provisioning
- `update_contact_role(org_id, contact_id, new_role, dry_run=True)` — Change role, show downstream effects
- `remove_contact(org_id, contact_id, dry_run=True)` — Remove contact, trigger offboarding
- `transfer_voting_rights(org_id, from_contact_id, to_contact_id)` — Transfer voting rights between contacts

### Domain 6: Working Group Enrollment (5 tools)
- `enroll_in_working_group(contact_id, wg_id, dry_run=True)` — Enroll across Groups.io + Discord + GitHub + Calendar
- `leave_working_group(contact_id, wg_id, dry_run=True)` — Remove from WG across all systems
- `list_available_working_groups(contact_id)` — List WGs with enrollment status
- `get_wg_members(wg_id)` — Get WG member roster
- `check_wg_eligibility(contact_id, wg_id)` — Check tier/role eligibility for a WG

### Domain 7: Election & Voting Operations (5 tools)
- `create_election(wg_id, election_type, nomination_start, nomination_end, voting_start, voting_end)` — Create WG chair election
- `validate_candidate_eligibility(contact_id, election_id)` — Check candidate prerequisites
- `check_voter_eligibility(contact_id, election_id)` — Check voting contact status
- `get_election_status(election_id)` — Get election timeline, candidates, votes
- `diagnose_ballot_access(contact_id, election_id)` — Diagnose all blockers for ballot access

### Domain 8: Press Release Drafting (3 tools)
- `draft_press_release(org_id, template_id)` — Generate press release from template + org data
- `get_press_release_status(pr_id)` — Check approval workflow progress
- `list_press_release_templates()` — List available PR templates

### Domain 9: Logo & Brand Validation (3 tools)
- `validate_logo(file_url)` — Validate logo against brand guidelines (SVG, min 1000x1000)
- `get_brand_guidelines()` — Retrieve brand specs and requirements
- `request_logo_upload(org_id)` — Generate secure upload URL for logo submission

### Domain 10: Onboarding Call Scheduling (3 tools)
- `schedule_onboarding_call(org_id, contact_ids, lf_staff_ids)` — Schedule call with contacts and LF staff
- `reschedule_onboarding_call(meeting_id, new_time)` — Reschedule an existing call
- `get_onboarding_call_status(org_id)` — Check call status (scheduled/pending/done)

### Domain 11: Renewal & Engagement Intelligence (5 tools)
- `get_renewal_status(org_id)` — Contract renewal timeline and stage
- `get_engagement_score(org_id)` — Calculate engagement score (0-100) with breakdown
- `predict_churn_risk(org_id)` — Predict churn risk (0-100) with contributing factors
- `get_renewal_dashboard()` — Foundation-wide renewal pipeline view
- `trigger_renewal_outreach(org_id, dry_run=True)` — Generate outreach plan with email template

### Domain 12: Orchestration (5 tools)
- `run_onboarding_checklist(org_id, contact_id, dry_run=True)` — Execute full D1-D5 flow
- `get_onboarding_status(org_id, contact_id)` — Check progress on each deliverable and step
- `reconcile_silos(org_id)` — Compare SFDC vs Groups.io vs SSO for discrepancies
- `run_offboarding_checklist(org_id, contact_email, reason, dry_run=True)` — Remove access on departure
- `get_silo_health()` — Foundation-wide sync health score

## Workflow Patterns

### New Member Onboarding (Full D1-D5)
1. `validate_membership_tier` → confirm tier and entitlements
2. `get_compliance_report` → verify sanctions and tax-exempt status
3. `list_contacts` → review contact roles
4. `provision_mailing_lists` (dry_run) → preview list additions, confirm, then execute
5. `provision_calendar_invites` (dry_run) → preview calendar invites
6. `enroll_in_working_group` → enroll in selected WGs
7. `schedule_onboarding_call` → book orientation call
8. `draft_press_release` → generate announcement
9. `request_logo_upload` → get logo upload URL
10. `run_onboarding_checklist` (dry_run) → preview full D1-D5, confirm, then execute
11. `reconcile_silos` → verify everything is in sync

### Working Group Enrollment
1. `list_available_working_groups` → show WGs with eligibility
2. `check_wg_eligibility` → verify contact can join
3. `enroll_in_working_group` (dry_run) → preview multi-system enrollment
4. Confirm → execute with `dry_run=False`
5. `get_upcoming_meetings` → show next meetings

### Election Management
1. `create_election` → set up WG chair election
2. `validate_candidate_eligibility` → check candidate prerequisites
3. `check_voter_eligibility` → verify voter status
4. `get_election_status` → monitor election progress
5. `diagnose_ballot_access` → troubleshoot access issues

### Renewal & Churn Prevention
1. `get_renewal_dashboard` → foundation-wide pipeline view
2. `predict_churn_risk` → identify at-risk members
3. `get_engagement_score` → understand engagement breakdown
4. `get_renewal_status` → check specific org renewal timeline
5. `trigger_renewal_outreach` (dry_run) → preview outreach plan

### Quarterly Health Check
1. `detect_tier_anomalies` → find access mismatches
2. `remediate_mailing_lists` (dry_run) → preview fixes
3. `get_silo_health` → overall sync score
4. `get_renewal_dashboard` → renewal pipeline status

### Contact Offboarding
1. `check_mailing_list_membership` → see current subscriptions
2. `run_offboarding_checklist` (dry_run) → preview removals
3. Confirm with user → execute with `dry_run=False`

### Silver Member Onboarding (Guided 8-Phase Flow)
Use `/silver-onboard` for the full conversational flow. Phases:
1. **Welcome & Identity** — `validate_membership_tier` → `list_contacts` → `add_contact`
2. **LFX Account Setup** — Direct to myprofile.lfx.linuxfoundation.org
3. **Working Group Selection** — `list_available_working_groups` (7 WGs) → `check_wg_eligibility` → `enroll_in_working_group`
4. **Invite Colleagues** — `add_contact` → `provision_mailing_lists` → `enroll_in_working_group`
5. **Events** — Present MCP Dev Summit, AGNTCon with discount codes → `provision_calendar_invites`
6. **Newsletter & Lists** — `provision_mailing_lists` for Silver tier (members-all)
7. **Community Access** — Discord invite, GitHub username, `get_upcoming_meetings`
8. **Summary & Verification** — `get_onboarding_status` → `check_mailing_list_membership` → `reconcile_silos`

## Important Notes

- Sanctions screening is handled by the Descartes integration in Salesforce at membership intake — the MCP server reads that status, it does not run its own screening
- Always show dry_run results to the user before executing write operations
- The server auto-falls back to mock data when backend credentials are not configured
- Mock members include: Hitachi (Gold), Bloomberg (Gold), Natoma (Silver), iProov (Silver), OpenAI (Platinum)
- 7 connectors: Salesforce, Groups.io, Google Calendar, Discord, GitHub, LFX Platform, HubSpot
- Working groups (7): Agentic Commerce, Accuracy & Reliability, Identity & Trust, Observability, Workflows, Governance Risk & Regulatory, Security & Privacy

For detailed provisioning rules and working group definitions, see `references/provisioning-rules.md`.
