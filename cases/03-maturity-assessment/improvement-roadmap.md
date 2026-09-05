# Data Governance Improvement Roadmap

**Roadmap version:** 1.0  
**Compatible model and questionnaire:** 1.0  
**Planning horizon:** illustrative 90-day plan, followed by recurring review  
**Status:** synthetic planning example; no implementation or achieved improvement is claimed

This roadmap translates validated assessment findings into owned, sequenced actions. It uses the synthetic worked assessment in the [scoring methodology](scoring-methodology.md), with an overall baseline score of **1.75** and **100% assessment coverage**.

The baseline below is that worked example only. It is not the separate single-response example in the questionnaire or a real organizational assessment.

[Case overview](README.md) | [Maturity model](maturity-model.md) | [Questionnaire](assessment-questionnaire.md)

## 1. Planning principles

- Prioritize business exposure and dependencies as well as maturity gaps.
- Define one accountable role for every action and identify delivery contributors.
- Use validated scores only; an unverified response creates an evidence-gathering action rather than an invented maturity gap.
- Keep an immediate containment track for material exposures discovered during the assessment.
- Define acceptance evidence before work begins.
- Treat target dates as planning assumptions until capacity and dependencies are agreed.
- Increase a maturity score only after evidence-based reassessment.

The assessment's equal scoring weights remain unchanged. Delivery priority does not alter the maturity calculation.

## 2. Synthetic baseline and targets

The illustrative target is to bring every control below level 2 to **Defined and Managed**, while sustaining controls already at level 2 or 3. This is a scenario assumption, not a universal target for all organizations.

For each of the 32 controls:

```text
Illustrative Target = max(Current Validated Score, 2)
Control Gap = max(Illustrative Target − Current Validated Score, 0)
```

| Domain | Baseline | Target average | Controls below target | Planned emphasis |
|---|---:|---:|---:|---|
| D01 — Governance Policy and Data Classification | 2.00 | 2.25 | 1 | Activate assigned governance roles |
| D02 — Data Lineage and Metadata Repository | 1.50 | 2.00 | 2 | Standardize catalog maintenance and required metadata |
| D03 — Data Quality | 2.00 | 2.00 | 0 | Sustain quality controls and review exceptions |
| D04 — Master and Reference Data | 1.00 | 2.00 | 3 | Establish entity ownership, identifiers and authoritative sources |
| D05 — Data Security and Access | 2.50 | 2.50 | 0 | Sustain access controls and verify continued effectiveness |
| D06 — Data Lifecycle | 1.00 | 2.00 | 4 | Establish retention, lifecycle records and controlled disposal |
| D07 — Data Collection and Sharing | 2.25 | 2.25 | 0 | Sustain purpose, authorization and sharing controls |
| D08 — Data Audit and Compliance | 1.75 | 2.00 | 1 | Operate a repeatable control-testing cycle |
| Overall | 1.75 | 2.125 | 11 | Close 12 control-score points of positive gap |

The target sum is 68 across 32 controls: **68 / 32 = 2.125**, displayed as **2.13** using the scoring methodology's rounding rule. The planned overall change is **+0.375 score points**, displayed as **+0.38**.

These are target calculations, not predictions. A reassessment may find unchanged scores or regressions. Eleven controls are below target because D04-Q01 has a two-point gap and the other ten have one-point gaps.

## 3. Prioritization rules

Use the following planning categories, recording the rationale on each action:

| Priority | Selection criteria | Planning treatment |
|---|---|---|
| P0 — Contain | A confirmed material exposure requires immediate action | Start containment promptly, assign an owner and track residual exposure |
| P1 — Establish | A foundational capability is missing or blocks dependent controls | Schedule first and define a prerequisite completion decision |
| P2 — Implement | Operational work depends on agreed foundations | Start when prerequisites are accepted |
| P3 — Sustain | Capability meets target but requires continued operation and monitoring | Include in recurring reviews and reassessment |

The synthetic example assigns no P0 action: scores alone do not establish an urgent incident. If one is discovered, address it without waiting for the 90-day sequence.

Within the same priority, compare exposure, dependency impact, delivery effort and available capacity. Record a reasoned decision rather than presenting an arbitrary weighted ranking as objective evidence.

## 4. Delivery phases

Day 1 is the approved kickoff date. Convert relative windows to actual dates only after resource and scope agreement.

| Phase | Illustrative window | Focus | Exit evidence |
|---|---|---|---|
| 1 — Confirm and establish | Days 1–30 | Confirm baseline, owners, entity scope and retention decisions | Approved scope and action register; accepted R01–R03 deliverables |
| 2 — Implement and operate | Days 31–60 | Apply catalog, identifier, source and lifecycle controls | Accepted R04–R06 deliverables, with representative execution evidence |
| 3 — Verify and reassess | Days 61–90 | Test controls, verify outcomes and reassess maturity | Accepted R07–R08 deliverables or documented carry-forward decisions |
| 4 — Sustain and improve | After Day 90 | Monitor control operation and revisit targets | Recurring review records, tracked exceptions and subsequent assessments |

An accepted phase does not imply that every control has reached its target. If evidence needs a longer operating period, carry the action forward with a revised date and retain the current validated score.

## 5. Illustrative action register

All actions initially have status **Planned**. Accountable roles are placeholders for role assignment, not named individuals.

| ID | Action and mapped controls | Priority | Accountable role | Target window | Prerequisites |
|---|---|---|---|---|---|
| R01 | Activate governance responsibilities — D01-Q01 (1→2) | P1 | Governance Lead | Days 1–15 | Approved assessment scope |
| R02 | Establish master/reference entity inventory and ownership — D04-Q01 (0→2) | P1 | Data Owner | Days 10–30 | R01 accepted |
| R03 | Approve retention and disposal rules — D06-Q01 (1→2) | P1 | Data Owner | Days 10–30 | R01 accepted; relevant policy and obligation review |
| R04 | Standardize metadata operations — D02-Q01, D02-Q02 (each 1→2) | P2 | Data Steward | Days 31–50 | R01, R02 accepted |
| R05 | Implement identifier and authoritative-source rules — D04-Q02, D04-Q03 (each 1→2) | P2 | Data Architect | Days 31–60 | R02 accepted |
| R06 | Operate lifecycle metadata and disposal controls — D06-Q02, D06-Q03, D06-Q04 (each 1→2) | P2 | Data Custodian | Days 45–60 | R03, R04 accepted |
| R07 | Establish and execute control testing — D08-Q01 (1→2) | P2 | Assurance Lead | Days 61–80 | R04, R05, R06 accepted |
| R08 | Reassess all 32 controls and review remaining gaps | P2 | Assessment Lead | Days 81–90 | R07 accepted; sufficient operating evidence |
| R09 | Sustain the 21 controls already meeting target | P3 | Governance Lead | Days 1–90 and recurring | Agreed control owners and review cadence |

Windows may overlap across actions, but dependent work starts only after the required deliverables are accepted. If R04 is accepted late in its window, R06 must be rescheduled when insufficient execution time remains.

R09 covers every control not mapped to R01–R07. It includes all D03, D05 and D07 controls and the already-at-target controls in the other domains.

## 6. Acceptance criteria and evidence

### R01 — Active governance responsibilities

Assign accountable and operating roles, communicate their responsibilities and put the governance decision process into operation.

**Acceptance:** approved responsibility matrix, role acceptance records, completed governance decisions and tracked exceptions demonstrate that roles are active across the scope. A signed matrix alone is insufficient.

**Contributors:** Data Owners, Data Stewards and delivery leads.

### R02 — Master and reference entity ownership

Inventory critical entities, agree criticality criteria and assign ownership. Confirm the register against the assessed asset population.

**Acceptance:** approved entity register, named roles for each scoped entity, coverage reconciliation and evidence of owner decisions. Record any uncovered entities as exceptions with actions.

**Contributors:** Data Steward, Data Architect and business representatives.

### R03 — Retention and disposal rules

Define data categories, retention periods, disposal triggers, review responsibilities and exception handling. Obtain the appropriate review of applicable obligations.

**Acceptance:** approved retention schedule, mapped assets and evidence that retention rules are applied through a controlled process. Record holds and exceptions. This action establishes the rules; R06 implements coordinated disposal and its evidence.

**Contributors:** Data Custodian and relevant legal, privacy or records-management reviewers.

### R04 — Managed metadata operations

Define required metadata fields, catalog maintenance responsibilities, update procedures and completeness checks.

**Acceptance:** current repository procedures, populated records, representative updates and completeness reviews demonstrate operation across the scope. Track missing metadata and approved exceptions.

**Contributors:** Data Owner, Data Architect and platform administrators.

### R05 — Identifiers and authoritative sources

Define consistent entity identifiers, document source mappings and approve authoritative sources and exception rules.

**Acceptance:** approved identifier standards and source register, mapping and uniqueness checks, consumption samples and resolved or tracked exceptions. Capture evidence separately for D04-Q02 and D04-Q03.

**Contributors:** Data Owner, Data Steward and integration teams.

### R06 — Managed lifecycle operation

Populate lifecycle metadata and operate a disposal workflow that coordinates relevant copies, verifies holds and preserves traceable evidence.

**Acceptance:** lifecycle records, approved execution records, cross-copy reconciliation, completion checks and managed failures demonstrate each of D06-Q02–Q04. Validate the workflow in a controlled environment before any authorized operational disposal.

This portfolio roadmap itself does not authorize deletion of real data. If an operational disposal event is not due during the evidence period, record that limitation and let the assessor determine whether available evidence supports the claimed level.

**Contributors:** Data Steward, platform administrators and relevant policy reviewers.

### R07 — Repeatable control testing

Define test scope, sampling, review cadence, responsibilities and finding follow-up. Execute the agreed cycle.

**Acceptance:** approved test plan, completed tests across the scope, assigned findings and verified follow-up show an operating process. A plan without executed tests does not establish level 2.

**Contributors:** Control owners and technical reviewers.

### R08 — Follow-up assessment

Create a new assessment ID and link it to the baseline. Review all 32 controls, including those expected to stay at their current level.

**Acceptance:** evidence-reviewed responses, scoring rationales, valid records and a published result state under the scoring methodology. Publish an overall score only when the standard assessment is complete; otherwise publish completion diagnostics and eligible domain scores.

Where possible, separate implementation ownership from assessment review. Document any unavoidable role overlap and its review arrangement.

### R09 — Sustained operation

Continue established quality, access, collection, sharing and other at-target controls while foundational changes proceed.

**Acceptance:** recurring execution records, review decisions and exception follow-up. For existing level 3 controls, retain evidence of measured effectiveness and evaluated improvements across cycles.

Treat R09 as recurring work with per-cycle completion records; do not mark the ongoing obligation permanently complete.

## 7. Action tracking and closure

Use one action record per action ID. Maintain a separate action-to-control mapping where an action affects multiple controls so the assessment dataset retains one score per control.

Record:

- Action ID, baseline assessment ID and mapped control IDs.
- Validated baseline scores, agreed control targets and acceptance criteria.
- Accountable role, contributors and reviewer role.
- Priority rationale, dependencies, planned start and target dates.
- Status, blockers, evidence references and decision history.
- Completion date and follow-up assessment ID where available.

| Action status | Meaning |
|---|---|
| Planned | Scope, ownership and acceptance criteria are proposed |
| In progress | Delivery has started |
| Blocked | A dependency, decision or resource constraint prevents progress |
| Awaiting validation | Deliverables exist and acceptance review is pending |
| Completed | The designated reviewer has accepted the action's evidence |
| Deferred | Work is postponed through a recorded decision, with a review date |

These are delivery statuses, separate from assessment statuses such as Validated or Unverified.

Action completion does not automatically change maturity. Preserve the baseline, and assign a new score only through the follow-up assessment. If an action is accepted but the target level is unsupported, retain the assessed score and create a follow-up action.

## 8. Monitoring cadence and indicators

An illustrative cadence is weekly delivery review, monthly owner review and a formal reassessment at the end of the planning horizon. Adjust it to the scope and risk.

| Indicator | Calculation or reporting rule | Interpretation |
|---|---|---|
| One-time action completion | Completed actions / approved one-time actions × 100 | Delivery progress; excludes recurring R09 |
| Overdue actions | Actions past target date that are not Completed | Include Deferred actions until a revised date is approved |
| Blocked actions | Count and age of Blocked actions | Dependency and capacity constraints |
| Assessment coverage | Validated controls / 32 × 100, after input validation | Evidence validation progress |
| Controls at target | Validated controls meeting their agreed target / 32 × 100 for this fully targeted example | Report alongside coverage; unverified controls do not count as achieved |
| Observed score change | Follow-up overall score − baseline overall score, only when comparable and complete | Assessed maturity movement, not action completion |
| Recurring-control review | R09 cycle results and unresolved exceptions | Sustained operation and possible regression |

For the original eight one-time actions R01–R08, completion uses a denominator of 8. If the approved action register changes, version it and disclose the new denominator. Do not improve the completion rate by silently dropping deferred or overdue work.

Report critical control gaps separately even when delivery progress or average maturity looks strong.

## 9. Replanning decisions

Replan when dependencies slip, evidence is insufficient, scope changes, a control regresses or a new material exposure is confirmed.

Record the reason, impact, decision owner and revised dates. Preserve original dates and baseline scores for traceability. Revalidate targets when scope changes materially; do not compare incompatible assessments as if they measured the same population.

A missed target is a planning finding to investigate, not a reason to inflate a score.

## 10. Public release dependency

**Power BI template sanitization remains pending.**

Before uploading the template:

- Replace original responses and assessment evidence with synthetic content.
- Review source connections, parameters, queries, model metadata and report elements for internal references.
- Verify the report's calculations against the acceptance cases in the [scoring methodology](scoring-methodology.md).
- Review the resulting file and record the sanitization and validation outcome.

This is a portfolio release task, separate from the synthetic organization's R01–R09 improvement plan. It is not included in organizational action-completion metrics.

## 11. Next artifact

The planned `data/synthetic-assessment-results.csv` will provide public demonstration records. Keep assessment IDs and scope explicit so the worked baseline, questionnaire example and any future follow-up scenarios are not accidentally mixed.

[Return to the case overview](README.md)
