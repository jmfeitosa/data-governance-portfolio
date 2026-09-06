# Access operating model

[Back to the case](README.md)

## Scope

This demonstration governs human access to three fictional resources: a metadata catalog, a restricted operational dataset and an approved analytical view. Service identities require a separate catalog entry with a technical owner, workload purpose and credential/identity lifecycle; they must not inherit human roles automatically.

## Design rules

1. Deny any action absent from the approved matrix.
2. Grant the smallest resource scope and duration that meet the approved purpose.
3. Treat job title, project membership and requester preference as context, not authorization.
4. Keep request, approval, implementation and verification as distinct recorded events.
5. Resolve conflicting group memberships and direct grants before declaring an effective permission safe.
6. End temporary access automatically where supported, and verify the result.
7. Treat emergency access as a separately controlled exception, not a reusable standing role.

## Responsibilities

| Role | Accountability in this model |
| --- | --- |
| Requester | States purpose, requested scope, duration and business sponsor |
| Manager / sponsor | Confirms business assignment; cannot replace resource-owner approval |
| Data Owner | Approves or denies resource access and acceptable purpose |
| Data Steward | Checks resource identity, classification and metadata completeness |
| Security reviewer | Assesses privileged access, conflicts and emergency exceptions |
| Privacy reviewer | Reviews proposed sensitive personal-data use when applicable |
| Custodian | Implements the approved entitlement and records the actual configuration |
| Independent verifier | Checks effective access and required removal |
| Governance coordinator | Maintains catalog, campaign scope, exceptions and overdue actions |

The requester must not approve their own access. A custodian cannot unilaterally approve permissions they will receive. If staffing prevents independent implementation and verification, record an approved compensating review; do not silently mark independence as satisfied.

## Role catalog

| Role ID | Role | Intended scope | Maximum demo grant |
| --- | --- | --- | --- |
| R-CAT | Catalog reader | Read approved catalog metadata only | 90 days |
| R-ANL | Analytics reader | Query an approved analytical view | 90 days |
| R-STW | Metadata steward | Edit metadata in an assigned domain | 90 days |
| R-OPS | Access operator | Implement approved access changes | 30 days |
| R-AUD | Evidence reviewer | Read an approved evidence collection | 30 days |

These durations are illustrative configuration choices, not standard or legal requirements. Renewal is a new decision supported by a current purpose, not an automatic extension.

## Exception register

Record exception ID, affected entitlement, reason, conflict or unmet control, risk owner, independent approver, compensating control, start, expiry and closure evidence. An expired exception does not authorize continued access. Route unresolved expiry to the accountable owner and suspend the exception grant when policy requires.

## Boundaries

The matrix documents authorization intent. It does not itself configure database privileges, identity-provider groups, row-level security, export controls or Power BI workspace roles. Implementation must map every logical permission to a concrete platform control and test the resulting effective access.
