# Maturity Assessment Scoring Methodology

**Methodology version:** 1.0  
**Compatible artifacts:** [Maturity Model 1.0](maturity-model.md) and [Assessment Questionnaire 1.0](assessment-questionnaire.md)  
**Standard baseline:** 8 domains, 4 controls per domain, 32 controls  
**Public examples:** synthetic

This specification defines how validated responses become domain and overall scores. It separates evidence validation, data quality, assessment completion and maturity so that missing information cannot create misleading results.

[Return to the case overview](README.md)

## 1. Unit of calculation

Calculate each assessment independently.

- One assessment header defines scope, population, dates, sampling and model versions.
- One response record represents one control within that assessment.
- The unique key is `assessment_id + control_id`.
- Expected control IDs are `D01-Q01` through `D08-Q04`: domains D01–D08, each containing Q01–Q04.
- Multiple interviewees or evidence references do not create additional scored rows.
- A follow-up assessment has a new assessment ID and retains a reference to its baseline.

Maintain an authoritative 32-control register from the questionnaire. Use it to detect missing and unexpected IDs. Counting 32 rows alone is insufficient: duplicated controls can conceal missing ones.

## 2. Assigning control scores

A reviewer assigns the highest fully supported integer level using the model:

| Score | Level | Basis for validation |
|---:|---|---|
| 0 | Nonexistent | Confirmed absence of an established control within the scope |
| 1 | Reactive | Evidence of informal, inconsistent or mainly incident-driven activity |
| 2 | Defined and Managed | Documented, owned and standardized execution across the scope, with managed exceptions |
| 3 | Optimized | Sustained level 2 capability plus measured effectiveness, review cycles and evaluated improvements |

Levels 1–3 represent progressively stronger capabilities. Zero denotes absence. Do not average interview answers or components of a question into a fractional control score.

Retain the response summary, evidence references, coverage limitations, rationale, reviewer role and review date. For a zero, the evidence may be a documented absence finding; it need not be an artifact for a control that does not exist.

Self-reported scores are optional supporting information. They never substitute for validated scores in any maturity calculation.

## 3. Status and null handling

| assessment_status | validated_score | Effect on standard scoring |
|---|---|---|
| Validated | Required integer 0–3 | Counts toward coverage and contributes to eligible aggregates |
| Not assessed | Null | Assessment remains incomplete |
| Unverified | Null | Assessment remains incomplete pending evidence resolution |
| Not applicable | Null | Requires approved scope justification and a separate assessment variant |

Use blank CSV cells or a true null in storage for absent scores. Do not encode missing values as zero, -1, "N/A", or a maturity label in the numeric column. Parse blanks as null before numeric conversion.

Reject contradictory records, such as Unverified with a validated score or Validated with a blank score. Correct them at the source with a traceable decision; do not silently discard them or coerce them into valid values.

## 4. Input validation before aggregation

For each assessment, check:

1. The header exists and identifies the compatible model and questionnaire versions.
2. Every response ID belongs to the expected control register.
3. Each expected ID appears no more than once.
4. Status values exactly match the four allowed statuses.
5. Validated scores are numeric integers from 0 to 3, including zero.
6. Other statuses have null validated scores.
7. Validated records contain evidence references, rationale, reviewer role and review date.
8. Dates are valid; applicability exclusions have documented justification and approval.
9. Optional self-reported and target scores are null or integers from 0 to 3.

Treat duplicate keys, unexpected IDs, invalid scores, contradictory statuses and missing required validation metadata as **Data error**. Withhold maturity aggregates and official coverage for that assessment until corrected; show the errors separately.

Missing expected rows are a completion issue, not evidence that a control is nonexistent. Expose them as **Missing response** in completeness diagnostics without adding a fifth stored assessment status or fabricating a response.

## 5. Completion and coverage

For an assessment that passes input validation, let:

- `N = 32`: expected controls.
- `V`: unique expected controls with Validated status and a valid score.
- `M`: expected controls with no response record.

```text
Assessment Coverage (%) = V / 32 × 100
Missing Response Count = 32 − Count of unique expected response records
Domain Coverage (%) = Validated controls in that domain / 4 × 100
```

Coverage measures how much of the questionnaire has been validated. It is not asset coverage, control effectiveness or compliance. Describe asset sampling separately.

The counts of Validated, Not assessed, Unverified, Not applicable and missing responses must sum to 32.

### Assessment result state

Apply this precedence:

| State | Condition | Final standard overall score |
|---|---|---|
| Data error | Input validation fails | Null |
| Variant required | Input is valid and at least one control is Not applicable | Null |
| Incomplete | Input is valid, no exclusions exist, and fewer than 32 controls are validated | Null |
| Complete | All 32 expected controls are applicable and validated | Calculated |

An assessment with approved exclusions can have all applicable responses completed while still being ineligible for the standard overall score.

## 6. Domain and overall scores

### Domain score

Calculate only when all four expected controls in the domain have valid, validated scores and the assessment passes input validation.

```text
Domain Score(d) = [Score(d,Q01) + Score(d,Q02)
                 + Score(d,Q03) + Score(d,Q04)] / 4
```

Otherwise return null for that domain. Do not average only the available answers.

A complete domain may be displayed while another domain is incomplete. Make the assessment state and domain coverage visible.

### Overall score

Calculate only for a Complete standard assessment.

```text
Overall Score = Sum of the eight unrounded Domain Scores / 8
              = Sum of the 32 validated control scores / 32
```

Each domain carries 12.5% of the overall weight, and each control carries 3.125%. Risk and criticality affect improvement priorities; they do not change these baseline weights.

Both aggregate scores range from 0 to 3. An assessment with 32 validated zeros is Complete, has 100% coverage and an overall score of 0.00.

### Precision and display

Keep full precision for calculation and comparison. Round only displayed scores to two decimal places using decimal half-up rounding. Display coverage with up to two decimal places.

Do not round domain scores before computing the overall score. Display null scores as "Incomplete", "Variant required" or "Data error", as appropriate, rather than as 0.00.

Fractional averages are indicators, not additional maturity levels. Do not round a 1.75 average to level 2 or present it as proof that all controls are Defined and Managed.

## 7. Synthetic worked assessment

All controls in this example are applicable and validated.

| Domain | Q01 | Q02 | Q03 | Q04 | Sum | Domain score |
|---|---:|---:|---:|---:|---:|---:|
| D01 | 1 | 2 | 2 | 3 | 8 | 2.00 |
| D02 | 1 | 1 | 2 | 2 | 6 | 1.50 |
| D03 | 2 | 2 | 2 | 2 | 8 | 2.00 |
| D04 | 0 | 1 | 1 | 2 | 4 | 1.00 |
| D05 | 2 | 2 | 3 | 3 | 10 | 2.50 |
| D06 | 1 | 1 | 1 | 1 | 4 | 1.00 |
| D07 | 2 | 2 | 2 | 3 | 9 | 2.25 |
| D08 | 1 | 2 | 2 | 2 | 7 | 1.75 |
| Total | | | | | 56 | |

```text
Overall Score = 56 / 32 = 1.75
Assessment Coverage = 32 / 32 × 100 = 100%
Assessment State = Complete
```

The zero in D04 remains a visible control gap despite the complete assessment and overall average.

If D04-Q01 is instead Unverified with a null score:

```text
D04 Score = null
Overall Score = null
Assessment Coverage = 31 / 32 × 100 = 96.875%
Displayed Coverage = 96.88%
Assessment State = Incomplete
```

The other seven complete domain scores remain available. Their mean must not be used as a replacement overall score.

## 8. Targets and changes over time

### Control target gap

Calculate only when a validated current score and an agreed target score exist:

```text
Control Gap = max(Target Score − Current Validated Score, 0)
```

A current score of 1 with a target of 2 has a gap of 1. A missing target produces a null gap, not zero. A current score above target produces zero gap while retaining both values.

For a domain target average, require all four control targets; average them with equal weights. Keep control gaps visible because overperformance on one control can conceal a shortfall on another.

### Baseline-to-follow-up change

Compare complete standard assessments with equivalent scope, question definitions, scoring rules and sampling expectations.

```text
Score Change = Follow-up Overall Score − Baseline Overall Score
```

A change from 1.75 to 2.00 is **+0.25 score points**. Do not label it a percentage-point improvement in compliance. If either score is null or scope is materially different, withhold the comparison and explain why.

Store reassessments separately. Preserve previous validated scores and the evidence supporting them rather than overwriting the baseline.

## 9. Scope exclusions and weighting variants

The standard method does not automatically remove Not applicable controls from denominators.

Before publishing a variant, document its identifier, scope justification, approved exclusions, retained questions, completeness rules, weights and denominators. Distinguish its results from version 1.0 standard scores.

If all controls in a domain are excluded, do not assign that domain a zero or a three. A variant must explicitly define how that domain and its weight are handled. A risk-weighted model likewise requires a separately documented method and cannot be compared directly with the equal-weight baseline.

## 10. Implementation guidance

Apply the same rules in spreadsheets, scripts and the future Power BI model:

- Validate records before calculating measures.
- Build completeness checks against the full expected control register, not just observed rows.
- Keep evidence records separate from scored responses to avoid duplicating scores during joins.
- Treat zero as a valid number; test for null explicitly.
- Add completeness conditions before using average functions, which may otherwise ignore blanks.
- Require a single assessment for an overall score card, or display assessments separately. Do not pool scores from different scopes.
- Preserve the full 32-control denominator for an assessment-wide coverage card even when the user filters to a domain.
- Label domain-filtered coverage as Domain Coverage with denominator 4.
- Ensure a filter on Validated status cannot make an incomplete assessment appear complete.
- Never replace a missing score with zero solely to fill a chart.
- Display model version, assessment scope, date, coverage and result state alongside score visuals.

An optional scale conversion, Overall Score / 3 × 100, is only a normalized score index. It must not be called compliance percentage, implementation coverage or probability of success. The primary display in this case remains the 0–3 scale.

## 11. Calculation acceptance cases

These are expected implementation checks, not claims that a Power BI template has already passed testing.

| Scenario | Expected result |
|---|---|
| Worked assessment in section 7 | Complete; overall 1.75; coverage 100% |
| All 32 controls Validated with score 0 | Complete; overall 0.00; coverage 100% |
| All 32 controls Validated with score 3 | Complete; overall 3.00; coverage 100% |
| One Unverified control with null score | Incomplete; affected domain and overall null; coverage 96.88% |
| One expected response row missing | Incomplete; missing count 1; coverage 96.88% if the other 31 are validated |
| One approved Not applicable control; 31 validated | Variant required; standard overall null; standard coverage 96.88% |
| Duplicate control key, even with identical answers | Data error; reject rather than silently deduplicate |
| Unexpected ID replacing an expected ID | Data error, even when row count equals 32 |
| Validated score is blank, 4 or 1.5 | Data error |
| Unverified record contains validated_score = 2 | Data error |
| Validated record lacks required evidence or reviewer metadata | Data error |
| Self-reported scores change; validated scores stay fixed | No change to maturity aggregates |
| Current score exists but target is blank | Null target gap |
| Several assessments selected for a single overall card | No pooled standard overall score |

## 12. Review and publication

Record reviewer decisions and retain the evidence period, scope and version with each published result. Resolve data errors and display critical gaps rather than relying on averages alone.

Public datasets and worked examples must be synthetic. Original responses, participant details, internal evidence and actual organizational scores remain excluded.

**Power BI template sanitization is still pending.** Before public upload, complete sanitization and check its calculations against the acceptance cases above.

[Case overview](README.md) | [Maturity model](maturity-model.md) | [Questionnaire](assessment-questionnaire.md)

Next planned artifact: `improvement-roadmap.md`.
