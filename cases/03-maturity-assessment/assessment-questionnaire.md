# Data Governance Assessment Questionnaire

**Questionnaire version:** 1.0  
**Compatible model:** [Maturity Model 1.0](maturity-model.md)  
**Structure:** 8 domains, 4 questions per domain, 32 scored controls

This questionnaire operationalizes the custom maturity model for this portfolio. It supports structured interviews, evidence review and gap analysis. It is not a certification or a legal compliance determination.

[Case overview](README.md) | [Maturity model and scoring criteria](maturity-model.md)

## 1. How to use this questionnaire

1. Agree on the assessment scope, asset population, evidence period, sampling approach and reviewers.
2. Ask the relevant owner roles to describe how each control operates and provide evidence references.
3. Record self-reported scores separately from reviewer-validated scores.
4. Review evidence against the maturity model and document the scoring rationale.
5. Record gaps, exceptions and follow-up actions before finalizing results.

The questions are prompts for assessing maturity, not a yes/no checklist. A positive answer or a policy document alone does not establish that a control operates consistently.

Question IDs are stable within version 1.0. Use the combined ID, such as `D01-Q01`, as the control identifier in response records and future datasets. Supporting interview prompts and evidence requests are not additional scored questions.

## 2. Response scale and assessment status

| Score | Level | Decision rule |
|---:|---|---|
| 0 | Nonexistent | The absence of an established control is validated within the scope. |
| 1 | Reactive | Relevant activity exists but is informal, inconsistent or primarily incident-driven. |
| 2 | Defined and Managed | The control is documented, owned, standardized and demonstrably operated across the scope; exceptions are tracked. |
| 3 | Optimized | Level 2 is sustained; effectiveness is measured across review cycles and improvements are implemented and evaluated. |

Progression from 1 to 2 to 3 requires the additional capabilities at each level. Zero denotes absence, not a prerequisite capability. Assign the highest fully supported level using the [full model](maturity-model.md).

| Assessment status | Validated score |
|---|---|
| Validated | Required integer from 0 to 3 |
| Not assessed | Blank |
| Unverified | Blank; retain any self-reported score separately |
| Not applicable | Blank; require documented scope justification and approval |

Missing evidence is not automatically a zero. Use **Unverified** when the available information does not support a reliable conclusion. Use **Not applicable** only for a justified scope exclusion, not because a control is absent or difficult to implement.

## 3. Assessment header

Complete these fields once per assessment. Public demonstrations must use fictional identifiers and role labels.

| Field | Required content |
|---|---|
| Assessment ID | Unique identifier for this assessment instance |
| Model and questionnaire versions | Version 1.0 for both artifacts |
| Assessment scope | Organization unit, project or domain and explicit boundaries |
| Asset population | Included assets, systems and processes; criticality criteria |
| Assessment date and evidence period | Review date and period covered by evidence |
| Sampling approach | Sample selection, sample size, coverage and limitations |
| Assessment lead and reviewers | Accountable roles and review responsibilities |
| Applicability decisions | Approved exclusions and their rationale, if any |
| Evidence rules | Freshness expectations, access arrangements and storage location |

## 4. Control questions

For every question, examine ownership, documentation, execution coverage, exception handling and evidence of improvement. Evidence examples are illustrative; equivalent records may demonstrate the same capability. Set thresholds and review frequencies for the scope before evaluating them.

### D01 — Governance Policy and Data Classification

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D01-Q01 | Are governance roles formally assigned and actively performing their responsibilities within the assessed scope? | Role assignments, responsibility matrix, decisions and completed owner actions. |
| D01-Q02 | Are data governance policies approved, accessible and consistently applied by the relevant teams? | Current policies, approval records, communication records and execution samples. |
| D01-Q03 | Are critical data assets classified according to an approved sensitivity scheme? | Critical-asset inventory, classification criteria, catalog samples and exception register. |
| D01-Q04 | Is classification reviewed periodically and when changes affect data content, purpose or risk? | Review schedule, completed reviews, change triggers and reclassification decisions. |

### D02 — Data Lineage and Metadata Repository

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D02-Q01 | Is a centralized metadata repository maintained for the assessed assets, including business definitions and technical descriptions? | Catalog or equivalent repository, glossary entries, maintenance procedures and update history. |
| D02-Q02 | Do critical-asset metadata records identify accountable owners, classification, access requirements and applicable obligations? | Mandatory metadata standard, sampled records, completeness checks and remediation records. |
| D02-Q03 | Is lineage maintained from data origin through transformations to consumption, including the purpose of use? | Lineage maps, transformation documentation, validation records and impact-analysis examples. |
| D02-Q04 | Are structural changes detected and reflected in the metadata repository through a managed process? | Schema-change records, detection results, update tickets and catalog revision history. |

### D03 — Data Quality

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D03-Q01 | Are quality rules defined and applied to critical data according to business requirements? | Approved rules, covered assets, execution results and recorded exceptions. |
| D03-Q02 | Are data quality metrics and service levels defined, owned and monitored? | Metric definitions, agreed thresholds, monitoring history and review decisions. |
| D03-Q03 | Are quality or integration failures detected, routed and escalated within agreed response times? | Alert rules, routing procedures, timestamped incidents and escalation records. |
| D03-Q04 | Are data quality issues remediated through a controlled workflow with accountable ownership and required approvals? | Issue register, root-cause analysis, remediation tickets, approvals and post-fix validation. |

### D04 — Master and Reference Data

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D04-Q01 | Are critical master and reference data entities identified and assigned accountable ownership? | Entity inventory, criticality criteria, owner assignments and review records. |
| D04-Q02 | Are consistent identifiers defined and used to identify master entities across relevant systems? | Identifier standards, source-to-target mappings, uniqueness checks and exception handling. |
| D04-Q03 | Are authoritative sources approved and used, with controlled exceptions for alternative sources? | Source register, approval decisions, consumption mappings and exception records. |
| D04-Q04 | Are matching, merging and survivorship rules defined and operated to resolve conflicts when consolidating master records? | Consolidation rules, match results, merge decisions, conflict reviews and validation records. |

### D05 — Data Security and Access

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D05-Q01 | Are security controls selected and operated according to data classification and assessed risk? | Classification-to-control mapping, implementation samples, control tests and approved exceptions. |
| D05-Q02 | Is access granted through defined roles and approval criteria rather than unmanaged individual permissions? | Role and access matrix, access requests, approvals and sampled permission assignments. |
| D05-Q03 | Are unclassified assets identified and prevented from being accessed until classification or an approved exception is in place? | Access-gating rules, classification checks, denied requests and exception approvals. |
| D05-Q04 | Are non-production environments protected from inappropriate exposure of real data through approved masking, anonymization or synthetic-data practices? | Non-production data standard, transformation or generation records, validation results and approved exceptions. |

### D06 — Data Lifecycle

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D06-Q01 | Are retention periods and disposal triggers defined, approved and applied to the relevant data categories? | Retention schedule, owner approvals, configured rules and execution samples. |
| D06-Q02 | Are lifecycle status, retention requirements and responsible roles maintained in asset metadata? | Lifecycle metadata standard, catalog samples, update history and completeness checks. |
| D06-Q03 | Is disposal coordinated across relevant copies and environments, with retention holds and exceptions accounted for? | Copy inventory, disposal workflow, hold checks, execution records and reconciliation results. |
| D06-Q04 | Does data disposal produce sufficient traceable evidence to verify authorization, execution and outcome? | Approval references, execution logs, completion checks and failure-resolution records. |

### D07 — Data Collection and Sharing

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D07-Q01 | Are the purpose, necessity and accountable owner established before data is collected? | Purpose register, collection approvals, necessity assessments and owner records. |
| D07-Q02 | Is the required authorization or legal-basis review recorded and maintained for collection and use where applicable? | Review workflow, approved records, change reviews and recorded conditions of use. |
| D07-Q03 | Is external sharing authorized and protected through appropriate transfer controls and traceability? | Sharing approvals, recipient requirements, transfer-control configuration and transfer logs. |
| D07-Q04 | Are withdrawal requests assessed and acted upon through a documented workflow that considers affected copies, applicable obligations and approved exceptions? | Request records, impact assessments, decisions, action logs and completion verification. |

### D08 — Data Audit and Compliance

| Control ID | Assessment question | Suggested evidence |
|---|---|---|
| D08-Q01 | Are governance controls periodically tested against agreed requirements, with findings assigned and followed up? | Test plan, sampled test results, findings register, action owners and closure evidence. |
| D08-Q02 | Are access rights periodically recertified by accountable owners, with decisions implemented and verified? | Review schedule, access snapshots, owner decisions, remediation tickets and verification records. |
| D08-Q03 | Are inactive accounts identified and reviewed against defined criteria, with justified retention or timely removal of access? | Inactivity criteria, account reports, review decisions, exceptions and revocation records. |
| D08-Q04 | Are audit and security-control indicators monitored and used to identify and address recurring weaknesses? | Indicator definitions, trend reports, review minutes, corrective actions and follow-up results. |

## 5. Supporting interview prompts

Apply these prompts as needed to each control; do not score them separately.

- Who owns the control and who performs it?
- Where is the current procedure or approved standard?
- Can the team show actual execution during the evidence period?
- Which assets or activities are not covered, and how are exceptions managed?
- What happens when the control fails or a deadline is missed?
- How is effectiveness measured, and what changed following a review?

If a question contains multiple related requirements, review each component. Do not average component answers into a fractional control score or allow one strong component to conceal an unsupported requirement. Record the limiting component in the rationale.

## 6. Response record template

Create one record per control per assessment: the pair `assessment_id` and `control_id` must be unique. Multiple evidence references belong to that record and must not create duplicate scored controls.

| Field | Entry guidance |
|---|---|
| assessment_id | Identifier from the assessment header |
| control_id | Exact ID from section 4 |
| respondent_role | Role providing the response |
| control_owner_role | Role accountable for the control |
| response_summary | How the control operates and where it does not |
| self_reported_score | Optional integer 0–3; never used as a validated result |
| assessment_status | Validated, Not assessed, Unverified or Not applicable |
| validated_score | Integer 0–3 only when status is Validated; otherwise blank |
| evidence_references | Traceable references to supporting records or absence findings |
| evidence_period | Period demonstrated by the evidence |
| coverage_and_limitations | Population, sample and limits of the conclusion |
| scoring_rationale | Why the selected level is supported and the next level is not |
| exceptions_or_exclusions | Relevant exceptions or approved applicability justification |
| reviewer_role | Role responsible for validation |
| review_date | Date in YYYY-MM-DD format |
| gap_and_follow_up | Missing capability, action and accountable role |
| target_score | Optional agreed integer 0–3, based on business needs |
| target_date | Optional date for the improvement action |

Preserve the assessment header with the response records so scope and model versions remain traceable.

### Synthetic response example

| Field | Fictional entry |
|---|---|
| assessment_id | SYN-MAT-001 |
| control_id | D01-Q03 |
| respondent_role | Data Steward |
| control_owner_role | Data Owner |
| response_summary | Classification is applied when requests arrive, but there is no standard procedure across the asset population. |
| self_reported_score | 2 |
| assessment_status | Validated |
| validated_score | 1 |
| evidence_references | SYN-EV-001: fictional classification register; SYN-EV-002: fictional request records |
| evidence_period | 2026-06-01 to 2026-08-31 |
| coverage_and_limitations | Fictional population of 20 critical assets; all 20 reviewed, with classification recorded for 12. |
| scoring_rationale | Activity exists, but execution is inconsistent and no approved procedure is in operation. Level 2 is not supported. |
| exceptions_or_exclusions | No approved scope exclusions; eight assets remain unclassified. |
| reviewer_role | Governance Assessment Lead |
| review_date | 2026-09-01 |
| gap_and_follow_up | Data Owner to approve a procedure, assign execution responsibilities and address missing classifications. |
| target_score | 2 |
| target_date | 2026-11-30 |

These evidence references are fictional labels, not links to real records. The example illustrates reviewer validation; it is not an actual organizational assessment.

## 7. Completion and handoff checks

- Confirm exactly 32 unique control records, with four under each domain.
- Require a validated integer score and supporting rationale for every Validated record.
- Keep other statuses unscored; never replace blanks with zero.
- Resolve conflicting evidence or retain an Unverified status.
- Report assessment coverage as validated controls divided by 32.
- Calculate a standard domain score only when its four controls are validated.
- Withhold the final standard overall score until all 32 controls are applicable and validated.
- If scope exclusions apply, document a separate variant and aggregation rules before comparing totals.
- Retain full calculation precision and round only the displayed result.
- Carry critical gaps into improvement planning even when the average score is high.

The planned `scoring-methodology.md` will provide the detailed calculation and validation specification.

## 8. Public portfolio safeguards

Publish only synthetic response records and evidence examples. Keep real participant details, internal evidence, system references and organizational scores out of this repository.

**Pending release task:** sanitize and review the Power BI template before public upload. Creating or completing this questionnaire does not complete that task.

[Return to the case overview](README.md)
