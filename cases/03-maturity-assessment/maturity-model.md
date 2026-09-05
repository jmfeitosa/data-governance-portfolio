# Data Governance Maturity Model

This model defines how to assess operational data governance capabilities across eight domains using a consistent 0–3 scale. It supports evidence-based gap analysis and improvement planning.

**Model version:** 1.0  
**Scope:** 8 domains, 4 control questions per domain, 32 control questions in total  
**Assessment unit:** a defined organization, business unit, data domain, or project  
**Status:** public portfolio methodology; examples are synthetic

This is a custom operational model for this portfolio. It is not a certification, an official implementation of a named maturity standard, or a legal compliance assessment.

[Return to the case overview](README.md)

## 1. Purpose and boundaries

The assessment should help stakeholders:

- Establish a baseline of current governance practices.
- Distinguish documented intentions from controls operating in practice.
- Identify gaps and the evidence supporting each finding.
- Agree on achievable target capabilities and accountable owners.
- Reassess progress using a comparable scope and model version.

Assess a clearly defined population of assets and processes. Do not generalize results from one project or a small sample to an entire organization without supporting evidence.

## 2. Assessment domains

The control areas below define the scope of the four questions in each domain. Evidence examples are illustrative; equivalent evidence may be used when it demonstrates the same capability.

| ID | Domain | Four control areas | Example evidence |
|---|---|---|---|
| D01 | Governance Policy and Data Classification | Assigned and active roles; approved policies; classification of critical assets; periodic classification review | Role assignments, approved policy, classification register, review records |
| D02 | Data Lineage and Metadata Repository | Centralized metadata; ownership and access metadata for critical assets; documented lineage; schema-change controls | Catalog records, metadata completeness checks, lineage maps, change tickets |
| D03 | Data Quality | Defined quality rules; monitored metrics and service levels; alert handling; formal remediation | Rule specifications, monitoring results, alert records, remediation approvals |
| D04 | Master and Reference Data | Identified critical entities; consistent identifiers; authoritative sources; matching, merging and survivorship rules | Entity register, identifier standards, source ownership records, consolidation rules |
| D05 | Data Security and Access | Controls aligned to classification; role-based access; handling of unclassified assets before access; protected non-production data | Control mappings, access matrix, classification checks, masking or synthetic-data records |
| D06 | Data Lifecycle | Defined retention; lifecycle metadata; coordinated disposal across copies; auditable disposal evidence | Retention schedule, catalog lifecycle fields, disposal workflow, execution logs |
| D07 | Data Collection and Sharing | Defined purpose and accountability; recorded authorization or legal-basis review where applicable; controlled external sharing; handling of withdrawal requests | Purpose register, authorization records, sharing approvals, request-handling records |
| D08 | Data Audit and Compliance | Periodic control testing; access recertification; inactive-account review; monitored control indicators | Test reports, access review decisions, account-review logs, indicator histories |

Control implementation depends on context. For example, the handling of withdrawal requests must account for applicable retention obligations and approved exceptions. Specific frequencies, thresholds and technologies must be defined for the assessment scope rather than assumed to be universal requirements.

## 3. Maturity levels

Assign an integer score to each control. Levels are cumulative: a higher score requires the capabilities of the preceding levels as well as the additional criteria described below.

| Score | Level | Required characteristics | Evidence expectation |
|---:|---|---|---|
| 0 | Nonexistent | No initiative or operating control is established for the assessed requirement | A validated finding documenting the absence of the control within the agreed scope |
| 1 | Reactive | Some activity exists, but it is informal, inconsistent, dependent on individuals, or mainly triggered by incidents | Examples of actual activity, such as isolated tickets, manual checks or informal instructions |
| 2 | Defined and Managed | The process is documented, assigned to an accountable owner, standardized and demonstrably operated across the agreed scope; exceptions are tracked | Current approved procedure or equivalent standard, ownership records, execution samples and exception records |
| 3 | Optimized | Level 2 is sustained; performance and effectiveness are measured and reviewed; improvements are implemented and their effects evaluated | Evidence across successive review cycles, trend analysis, improvement decisions and follow-up results |

### Level 0 — Nonexistent

The control has not been established. Record the resulting gap and the basis for the finding.

**Synthetic example:** an asset inventory review and owner validation confirm that critical assets have no assigned classification.

Do not use zero as a substitute for a missing answer or an unverified claim.

### Level 1 — Reactive

People perform relevant activities, but execution is not reliably standardized or managed across the assessed scope.

**Synthetic example:** a team classifies selected datasets when access requests arrive, using individual judgment without an agreed procedure.

A draft policy alone does not demonstrate an operating control. If there is no evidence of execution, assess whether the absence of the control is confirmed or whether the result remains unverified.

### Level 2 — Defined and Managed

The control is repeatable, documented and owned. Evidence demonstrates routine execution, and exceptions have an owner and follow-up action.

**Synthetic example:** the team applies an approved classification procedure to its critical assets, records ownership and classification in a catalog, and tracks exceptions through a defined review process.

A tool installation, policy approval or isolated successful execution does not independently establish this level.

### Level 3 — Optimized

The control is managed over time and improved using evidence of its effectiveness.

**Synthetic example:** the team reviews classification coverage and misclassification trends over successive cycles, improves its checks, and verifies that the changes reduce recurring errors.

Automation may support this level, but automation alone does not establish maturity.

## 4. Evidence and scoring decisions

Before scoring, agree on:

- The business scope, asset population and assessment period.
- The model version and applicable control questions.
- Evidence freshness expectations and sampling approach.
- Review responsibilities and how disagreements will be resolved.

For each control, retain a question identifier, respondent or owner role, evidence reference, assessment status, validated score when available, scoring rationale, reviewer and review date. Record limitations and exceptions explicitly.

Use evidence that is relevant to the control, current for the assessment period, traceable to its source and sufficiently representative of the scope. A self-reported answer is a starting point for validation.

Assign the highest level whose required characteristics are fully supported. Where evidence is contradictory, resolve the discrepancy or retain an unverified result. A strong example from one asset does not establish consistent execution across the full population.

### Assessment status is separate from maturity

| Status | Meaning | Numeric treatment |
|---|---|---|
| Validated | The reviewer has sufficient evidence to assign a score, including a confirmed absence of a control | Integer from 0 to 3 |
| Not assessed | The control has not yet been evaluated | No score |
| Unverified | A response exists, but evidence is insufficient or contradictory | No validated score; retain any self-reported score separately |
| Not applicable | The requirement is outside the agreed scope, with documented justification and approval | No score; do not substitute 0 or 3 |

The standard baseline requires all 32 controls to be applicable and validated. If applicability differs, document a separate assessment variant and its aggregation rules before reporting comparable totals. Do not silently change denominators.

## 5. Aggregation and interpretation

For a complete standard assessment:

```text
Domain Score = Sum of its four validated control scores / 4
Overall Score = Sum of the eight domain scores / 8
Assessment Coverage = Validated controls / 32 × 100
```

All domains have equal weight. Because each domain contains four questions, all 32 controls also have equal weight in the overall score.

Retain full precision during calculation and round only for display, preferably to two decimal places. If any required control lacks a validated score, show the assessment as incomplete and withhold the final overall score. Complete domains may still be reported individually, with coverage made explicit.

A fractional score is an aggregate indicator, not a new maturity level. An overall score of 2.25 does not mean every control has reached level 2, nor does it demonstrate that 75% of requirements are compliant.

Always show the domain profile and low-scoring critical controls alongside the overall score. A high average can conceal a material gap.

### Synthetic worked example

A domain has validated control scores of **1, 2, 2 and 3**:

```text
Domain Score = (1 + 2 + 2 + 3) / 4 = 2.00
```

The average is 2.00, but the first control remains reactive. Its gap should remain visible and be evaluated for remediation.

## 6. Targets and improvement priorities

Set target levels by control or domain based on business needs, risk, dependencies and available resources. Level 3 is not automatically the appropriate immediate target for every control.

For a scored control, a target gap may be expressed as:

```text
Gap = max(Target Score − Current Validated Score, 0)
```

Do not prioritize solely by the largest gap. Consider:

- Business impact and control criticality.
- Exposure associated with the missing capability.
- Dependencies on foundational controls.
- Implementation effort and available ownership.
- The evidence needed to demonstrate successful completion.

Each improvement action should have an owner role, target date, target capability and acceptance evidence. Closing an action does not automatically increase maturity; validate the resulting control before changing its score.

## 7. Reassessment and comparability

Reassess at an agreed cadence and after material changes to processes, systems or scope.

Keep baseline and follow-up records with their assessment date, scope, model version and evidence period. Use the same control definitions and scoring rules for trend comparisons. If these change, explain the impact or establish a new baseline.

Track both score movement and the underlying evidence. A change may reflect better evidence or a revised scope rather than an improvement in the operating control.

## 8. Portfolio publication checklist

- [ ] Use only synthetic responses, scores and evidence examples in public assessment datasets.
- [ ] Exclude participant details, original evidence and internal technical references.
- [ ] Validate all 32 standard controls before publishing a final aggregate score.
- [ ] Label incomplete assessments and disclose scope limitations.
- [ ] Sanitize and review the Power BI template before uploading it to the public repository.

**Power BI sanitization remains pending.** This document does not establish that the template is ready for publication.

## 9. Next artifacts

The planned `assessment-questionnaire.md` will translate the control areas into 32 questions. The planned `scoring-methodology.md` will detail calculation and validation rules, while `improvement-roadmap.md` will turn assessed gaps into sequenced actions.

[Return to the case overview](README.md)
