---
name: silver-onboard
description: Guided Silver Member onboarding — walk a new Silver member through identity verification, LFX setup, working group selection, colleague invitations, events, newsletters, and community access.
---

# Silver Member Onboarding Flow

Walk a new Silver Member through complete AAIF onboarding in 8 conversational phases. This is a guided, interactive flow — ask questions, confirm answers, and use MCP tools at each step.

**Important:** Always use `dry_run=True` first for any write operations, show the user what will happen, and get confirmation before executing with `dry_run=False`.

## Phase 1 — Welcome & Identity Verification

1. Greet the member warmly and ask for:
   - Full name
   - Organization name
   - Role/title
   - Email address
2. Call `validate_membership_tier(org_id)` to confirm Silver tier status
3. Call `list_contacts(org_id)` to check if they're already in the system
4. If new contact: `add_contact(org_id, name, email, "primary_contact", dry_run=True)` → show what will happen → confirm → execute with `dry_run=False`
5. If contact exists: confirm their details are correct, offer to update role if needed via `update_contact_role`

## Phase 2 — LFX Account Setup

1. Ask if they already have an LFX (Linux Foundation) account
2. If **no**: Direct them to create one at https://myprofile.lfx.linuxfoundation.org/
   - Explain this is their single sign-on for all LF tools
   - Offer to wait while they set it up
3. If **yes**: Confirm their LFID is linked to their organization
4. Track progress via `get_onboarding_status(org_id, contact_id)`

## Phase 3 — Working Group Selection

1. Call `list_available_working_groups(contact_id)` to show all 7 WGs with descriptions:
   - **Agentic Commerce** — Standards for AI agent-to-agent transactions (Wed 9am PT)
   - **Accuracy & Reliability** — Benchmarking and testing frameworks (Tue 9am PT)
   - **Identity & Trust** — Authentication and trust for AI agents (Thu 9am PT)
   - **Observability & Traceability** — Monitoring and debugging agent systems (Wed 10am PT)
   - **Workflows & Process Integration** — Multi-agent orchestration patterns (Thu 8am PT)
   - **Governance, Risk & Regulatory Alignment** — Policy and compliance frameworks (Thu 10am PT biweekly)
   - **Security & Privacy** — Security architecture and data protection (Tue 10am PT biweekly)
2. Ask which WGs interest them (they can join multiple)
3. For each selected WG:
   - `check_wg_eligibility(contact_id, wg_id)` → verify they can join
   - `enroll_in_working_group(contact_id, wg_id, dry_run=True)` → show enrollment across Groups.io, Discord, GitHub, Calendar
   - Confirm → execute with `dry_run=False`
4. Mention that WG chairs must be Gold+ tier, but Silver members can actively participate

## Phase 4 — Invite Colleagues

1. Ask if they'd like to add colleagues from their organization
2. Remind them Silver tier allows up to 5 contacts total
3. For each colleague:
   - Collect name, email, and role
   - `add_contact(org_id, name, email, role, dry_run=True)` → confirm → execute
   - `provision_mailing_lists(org_id, contact_email, dry_run=True)` → confirm → execute
   - Optionally enroll them in the same working groups
4. Offer to generate an invitation email template they can send to colleagues

## Phase 5 — Upcoming Events

1. Present upcoming AAIF events:
   - **MCP Dev Summit NA** — San Francisco (discount code: 20MCPNA25 for 20% off)
   - **MCP Dev Summit EU** — Amsterdam
   - **AGNTCon** — Co-located with Open Source Summit
2. `provision_calendar_invites(org_id, contact_id, dry_run=True)` for eligible events
3. Share registration links and member discount codes
4. Mention that Silver members get event member pricing

## Phase 6 — Newsletter & Mailing Lists

1. `provision_mailing_lists(org_id, contact_email, dry_run=True)` → show Silver-tier lists (members-all)
2. Confirm → execute with `dry_run=False`
3. Explain the biweekly AAIF newsletter with WG updates, event announcements, and project news
4. Offer to subscribe colleagues added in Phase 4

## Phase 7 — Community Access

1. Share the AAIF Discord invite link for real-time community discussion
2. Ask for their GitHub username to provision repository access for WG repos
3. `get_upcoming_meetings(contact_id)` to show their personalized meeting calendar
4. Point them to key resources:
   - AAIF website: https://aaif.io
   - LFX Platform: https://lfx.linuxfoundation.org
   - Community calendar for all WG meetings

## Phase 8 — Summary & Verification

1. `get_onboarding_status(org_id, contact_id)` — show D1–D5 progress
2. `check_mailing_list_membership(contact_email)` — verify list subscriptions are correct
3. `reconcile_silos(org_id)` — cross-system sync check
4. Present a recap of everything completed:
   - Contact added and verified
   - Working groups enrolled
   - Mailing lists provisioned
   - Calendar invites sent
   - Colleagues invited (if any)
5. List any remaining action items (LFX account creation, logo submission, etc.)
6. Provide their key contacts at LF for ongoing support
7. Thank them and welcome them to AAIF!
