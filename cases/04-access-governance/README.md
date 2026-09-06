# Data Access Governance

[Back to portfolio](../../README.md)

> A demonstration operating model that connects business justification, role-based permissions, independent approval, expiry, and verified revocation.

## Business challenge

Access often accumulates after role changes, temporary assignments, and emergency support. Approval alone does not show that the implemented permission matches the decision or that it was removed when no longer needed.

## Proposed solution

Use a controlled role catalog, an explicit permissions matrix, request records, and periodic reviews. Separate the authority to approve access from the ability to implement it. Close a removal task only after effective access has been verified.

## Published artifacts

| Artifact | Decision supported |
| --- | --- |
| [Access operating model](access-model.md) | Which roles are permitted, and who is accountable? |
| [Permissions matrix](access-permissions-matrix.md) | What may each role do on each fictional resource? |
| [Request and revocation workflow](access-lifecycle.md) | What evidence is needed before granting or ending access? |
| [Access review procedure](access-review-procedure.md) | Which existing permissions should be retained, changed, or revoked? |
| [Synthetic review evidence](synthetic-review-evidence.md) | How are decisions, implementation, and verification distinguished? |
| [Access KPI dictionary](access-kpis.md) | How are completion, remediation, and exceptions measured? |

## Worked example

The synthetic campaign reviews six entitlements. Five have a recorded decision, three require removal, and two removals are verified. The third removal remains open. These numbers illustrate why a completed review decision is different from completed remediation.

## Skills demonstrated

Role-based access design, least privilege, separation of duties, evidence traceability, exception management, review operations, and metric definitions.

## Publication status

This case is a newly authored, technology-agnostic portfolio demonstration. It does not assert deployment in an employer environment, actual access reductions, or independent security certification. All resources, identities, tickets, evidence references, dates and outcomes in the example are fictional. Adapt proposed cadences and time limits to the target organization's risk decisions.
