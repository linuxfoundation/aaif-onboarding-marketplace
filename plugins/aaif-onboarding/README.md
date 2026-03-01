# AAIF PMO Agent — Cowork Plugin

Cowork plugin for executives and leadership to interact with the AAIF PMO Agent. Connects to the AAIF MCP Server (49 tools across 12 domains) and provides domain knowledge, slash commands, and guided workflows. Designed for Claude Desktop's Cowork tab — just drag and drop to install.

> **Who is this for?** Executives and leadership who want conversational AI access to member onboarding status, compliance reports, renewal dashboards, and ad-hoc questions. PMO staff doing day-to-day operations use LFX PCC instead.

## Setup

### 1. Install the plugin

Double-click `aaif-onboarding.plugin` or drag it into Claude Desktop/Cowork.

### 2. Configure the MCP server connection

Set these environment variables (or the plugin will use defaults):

| Variable | Description | Default |
|---|---|---|
| `AAIF_MCP_URL` | MCP server URL | `https://aaif-mcp-server.lfx.dev/mcp` |
| `AAIF_MCP_API_KEY` | API key for authentication | (none) |

**For local development** (running the MCP server on your machine), update `.mcp.json` to use stdio transport instead of HTTP.

## Commands

| Command | Description |
|---|---|
| `/onboard [org] [email]` | Full D1-D5 onboarding flow for a new member contact |
| `/offboard [org] [email] [reason]` | Remove a contact's access across all systems |
| `/health-check` | Foundation-wide health scan (anomalies, list gaps, silo sync, renewals, churn) |
| `/lookup [org]` | Comprehensive member profile with compliance and sync status |
| `/silver-onboard` | Guided 8-phase Silver Member onboarding (identity, LFX setup, WGs, events, community) |

## Skill

The **aaif-onboarding** skill activates automatically when you ask about member onboarding, tier validation, compliance, mailing lists, working groups, elections, renewals, or AAIF membership. It provides domain knowledge about tiers, D1-D5 deliverables, provisioning rules, and workflow patterns across all 12 domains.

## Components

| Type | Count | Purpose |
|------|-------|---------|
| Skills | 1 | AAIF onboarding domain knowledge |
| Commands | 5 | /onboard, /offboard, /health-check, /lookup, /silver-onboard |
| MCP Servers | 1 | AAIF MCP Server (49 tools via HTTP) |

## Tools Available (via MCP)

- **Tier Validation** (3): validate_membership_tier, check_tier_entitlements, detect_tier_anomalies
- **Compliance** (4): check_sanctions, check_tax_exempt_status, get_compliance_report, flag_compliance_issue
- **Mailing Lists** (4): provision_mailing_lists, remove_from_mailing_lists, check_mailing_list_membership, remediate_mailing_lists
- **Contact Roles** (5): list_contacts, add_contact, update_contact_role, remove_contact, transfer_voting_rights
- **Calendar** (3): provision_calendar_invites, update_meeting_schedule, get_upcoming_meetings
- **Working Groups** (5): enroll_in_working_group, leave_working_group, list_available_working_groups, get_wg_members, check_wg_eligibility
- **Elections** (5): create_election, validate_candidate_eligibility, check_voter_eligibility, get_election_status, diagnose_ballot_access
- **Press Releases** (3): draft_press_release, get_press_release_status, list_press_release_templates
- **Logo & Brand** (3): validate_logo, get_brand_guidelines, request_logo_upload
- **Onboarding Calls** (3): schedule_onboarding_call, reschedule_onboarding_call, get_onboarding_call_status
- **Renewal Intelligence** (5): get_renewal_status, get_engagement_score, predict_churn_risk, get_renewal_dashboard, trigger_renewal_outreach
- **Orchestration** (5): run_onboarding_checklist, get_onboarding_status, reconcile_silos, run_offboarding_checklist, get_silo_health
- **Health Check** (1): tool_health_check
