# Access permissions matrix

[Back to the case](README.md)

All resources and permissions are fictional. “Conditional” means the listed prerequisites must be met; it is not an implicit grant. Unlisted actions are denied.

## Resource catalog

| Resource ID | Resource | Classification | Accountable owner |
| --- | --- | --- | --- |
| RES-CAT | Domain A metadata catalog | Internal | Domain A Data Owner |
| RES-RAW | Operational source dataset | Restricted | Operational Data Owner |
| RES-VIEW | Approved analytical view | Internal | Analytics Data Owner |
| RES-EV | Access review evidence collection | Confidential | Governance Evidence Owner |

The analytical view is assumed to exclude restricted source fields. This assumption must be tested before applying its classification. Access to metadata can itself expose sensitive descriptions; catalog readers receive only the approved metadata scope.

## Entitlements

| Role | Read approved metadata | Edit domain metadata | Query analytical view | Read restricted source | Administer access | Read review evidence |
| --- | --- | --- | --- | --- | --- | --- |
| R-CAT | Conditional | Denied | Denied | Denied | Denied | Denied |
| R-ANL | Conditional | Denied | Conditional | Denied | Denied | Denied |
| R-STW | Conditional | Conditional | Denied | Denied | Denied | Denied |
| R-OPS | Denied | Denied | Denied | Denied | Conditional | Denied |
| R-AUD | Denied | Denied | Denied | Denied | Denied | Conditional |

No standard role permits RES-RAW access. A separately approved, scoped and expiring exception is required. Query permission does not automatically include bulk export, sharing, local copies or onward distribution.

## Prerequisites

| Permission | Required checks |
| --- | --- |
| Read metadata | Owner approval, active business purpose and approved metadata scope |
| Edit metadata | Owner approval, assigned domain, change traceability and prior-state recovery |
| Query analytical view | Owner approval, verified view definition, approved filters and export decision |
| Administer access | Security review, approved task, named operator, scoped privilege and independent verification |
| Read evidence | Evidence-owner approval, minimized content, retention restrictions and read logging |

## Separation of duties

- R-OPS must not approve the requests it implements.
- A requester cannot act as the final approving Data Owner for their own request.
- An R-STW assignment does not authorize source-data access.
- R-AUD must not edit the evidence it reviews.
- Resolve a conflicting combination by removing the conflicting grant or recording an independently approved, expiring exception.

## Verification examples

| Test | Expected |
| --- | --- |
| R-ANL queries RES-VIEW within approved scope | Allowed |
| R-ANL queries RES-RAW | Denied |
| R-STW edits metadata outside assigned domain | Denied |
| R-AUD attempts to alter a review record | Denied |
| Expired R-OPS assignment attempts administration | Denied |
| User with removed group but remaining direct grant | Removal verification fails |

Record the tested identity, resource, action, expected and observed outcomes, timestamp, verifier and evidence reference. A policy document alone is not proof that these tests passed.
