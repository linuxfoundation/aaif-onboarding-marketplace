# Provisioning Rules

Detailed rules for which mailing lists each contact role gets access to, by tier.

## Rule Matrix

| Tier | Role | Lists |
|------|------|-------|
| Platinum | voting_contact | governing-board, technical-committee, members-all |
| Platinum | technical_contact | technical-committee, members-all |
| Platinum | primary_contact | members-all |
| Gold | voting_contact | governing-board, members-all |
| Gold | technical_contact | members-all |
| Gold | primary_contact | members-all |
| Silver | voting_contact | members-all |
| Silver | technical_contact | members-all |
| Silver | primary_contact | members-all |

## Working Groups

All working groups are open to any tier member who requests participation:

| Working Group | List | Chair Eligible |
|--------------|------|----------------|
| Accuracy & Reliability | wg-accuracy-reliability@lists.aaif.io | Gold+ |
| Agentic Commerce | wg-agentic-commerce@lists.aaif.io | Gold+ |
| Identity & Trust | wg-identity-trust@lists.aaif.io | Gold+ |
| Observability | wg-observability@lists.aaif.io | Gold+ |
| Workflows | wg-workflows@lists.aaif.io | Gold+ |

## Anomaly Detection Rules

An anomaly is flagged when:
- A contact is on a list they shouldn't have access to per their tier/role (EXCESS_ACCESS)
- A contact is missing from a list they should be on per their tier/role (MISSING_ACCESS)
- A contact's role doesn't match what's in SFDC (ROLE_MISMATCH)

Severity levels:
- **high** — Platinum/Gold member missing governing board access
- **medium** — Any member missing their expected list subscriptions
- **low** — Informational discrepancies (e.g., extra working group subscriptions)
