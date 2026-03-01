---
description: Run AAIF foundation-wide health check
---

Run a comprehensive health check across all AAIF member organizations.

Execute these checks in order and present a unified report:

1. **Tier anomaly scan** — Call `detect_tier_anomalies`. Report any members with access mismatches.

2. **Mailing list remediation scan** — Call `remediate_mailing_lists` with `dry_run=True`. Report gaps found and proposed fixes.

3. **Silo health** — Call `get_silo_health`. Report the overall sync score, members in sync vs. with issues, and top discrepancies.

Present the results as a single dashboard-style summary with:
- Overall health score (from silo health)
- Number of anomalies found
- Number of mailing list gaps
- Top 5 issues requiring attention
- Recommended next actions

If the user wants to fix any issues, offer to run `remediate_mailing_lists` with `dry_run=False` after confirmation.
