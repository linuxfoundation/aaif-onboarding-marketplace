---
description: Look up an AAIF member org's full profile
argument-hint: [org-name-or-id]
---

Look up everything about an AAIF member organization.

Call these tools and compile a comprehensive profile:

1. `validate_membership_tier` — Tier, entitlements, contract expiry, anomalies
2. `get_compliance_report` — Sanctions and tax-exempt status
3. `reconcile_silos` — Cross-system sync status

Present a clean summary with:
- Organization name, tier, and status
- Contract expiry date
- Entitlements (board seats, voting rights, max contacts, mailing lists)
- Compliance status (sanctions clear/flagged, tax-exempt status)
- Silo sync status (any discrepancies between SFDC, Groups.io, SSO)
- Contact list with their roles and mailing list subscriptions
