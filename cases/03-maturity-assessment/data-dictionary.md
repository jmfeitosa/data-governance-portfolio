# Synthetic Assessment Results — Data Dictionary

**Dictionary version:** 1.0  
**Source:** [synthetic-assessment-results.csv](data/synthetic-assessment-results.csv)  
**Compatible model and questionnaire:** 1.0

This document defines all 33 source columns and how to import the CSV into Power BI while preserving the assessment's scoring rules.

[Case overview](README.md) | [Scoring methodology](scoring-methodology.md) | [Improvement roadmap](improvement-roadmap.md)

## 1. Dataset contract

The grain is **one control response per assessment**. The composite key is `assessment_id + control_id`.

The current file contains 32 records for one fictional assessment, `SYN-MAT-BASE-001`, with four controls in each of eight domains. It reproduces the worked baseline in the scoring methodology, not the separate single-response questionnaire example.

The CSV uses UTF-8, comma delimiters, a header row and double-quoted fields when needed. Blank cells represent missing optional values. Dates use YYYY-MM-DD.

Assessment-level metadata is repeated on each row for standalone portability. Within an assessment, scope, scenario, versions, assessment date, population, sampling approach, evidence rules, assessment lead and applicability decisions must agree. Reconstruct a single assessment header from these consistent fields; do not silently choose between conflicting values.

## 2. Column dictionary

Types below are the intended Power Query types after import. CSV itself does not store typed columns.

| # | Column | Import type | Required | Meaning and rules |
|---:|---|---|---|---|
| 1 | `assessment_id` | Text | Yes | Unique assessment instance; current value SYN-MAT-BASE-001. |
| 2 | `scenario` | Text | Yes | Identifies the synthetic worked baseline from scoring-methodology.md section 7. |
| 3 | `is_synthetic` | True/False | Yes | CSV literal true; denotes fabricated demonstration content, not independently verified organizational evidence. |
| 4 | `model_version` | Text | Yes | Maturity model version; preserve 1.0 as text. |
| 5 | `questionnaire_version` | Text | Yes | Questionnaire version; preserve 1.0 as text. |
| 6 | `assessment_date` | Date | Yes | Assessment date in YYYY-MM-DD format. |
| 7 | `assessment_scope` | Text | Yes | Boundaries of the fictional assessed unit and processes. |
| 8 | `asset_population` | Text | Yes | Description of the fictional assets, systems and criticality assumptions; not a numeric asset-count field. |
| 9 | `sampling_approach` | Text | Yes | Simulated review approach and limitations; no real records were inspected. |
| 10 | `evidence_rules` | Text | Yes | Evidence-period and interpretation assumptions; fictional labels are not file links. |
| 11 | `assessment_lead_role` | Text | Yes | Role coordinating the assessment. |
| 12 | `applicability_decision` | Text | Yes | Scope applicability decision; all 32 controls apply in this baseline. |
| 13 | `domain_id` | Text | Yes | Domain key D01 through D08. |
| 14 | `domain_name` | Text | Yes | Domain label associated with domain_id. |
| 15 | `control_id` | Text | Yes | Questionnaire key: D01-Q01 through D08-Q04; four controls per domain. |
| 16 | `assessment_question` | Text | Yes | Exact question associated with the control ID. |
| 17 | `respondent_role` | Text | Yes | Role supplying the simulated response. |
| 18 | `control_owner_role` | Text | Yes | Role accountable for operating the control; may differ from the roadmap action owner. |
| 19 | `response_summary` | Text | Yes | Description of simulated operation and limitations. |
| 20 | `self_reported_score` | Whole number | Optional | Respondent score 0–3 when supplied; currently blank in all rows. Never used in validated aggregates. |
| 21 | `assessment_status` | Text | Yes | Validated, Not assessed, Unverified or Not applicable. Here Validated represents a simulated review. |
| 22 | `validated_score` | Whole number | Conditional | Integer 0–3 required for Validated; null for all other statuses. Zero is a valid finding of absence. |
| 23 | `evidence_references` | Text | For Validated | Fictional evidence labels and descriptions; these are not attached evidence files. |
| 24 | `evidence_period` | Text | Yes | Date-range description, currently 2026-06-01 to 2026-08-31. Do not convert the entire range to one Date. |
| 25 | `coverage_and_limitations` | Text | Yes | Limits of the simulated conclusion and its population coverage. |
| 26 | `scoring_rationale` | Text | For Validated | Basis for the assigned level; explanation of why a higher level is unsupported, where applicable. |
| 27 | `exceptions_or_exclusions` | Text | Yes | Control exceptions, gaps or statement that there are no scope exclusions. |
| 28 | `reviewer_role` | Text | For Validated | Role responsible for simulated validation. |
| 29 | `review_date` | Date | For Validated | Validation date in YYYY-MM-DD format. |
| 30 | `gap_and_follow_up` | Text | Yes | Planned improvement or recurring sustainment; not a numeric gap. |
| 31 | `target_score` | Whole number | Optional | Agreed target 0–3. In this scenario max(validated_score, 2). |
| 32 | `target_date` | Date | Optional | Specific target date if agreed; currently blank because the roadmap uses relative windows and recurring work. |
| 33 | `roadmap_action_id` | Text | Yes | Primary action mapping R01–R07 or R09; R08 is the cross-assessment reassessment action, not a primary control action. |

## 3. Validation and missing values

- Check the expected set of 32 questionnaire IDs, not only the row count.
- Reject duplicate assessment/control keys and unexpected IDs.
- Check that each control belongs to its stated domain and matches the questionnaire.
- Accept only the four documented assessment statuses.
- A Validated record requires an integer score from 0 to 3, evidence references, rationale, reviewer role and review date.
- Other statuses require a null validated score.
- Optional self-reported and target scores must be null or integers from 0 to 3.
- Keep blank optional dates as null; do not substitute today's date.
- Preserve version numbers and identifiers as text.
- Validate repeated assessment metadata before extracting a header.

Validate score ranges and integrality **before** conversion to Whole number so an invalid fractional score is not rounded into a valid one. Retain conversion errors for investigation; do not replace errors with zero or remove failing rows.

A missing control row is a completeness issue. A missing score is not evidence of a nonexistent control. Follow the distinction between Data error, Variant required, Incomplete and Complete in the [scoring methodology](scoring-methodology.md).

The synthetic flag is a label, not proof of sanitization. Review content as well as the flag.

## 4. Import into Power BI Desktop

1. Download the linked CSV to a stable local folder.
2. In Power BI Desktop, select **Get data → Text/CSV**, choose the file and open it.
3. Set the delimiter to **Comma** and file origin to **65001: Unicode (UTF-8)**.
4. Turn off automatic data-type detection where available, then select **Transform Data**. This helps preserve IDs and version strings.
5. Confirm that the header is recognized and the preview contains 33 columns.
6. Name the query `AssessmentResponses`.
7. Inspect or remove any automatically generated type-conversion step before assigning the types in section 2.

These connector options are described in [Microsoft's Text/CSV documentation](https://learn.microsoft.com/en-us/power-query/connectors/text-csv).

Continue preparation for this dataset:

8. Trim surrounding whitespace in identifier and categorical fields. Preserve meaningful narrative text.
9. Normalize empty optional values to null. Check all score values for integer 0–3 validity before assigning Whole number.
10. Convert `is_synthetic` from the literal true/false to True/False; keep both version columns as Text.
11. Convert the three single-date fields to Date and check that the ISO values were interpreted correctly. Keep `evidence_period` as Text.
12. Apply the validation rules in section 3. Investigate errors without dropping or duplicating response records.
13. Select **Close & Apply** after the checks pass. Keep score columns set to **Don't summarize** for raw-detail visuals; use explicit measures for aggregates.

This is an import procedure, not a claim that a Power BI report or template has been executed and tested.

## 5. Model structure

A single `AssessmentResponses` table is sufficient to inspect this baseline. For a report designed for further assessments, use:

| Table | Grain and key | Purpose |
|---|---|---|
| Assessment | One row per assessment_id | Scope, dates, versions and assessment metadata |
| Control | One row per control_id for the supported questionnaire version | Authoritative 32-control register, domain and question |
| AssessmentResponses | One row per assessment_id + control_id | Responses, status, scores, rationale and reviewer information |
| RoadmapAction | One row per action ID within a roadmap version | Action owner, priority, dependencies and delivery status, when loaded |

Use one-to-many relationships from dimensions to responses and single-direction filtering. Build the Control register from the full questionnaire, not just observed response rows, so missing controls remain detectable.

The CSV contains only a primary action mapping. It does not contain roadmap delivery status or actual completion dates. Do not infer that an action is complete from its control score.

If future questionnaire or roadmap versions reuse IDs with changed definitions, include version in the corresponding dimension key and relationships.

Evidence can later be stored separately with one-to-many references. Do not expand it into additional scored fact rows, which would distort averages.

## 6. Score and filter behavior

Implement these requirements before publishing score visuals:

| Output | Required behavior |
|---|---|
| Assessment coverage | Validated expected controls / 32, only after input validation passes |
| Domain coverage | Validated expected controls in the selected domain / 4 |
| Domain score | Mean of its four validated scores only when all four are valid and present |
| Overall score | Mean of all 32 validated scores only for one Complete standard assessment |
| Control target gap | max(target_score − validated_score, 0); null when the target or validated score is absent |
| Total target gap | Sum of eligible control gaps, accompanied by the count of controls with both scores |

An assessment-wide score or coverage card must retain the full selected assessment population when domain, status, owner or action filters are applied. Domain and detail visuals may respond to those filters, but must be labeled accordingly. Preserve the selected assessment identity when removing detail filters.

Require exactly one assessment for a single overall score. Do not combine responses from separate scopes. Do not let a filter on Validated status conceal incomplete or erroneous records.

A distinct count of 32 control IDs is not sufficient validation: duplicate rows, invalid scores and missing reviewer metadata must still block the result. Average functions alone are also insufficient because they may ignore nulls.

The dictionary intentionally specifies measure behavior rather than providing simplified DAX that bypasses these checks. Use the acceptance cases in the scoring methodology when implementing the report.

## 7. Baseline reconciliation

After import, this file should reproduce:

| Check | Expected value |
|---|---:|
| Rows | 32 |
| Columns | 33 |
| Unique assessment IDs | 1 |
| Unique assessment/control keys | 32 |
| Domains | 8 |
| Validated controls | 32 |
| Sum of validated scores | 56 |
| Overall score | 1.75 |
| Assessment coverage | 100% |
| Sum of target scores | 68 |
| Target average, before display rounding | 2.125 |
| Controls below target | 11 |
| Total positive control-score gap | 12 |

Expected domain scores for D01 through D08 are **2.00, 1.50, 2.00, 1.00, 2.50, 1.00, 2.25 and 1.75**.

All 32 self-reported scores and target dates are blank by design. A blank target date does not mean that an action is overdue. Retain the roadmap's relative scheduling assumptions.

Keep full precision in calculations and use the methodology's decimal half-up rule for display: the target average is shown as **2.13**. Scores are not percentages of compliance.

## 8. Suggested report page

Use cards for assessment state, coverage and overall score; a domain comparison chart; and a control table with validated score, target, owner and roadmap action. Include a table of controls below target and their follow-up descriptions.

Show the synthetic-data label, scope, model version and assessment date. Keep unsupported or incomplete scores visibly blank with an explanatory status.

## 9. Publication and template dependency

Only synthetic responses and fictional evidence descriptions belong in this public dataset. Review replacement files for personal information, organizational references and internal evidence even when is_synthetic is true.

**Power BI template sanitization remains pending.** Before public upload, review connections, query steps, parameters, source paths, metadata and report content, then validate calculations against the scoring acceptance cases.

[Return to the case overview](README.md)
