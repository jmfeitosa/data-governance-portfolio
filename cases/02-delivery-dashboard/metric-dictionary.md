# Delivery Dashboard Metric Dictionary

[← Back to the case overview](README.md) · [Synthetic dataset](data/synthetic-work-items.csv)

## Purpose

This dictionary defines the business rules and example DAX measures for the public Data Governance Delivery Dashboard.

Its purpose is to ensure that executive and operational visuals use consistent work-item populations, status mappings, denominators, ageing logic, and risk definitions.

## Model assumptions

The examples assume that the synthetic CSV is imported into Power BI and the table is renamed:

```text
FactWorkItems
```

Expected fields include:

- `WorkItemId`
- `WorkItemType`
- `NormalizedStatus`
- `Workstream`
- `AssignedTo`
- `CreatedDate`
- `ActivatedDate`
- `ChangedDate`
- `ClosedDate`
- `DueDate`
- `StoryPoints`
- `IsBlocked`

Date fields should use the Power BI **Date** data type, identifiers should use **Whole number**, and `IsBlocked` should use **True/False**.

## Governed metric scopes

### Portfolio scope

Includes every row in `FactWorkItems`, including Epics and Features. Use this scope only for portfolio-structure views.

### Delivery-item scope

Includes:

```text
User Story
Task
Bug
Enabler
```

Epics and Features are excluded from delivery-item KPIs to prevent parent and child work from being counted as equivalent units of execution.

### Open-item scope

Includes delivery items whose normalized status is not `Closed`.

### Status mapping

| Normalized status | Meaning |
| --- | --- |
| New | Planned work that has not started. |
| Active | Work currently in execution. |
| In Validation | Work awaiting review, acceptance, or verification. |
| On Hold | Work formally paused. |
| Closed | Completed work. |
| Other | Unmapped state requiring review. |

## Base measures

These measures establish the shared scope used by the remaining KPIs.

### M-001 — Total portfolio items

**Definition:** All rows represented in the semantic model.

```DAX
Total Portfolio Items =
DISTINCTCOUNT ( 'FactWorkItems'[WorkItemId] )
```

**Use:** Portfolio structure, inventory, and reconciliation.

**Do not use as:** Denominator for delivery completion when Epics and Features are also represented by their child items.

---

### M-002 — Total delivery items

**Definition:** Distinct executable work items within the approved delivery scope.

```DAX
Total Delivery Items =
CALCULATE (
    DISTINCTCOUNT ( 'FactWorkItems'[WorkItemId] ),
    KEEPFILTERS (
        'FactWorkItems'[WorkItemType]
            IN { "User Story", "Task", "Bug", "Enabler" }
    )
)
```

**Use:** Primary denominator for delivery KPIs.

**Validation:** Must equal the sum of delivery items across mutually exclusive normalized statuses.

---

### M-003 — Total open delivery items

**Definition:** Delivery items whose normalized status is not Closed.

```DAX
Total Open Delivery Items =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] <> "Closed" )
)
```

**Use:** Backlog, workload, risk, and operational analysis.

## Delivery status metrics

### M-010 — Completed items

**Definition:** Delivery items with normalized status Closed.

```DAX
Completed Items =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] = "Closed" )
)
```

---

### M-011 — Completion rate

**Definition:** Share of delivery items completed within the current filter context.

```DAX
Completion Rate =
DIVIDE ( [Completed Items], [Total Delivery Items], 0 )
```

**Format:** Percentage.

**Interpretation:** Shows item-count completion, not effort-weighted completion.

**Validation:** Must remain between 0% and 100%.

---

### M-012 — New items

```DAX
New Items =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] = "New" )
)
```

---

### M-013 — Active items

```DAX
Active Items =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] = "Active" )
)
```

---

### M-014 — Items in validation

```DAX
Items In Validation =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] = "In Validation" )
)
```

---

### M-015 — On-hold items

```DAX
On Hold Items =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] = "On Hold" )
)
```

---

### M-016 — Other-status items

**Definition:** Delivery items that failed to map to an approved normalized status.

```DAX
Other Status Items =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] = "Other" )
)
```

**Interpretation:** A data-quality indicator. It must not be silently grouped into New, Active, or Closed.

## Risk and ageing metrics

The dashboard distinguishes four concepts:

| Concept | Rule |
| --- | --- |
| Blocked | Explicitly marked as blocked or placed On Hold. |
| Overdue | Open item with a Due Date earlier than today. |
| Stale | Active or In Validation item without a recent change for an approved number of days. |
| At risk | Open item that is blocked, overdue, or stale. |

The example stale threshold is 14 days and should be stored in a parameter rather than repeated in every measure.

### Recommended parameter

Create a numeric What-if parameter or a one-row configuration table:

```text
StaleThresholdDays = 14
```

### M-020 — Blocked items

```DAX
Blocked Items =
CALCULATE (
    [Total Delivery Items],
    FILTER (
        'FactWorkItems',
        'FactWorkItems'[NormalizedStatus] <> "Closed"
            && (
                'FactWorkItems'[IsBlocked] = TRUE ()
                || 'FactWorkItems'[NormalizedStatus] = "On Hold"
            )
    )
)
```

---

### M-021 — Overdue open items

```DAX
Overdue Open Items =
CALCULATE (
    [Total Delivery Items],
    FILTER (
        'FactWorkItems',
        'FactWorkItems'[NormalizedStatus] <> "Closed"
            && NOT ISBLANK ( 'FactWorkItems'[DueDate] )
            && 'FactWorkItems'[DueDate] < TODAY ()
    )
)
```

---

### M-022 — Stale active items

```DAX
Stale Active Items =
VAR StaleDays = 14
RETURN
    CALCULATE (
        [Total Delivery Items],
        FILTER (
            'FactWorkItems',
            'FactWorkItems'[NormalizedStatus] IN { "Active", "In Validation" }
                && NOT ISBLANK ( 'FactWorkItems'[ChangedDate] )
                && DATEDIFF (
                    'FactWorkItems'[ChangedDate],
                    TODAY (),
                    DAY
                ) > StaleDays
        )
    )
```

**Important:** Staleness measures lack of recent change. It is different from total time since activation.

---

### M-023 — At-risk items

**Definition:** Distinct open delivery items meeting at least one approved risk condition.

```DAX
At Risk Items =
VAR StaleDays = 14
RETURN
    CALCULATE (
        [Total Delivery Items],
        FILTER (
            'FactWorkItems',
            VAR IsOpen =
                'FactWorkItems'[NormalizedStatus] <> "Closed"
            VAR IsBlocked =
                'FactWorkItems'[IsBlocked] = TRUE ()
                    || 'FactWorkItems'[NormalizedStatus] = "On Hold"
            VAR IsOverdue =
                NOT ISBLANK ( 'FactWorkItems'[DueDate] )
                    && 'FactWorkItems'[DueDate] < TODAY ()
            VAR IsStale =
                'FactWorkItems'[NormalizedStatus]
                    IN { "Active", "In Validation" }
                    && NOT ISBLANK ( 'FactWorkItems'[ChangedDate] )
                    && DATEDIFF (
                        'FactWorkItems'[ChangedDate],
                        TODAY (),
                        DAY
                    ) > StaleDays
            RETURN
                IsOpen && ( IsBlocked || IsOverdue || IsStale )
        )
    )
```

This measure uses one row-level OR condition, preventing an item that is simultaneously blocked, overdue, and stale from being counted three times.

---

### M-024 — At-risk rate

```DAX
At Risk Rate =
DIVIDE ( [At Risk Items], [Total Open Delivery Items], 0 )
```

**Format:** Percentage.

**Interpretation:** Share of open delivery items that currently meet at least one risk rule.

---

### M-025 — Average open-item age

**Definition:** Average number of days since creation for open delivery items.

```DAX
Average Open Item Age Days =
AVERAGEX (
    FILTER (
        'FactWorkItems',
        'FactWorkItems'[WorkItemType]
            IN { "User Story", "Task", "Bug", "Enabler" }
            && 'FactWorkItems'[NormalizedStatus] <> "Closed"
            && NOT ISBLANK ( 'FactWorkItems'[CreatedDate] )
    ),
    DATEDIFF (
        'FactWorkItems'[CreatedDate],
        TODAY (),
        DAY
    )
)
```

**Format:** Whole number or one decimal place.

---

### M-026 — Average cycle time

**Definition:** Average elapsed days between activation and closure for completed delivery items.

```DAX
Average Cycle Time Days =
AVERAGEX (
    FILTER (
        'FactWorkItems',
        'FactWorkItems'[WorkItemType]
            IN { "User Story", "Task", "Bug", "Enabler" }
            && 'FactWorkItems'[NormalizedStatus] = "Closed"
            && NOT ISBLANK ( 'FactWorkItems'[ActivatedDate] )
            && NOT ISBLANK ( 'FactWorkItems'[ClosedDate] )
    ),
    DATEDIFF (
        'FactWorkItems'[ActivatedDate],
        'FactWorkItems'[ClosedDate],
        DAY
    )
)
```

## Ownership and workload metrics

### M-030 — Unassigned open items

```DAX
Unassigned Open Items =
CALCULATE (
    [Total Delivery Items],
    FILTER (
        'FactWorkItems',
        'FactWorkItems'[NormalizedStatus] <> "Closed"
            && (
                ISBLANK ( 'FactWorkItems'[AssignedTo] )
                || TRIM ( 'FactWorkItems'[AssignedTo] ) = ""
            )
    )
)
```

**Interpretation:** Indicates work without a visible operational owner.

---

### M-031 — Active workload

**Definition:** Active and In Validation delivery items in the current assignee or workstream context.

```DAX
Active Workload =
CALCULATE (
    [Total Delivery Items],
    KEEPFILTERS (
        'FactWorkItems'[NormalizedStatus]
            IN { "Active", "In Validation" }
    )
)
```

Use this measure in a visual grouped by assignee. Do not save a fixed list of names as the visual filter.

---

### M-032 — Dynamic assignee rank

```DAX
Assignee Workload Rank =
RANKX (
    ALLSELECTED ( 'FactWorkItems'[AssignedTo] ),
    [Active Workload],
    ,
    DESC,
    DENSE
)
```

Use a visual-level filter of rank less than or equal to 5 to create a dynamic Top 5.

## Effort metrics

Story points must not be mixed with raw item counts without clear labeling.

### M-040 — Total story points

```DAX
Total Story Points =
CALCULATE (
    SUM ( 'FactWorkItems'[StoryPoints] ),
    KEEPFILTERS (
        'FactWorkItems'[WorkItemType]
            IN { "User Story", "Enabler" }
    )
)
```

---

### M-041 — Completed story points

```DAX
Completed Story Points =
CALCULATE (
    [Total Story Points],
    KEEPFILTERS ( 'FactWorkItems'[NormalizedStatus] = "Closed" )
)
```

---

### M-042 — Story-point completion rate

```DAX
Story Point Completion Rate =
DIVIDE (
    [Completed Story Points],
    [Total Story Points],
    0
)
```

**Interpretation:** Effort-weighted completion for items that use story points. It should be displayed separately from item-count completion.

## Data-quality and reconciliation metrics

### M-050 — Missing required-field items

**Definition:** Delivery items missing an identifier, title, type, status, workstream, or applicable ownership field.

```DAX
Items Missing Required Fields =
COUNTROWS (
    FILTER (
        'FactWorkItems',
        ISBLANK ( 'FactWorkItems'[WorkItemId] )
            || TRIM ( 'FactWorkItems'[Title] ) = ""
            || TRIM ( 'FactWorkItems'[WorkItemType] ) = ""
            || TRIM ( 'FactWorkItems'[NormalizedStatus] ) = ""
            || TRIM ( 'FactWorkItems'[Workstream] ) = ""
    )
)
```

---

### M-051 — Status reconciliation check

**Definition:** Difference between total delivery items and the sum of the mutually exclusive approved status categories.

```DAX
Status Reconciliation Difference =
[Total Delivery Items]
    - (
        [New Items]
        + [Active Items]
        + [Items In Validation]
        + [On Hold Items]
        + [Completed Items]
        + [Other Status Items]
    )
```

**Expected result:** 0.

Any non-zero result indicates overlapping measures, an excluded state, or inconsistent filters.

---

### M-052 — Percentage-bound check

```DAX
Completion Rate Is Valid =
IF (
    [Completion Rate] >= 0
        && [Completion Rate] <= 1,
    TRUE (),
    FALSE ()
)
```

## Recommended visual mapping

| Dashboard element | Measure |
| --- | --- |
| Total scope card | Total Delivery Items |
| Completion card | Completion Rate |
| Active card | Active Items |
| Validation card | Items In Validation |
| On-hold card | On Hold Items |
| Risk card | At Risk Items |
| Status distribution | New, Active, In Validation, On Hold, Closed, Other |
| Workstream progress | Completion Rate by Workstream |
| Workload chart | Active Workload by AssignedTo |
| Dynamic Top 5 | Active Workload with Assignee Workload Rank |
| Risks table | Work items filtered by the same At Risk logic |
| Data-quality warning | Other Status Items and Items Missing Required Fields |

## Required dashboard tooltips

Every executive KPI should expose:

- metric definition;
- included work-item types;
- current filter context;
- numerator and denominator;
- last refresh timestamp;
- applicable threshold;
- comparison period where available.

## Metric validation checklist

Before publishing the dashboard:

- [ ] Work-item IDs are unique at the fact-table grain.
- [ ] Work-item types match the approved delivery scope.
- [ ] Every source state maps to one normalized status.
- [ ] Status Reconciliation Difference equals zero.
- [ ] Completion Rate remains between 0% and 100%.
- [ ] Executive and operational visuals use the same base scope.
- [ ] At-risk detail rows reconcile to the At Risk Items card.
- [ ] Blocked, overdue, and stale concepts are labeled separately.
- [ ] On Hold treatment matches the approved risk rule.
- [ ] Unassigned items remain visible.
- [ ] Dynamic rankings contain no saved personal-name filters.
- [ ] Default page filters are neutral or visibly disclosed.
- [ ] Date columns use the correct data type.
- [ ] Blank and unknown values are handled explicitly.
- [ ] Measures reconcile at portfolio and workstream levels.
- [ ] Refresh timestamp and source status are visible.

## Change control

Each metric change should record:

| Field | Required information |
| --- | --- |
| Metric ID | Stable identifier from this dictionary. |
| Previous definition | Rule used before the change. |
| New definition | Complete updated rule. |
| Reason | Business, technical, or control justification. |
| Impact | Affected visuals, trends, targets, and consumers. |
| Approver | Accountable business owner. |
| Test evidence | Reconciliation and regression results. |
| Effective date | Date from which the new rule applies. |

Historical comparisons should disclose definition changes that materially affect results.

## Disclaimer

This metric dictionary is an anonymized portfolio artifact. DAX examples are designed for the published synthetic model and may require adaptation to a different Power BI model, workflow configuration, calendar, refresh design, or risk policy.
