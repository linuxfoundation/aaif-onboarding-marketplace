# AAIF Onboarding Marketplace

Private Claude plugin marketplace for the AI & Agentic Infrastructure Foundation (AAIF) member onboarding tools.

## Quick Install

```bash
/plugin marketplace add LF-Engineering/aaif-onboarding-marketplace
/plugin install aaif-onboarding@aaif-onboarding-marketplace
```

That's it. The plugin connects to the AAIF MCP Server on Railway and gives you 16 tools across 4 domains:

| Domain | Tools |
|--------|-------|
| Tier Validation | validate_membership_tier, check_tier_entitlements, detect_tier_anomalies |
| Compliance | check_sanctions, check_tax_exempt_status, get_compliance_report, flag_compliance_issue |
| Mailing Lists | provision_mailing_lists, remove_from_mailing_lists, check_mailing_list_membership, remediate_mailing_lists |
| Orchestration | run_onboarding_checklist, get_onboarding_status, reconcile_silos, run_offboarding_checklist, get_silo_health |

## Commands

| Command | Description |
|---------|-------------|
| `/onboard [org] [email]` | Full D1-D5 onboarding flow |
| `/offboard [org] [email] [reason]` | Remove access across all systems |
| `/health-check` | Foundation-wide health scan |
| `/lookup [org]` | Member profile with compliance status |

## Server

The MCP server is hosted on Railway:
- **URL**: `https://aaif-mcp-server-production.up.railway.app/mcp`
- Auto-sleeps on inactivity (first request may take 5-10s)

## Questions

Contact Manish Dixit (mdixit@linuxfoundation.org)
