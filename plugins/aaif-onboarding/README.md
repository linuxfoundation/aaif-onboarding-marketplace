# AAIF Onboarding Plugin

Claude plugin for managing AI & Agentic Infrastructure Foundation member onboarding. Connects to the AAIF MCP Server (16 tools) and provides domain knowledge, slash commands, and guided workflows.

## Setup

### 1. Install the plugin

Double-click `aaif-onboarding.plugin` or drag it into Claude Desktop/Cowork.

### 2. Configure the MCP server connection

Set these environment variables (or the plugin will use defaults):

| Variable | Description | Default |
|---|---|---|
| `AAIF_MCP_URL` | MCP server URL | `https://aaif-mcp-server-production.up.railway.app/mcp` |
| `AAIF_MCP_API_KEY` | API key for authentication | (none) |

**For local development** (running the MCP server on your machine), update `.mcp.json` to use stdio transport instead of HTTP.

## Commands

| Command | Description |
|---|---|
| `/onboard [org] [email]` | Full D1-D5 onboarding flow for a new member contact |
| `/offboard [org] [email] [reason]` | Remove a contact's access across all systems |
| `/health-check` | Foundation-wide health scan (anomalies, list gaps, silo sync) |
| `/lookup [org]` | Comprehensive member profile with compliance and sync status |

## Skill

The **aaif-onboarding** skill activates automatically when you ask about member onboarding, tier validation, compliance, mailing lists, or AAIF membership. It provides domain knowledge about tiers, D1-D5 deliverables, provisioning rules, and workflow patterns.

## Components

| Type | Count | Purpose |
|------|-------|---------|
| Skills | 1 | AAIF onboarding domain knowledge |
| Commands | 4 | /onboard, /offboard, /health-check, /lookup |
| MCP Servers | 1 | AAIF MCP Server (16 tools via HTTP) |

## Tools Available (via MCP)

- **Tier Validation**: validate_membership_tier, check_tier_entitlements, detect_tier_anomalies
- **Compliance**: check_sanctions, check_tax_exempt_status, get_compliance_report, flag_compliance_issue
- **Mailing Lists**: provision_mailing_lists, remove_from_mailing_lists, check_mailing_list_membership, remediate_mailing_lists
- **Orchestration**: run_onboarding_checklist, get_onboarding_status, reconcile_silos, run_offboarding_checklist, get_silo_health
