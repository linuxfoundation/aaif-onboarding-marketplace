# AAIF PMO Agent — Plugin Marketplace

Private Claude plugin marketplace for the AAIF PMO Agent. The Cowork plugin gives executives and leadership conversational AI access to all 49 onboarding tools. PMO staff access the same tools through LFX PCC.

## Quick Install

```bash
/plugin marketplace add LF-Engineering/aaif-onboarding-marketplace
/plugin install aaif-onboarding@aaif-onboarding-marketplace
```

That's it. The plugin connects to the AAIF MCP Server and gives you 49 tools across 12 domains:

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

The MCP server is hosted on LFX infrastructure:
- **URL**: `https://aaif-mcp-server.lfx.dev/mcp`

## Questions

Contact Manish Dixit (mdixit@linuxfoundation.org)
