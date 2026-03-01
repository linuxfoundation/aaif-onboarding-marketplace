---
description: Look up an AAIF member org's full profile
argument-hint: [org-name-or-id]
---

Look up everything about an AAIF member organization.

Call these tools and compile a comprehensive profile:

1. `validate_membership_tier` — Tier, entitlements, contract expiry, anomalies
2. `get_compliance_report` — Sanctions and tax-exempt status
3. `list_contacts` — All contacts with roles and access
4. `reconcile_silos` — Cross-system sync status
5. `get_renewal_status` — Contract renewal timeline and stage
6. `get_engagement_score` — Engagement score with breakdown
7. `predict_churn_risk` — Churn risk assessment
8. `get_onboarding_call_status` — Onboarding call status

Present a clean summary with:
- Organization name, tier, and status
- Contract expiry date and renewal stage
- Entitlements (board seats, voting rights, max contacts, mailing lists)
- Compliance status (sanctions clear/flagged, tax-exempt status)
- Contact list with their roles and mailing list subscriptions
- Working group enrollments per contact
- Engagement score and churn risk
- Silo sync status (any discrepancies between SFDC, Groups.io, Calendar, Discord, GitHub)
- Onboarding call status
