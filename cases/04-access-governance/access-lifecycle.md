# Access request and revocation lifecycle

[Back to the case](README.md)

## Minimum request record

Use a unique request ID and record: synthetic or controlled identity ID, manager/sponsor, role, resource, purpose, classification, requested start/end, approval decision, approver, approval time, exception reference if any, implementation task, implementer, implementation time, verification outcome and closure time.

A blank approval or missing expiry is incomplete, not approved. Preserve denied and cancelled requests in the audit trail.

## Grant workflow

| Stage | Action | Exit condition |
| --- | --- | --- |
| Submitted | Requester provides scope, purpose and duration | Required fields complete |
| Validated | Steward checks resource/classification; sponsor confirms assignment | Resource and need established |
| Assessed | Security checks privilege and conflicts; privacy review if applicable | Issues resolved or valid exception |
| Approved / Denied | Data Owner records a decision | Named independent decision with timestamp |
| Implemented | Custodian applies only the approved scope and expiry | Configuration evidence attached |
| Verified | Independent reviewer tests allowed and denied actions | Effective permissions match approval |
| Active | Monitor expiry and relevant identity events | Grant remains within purpose and duration |
| Revocation pending | Owner or lifecycle event triggers removal | Removal assigned and due time recorded |
| Revoked | Remove all paths and verify effective denial | Independent evidence confirms removal |
| Closed | Preserve the request and evidence under retention rules | No unresolved implementation task |

Never jump from Approved to Closed. If verification fails, keep the request open and remove or correct the excess permission.

## Joiner, mover and leaver events

- **Joiner:** no inherited default access beyond an approved baseline. Validate the business role before granting resource roles.
- **Mover:** reevaluate old and new entitlements together. Remove obsolete scope; document any temporary overlap with expiry.
- **Leaver:** disable access according to the applicable termination process, remove sessions/tokens and delegated paths where supported, then verify. Record actual completion rather than only the ticket status.

An identity status change and a resource permission change may be separate operations. Account disablement alone does not prove that shared credentials, delegated access or previously exported data have been addressed.

## Emergency access

Require a named incident/task, independent emergency approver, narrowly scoped elevation, an expiry and activity logging. In this demonstration, elevation lasts at most four hours unless separately extended. After expiry, verify removal and perform a retrospective review. The four-hour value is an illustrative design choice.

## Revocation evidence

Record all known direct and inherited paths, removal action, completion time, effective-access test and verifier. If group propagation or platform latency delays denial, mark the task awaiting verification and escalate according to risk. Do not count it as verified removal.

## Synthetic trace

SYN-REQ-003 approved temporary analytics access for SYN-U03. Its end date elapsed. The review campaign requests removal, the custodian records implementation, and the verifier confirms denial under SYN-EV-003. Only that last event supports a completed revocation.
