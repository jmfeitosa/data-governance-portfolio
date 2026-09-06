# Access review procedure

[Back to the case](README.md)

## Campaign scope

Define campaign ID, reference date, resource population, eligible entitlements, reviewers, deadlines and exclusion reasons before collecting decisions. In this example, the review unit is one identity–role–resource entitlement, not one person or one ticket.

Use an entitlement snapshot that includes direct grants, group-derived grants, privilege level, expiry and last relevant use where available. Missing activity evidence means unknown usage; it does not establish inactivity.

## Demonstration cadence

Review standard grants every quarter, privileged grants monthly, and emergency grants after each use. Also review on role changes, termination, classification changes and incidents. These are proposed portfolio settings, not universal requirements.

## Reviewer decisions

| Decision | Meaning | Required evidence |
| --- | --- | --- |
| Retain | Purpose and scope remain appropriate | Owner rationale and next review/expiry |
| Modify | Scope is excessive or role has changed | Approved replacement scope and removal task |
| Revoke | Access is no longer justified | Reason and removal task |
| Pending | Evidence or decision is missing | Named follow-up owner and due date |

Retain must not be the default for unanswered reviews. Escalate pending decisions; suspend or restrict access only according to the approved risk policy. An automated reminder is not a decision.

## Run and close

1. Freeze the eligible population and record exclusions.
2. Assign an accountable reviewer independent of the reviewed identity.
3. Validate purpose, scope, expiry, conflicts and available usage evidence.
4. Record a decision per entitlement.
5. Create remediation tasks for Modify and Revoke.
6. Verify changed effective access independently.
7. Reconcile the original snapshot with implemented changes.
8. Publish decision completion and remediation completion separately.

A campaign can finish collecting decisions while remediation remains open. Do not label it fully closed until all required actions are verified or valid exceptions are explicitly approved and disclosed.

## Evidence quality

Store campaign, entitlement, decision, approver, timestamps and verification references together. Protect evidence because it may reveal identity and permission information. For public demonstrations, use synthetic identifiers and descriptions only.

## Worked campaign

See [synthetic review evidence](synthetic-review-evidence.md). SYN-REV-001 has six eligible entitlements, five decisions and three removal obligations. Two removals are verified and one is overdue at the example cutoff. One entitlement still lacks a decision.
