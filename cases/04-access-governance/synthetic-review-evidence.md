# Synthetic access review evidence

[Back to the case](README.md)

**All rows, identifiers, dates and results below are invented for this demonstration. Evidence IDs are illustrative labels, not real files or audit attestations.**

Campaign: SYN-REV-001. Snapshot: 2026-09-01. Cutoff: 2026-09-06 23:59 UTC. Population: six entitlements; no exclusions. Reviewer roles represent separate fictional actors.

| Entitlement | Identity | Role / resource | Decision | Reason | Removal task | Due date | Verified removal |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SYN-E01 | SYN-U01 | R-CAT / RES-CAT | Retain | Current catalog purpose confirmed | — | — | Not applicable |
| SYN-E02 | SYN-U02 | R-STW / RES-CAT | Retain | Assigned domain confirmed | — | — | Not applicable |
| SYN-E03 | SYN-U03 | R-ANL / RES-VIEW | Revoke | Temporary assignment expired | SYN-T03 | 2026-09-04 | 2026-09-03 |
| SYN-E04 | SYN-U04 | R-OPS / access control | Revoke | Administrative assignment ended | SYN-T04 | 2026-09-05 | Pending |
| SYN-E05 | SYN-U05 | R-ANL / RES-VIEW | Modify | New assignment needs metadata only | SYN-T05 | 2026-09-05 | 2026-09-04 |
| SYN-E06 | SYN-U06 | R-AUD / RES-EV | Pending | Owner confirmation missing | — | — | Not applicable |

SYN-E05 requires removal of the old analytical entitlement and a separately approved catalog grant. The verified removal above proves only the old grant ended. This campaign does not claim that the replacement grant was implemented.

## Decision and implementation trail

| Record | Decision evidence | Implementation evidence | Independent verification |
| --- | --- | --- | --- |
| SYN-E01 | SYN-DEC-001: owner retained 2026-09-02 | No change | Next expiry/review recorded |
| SYN-E02 | SYN-DEC-002: owner retained 2026-09-02 | No change | Next expiry/review recorded |
| SYN-E03 | SYN-DEC-003: owner revoked 2026-09-02 | SYN-IMP-003: removal 2026-09-03 | SYN-EV-003: effective query denied 2026-09-03 |
| SYN-E04 | SYN-DEC-004: security/owner revoked 2026-09-02 | No completion evidence | Open; escalate as overdue |
| SYN-E05 | SYN-DEC-005: owner modified 2026-09-03 | SYN-IMP-005: old grant removed 2026-09-04 | SYN-EV-005: old query denied 2026-09-04 |
| SYN-E06 | No decision | No change | Pending owner response |

## Reconciliation

- Eligible: **6**.
- Decision recorded: **5** (2 Retain, 2 Revoke, 1 Modify).
- Decision pending: **1**.
- Removal required: **3**.
- Removal independently verified: **2**.
- Removal overdue and not verified: **1**.
- Campaign fully closed: **No**.

These are example process results, not improvements achieved for an employer or client.
