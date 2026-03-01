---
name: aaif-onboarding
description: >
  Use this skill when the user asks about "AAIF member onboarding", "new member setup",
  "membership tier validation", "mailing list provisioning", "compliance screening",
  "silo health", "onboarding checklist", "D1-D5 deliverables", "member offboarding",
  or any task related to managing Linux Foundation AAIF member organizations,
  contacts, and their access across Salesforce, Groups.io, and SSO systems.
version: 0.1.0
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

Every new member goes through five deliverables with 16 total steps:

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

There are 16 tools across 4 domains. Always default to `dry_run=True` for any write operations and confirm with the user before setting `dry_run=False`.

### Tier Validation (3 tools)
- `validate_membership_tier(org_id)` — Look up org tier, entitlements, contract expiry, anomalies
- `check_tier_entitlements(tier)` — Return the entitlement matrix for platinum/gold/silver
- `detect_tier_anomalies()` — Scan all members for access mismatches

### Compliance (4 tools)
- `check_sanctions(org_name, country, org_id)` — Look up Descartes screening status from SFDC (sanctions handled at membership intake)
- `check_tax_exempt_status(org_id)` — Verify 501(c)(6) compliance
- `get_compliance_report(org_id)` — Full compliance summary
- `flag_compliance_issue(org_id, issue_type, details)` — Create ticket for human review

### Mailing Lists (4 tools)
- `provision_mailing_lists(org_id, contact_email, dry_run=True)` — Add contact to tier-appropriate lists
- `remove_from_mailing_lists(org_id, contact_email, dry_run=True)` — Remove from all lists
- `check_mailing_list_membership(contact_email)` — Check subscription status across all lists
- `remediate_mailing_lists(dry_run=True)` — Foundation-wide gap detection and remediation

### Orchestration (5 tools)
- `run_onboarding_checklist(org_id, contact_id, dry_run=True)` — Execute full D1-D5 flow
- `get_onboarding_status(org_id, contact_id)` — Check progress on each deliverable and step
- `reconcile_silos(org_id)` — Compare SFDC vs Groups.io vs SSO for discrepancies
- `run_offboarding_checklist(org_id, contact_email, reason, dry_run=True)` — Remove access on departure
- `get_silo_health()` — Foundation-wide sync health score

## Workflow Patterns

### New Member Onboarding
1. `validate_membership_tier` → confirm tier and entitlements
2. `get_compliance_report` → verify sanctions and tax-exempt status
3. `provision_mailing_lists` (dry_run) → preview list additions, confirm, then execute
4. `run_onboarding_checklist` (dry_run) → preview full D1-D5, confirm, then execute
5. `reconcile_silos` → verify everything is in sync

### Quarterly Health Check
1. `detect_tier_anomalies` → find access mismatches
2. `remediate_mailing_lists` (dry_run) → preview fixes
3. `get_silo_health` → overall sync score

### Contact Offboarding
1. `check_mailing_list_membership` → see current subscriptions
2. `run_offboarding_checklist` (dry_run) → preview removals
3. Confirm with user → execute with `dry_run=False`

## Important Notes

- Sanctions screening is handled by the Descartes integration in Salesforce at membership intake — the MCP server reads that status, it does not run its own screening
- Always show dry_run results to the user before executing write operations
- The server auto-falls back to mock data when SFDC/Groups.io credentials are not configured
- Mock members include: Hitachi (Gold), Bloomberg (Gold), Natoma (Silver), iProov (Silver), OpenAI (Platinum)

For detailed provisioning rules and working group definitions, see `references/provisioning-rules.md`.
