# Delivery dashboard — reviewed Power BI template

[Back to case](../README.md) · [Download PBIT](DataGovernance_Delivery.pbit?raw=true)

## Open the demonstration

Download the template, open it in Power BI Desktop and refresh. The two source queries contain an embedded copy of the public synthetic CSV. No corporate Azure DevOps connection or original Excel file is required. The packaged custom visual remains subject to Desktop visual policies.

The author returned this export as reviewed and without errors. A follow-up static inspection found no known original personal, project or corporate identifiers, no external source query calls, and no remote dataset/report links in the checked text. Source query and measure definitions match the sanitized candidate. The reviewed bytes are published unchanged.

## Reconciliation reference

The following figures are calculated independently from the synthetic CSV. Successful Desktop opening is not a substitute for testing every visual and filter combination against these targets.

| Scope / measure | Expected unfiltered result |
| --- | ---: |
| All portfolio work items | 60 |
| Executable delivery items | 53 |
| Completed delivery items | 17 |
| Active delivery items | 16 |
| New delivery items | 10 |
| In Validation delivery items | 5 |
| On Hold delivery items | 5 |
| Delivery completion | 17 / 53 = 32.1% |
| Open delivery items | 36 |
| At-risk delivery items at the fixed snapshot | 36 |

**Snapshot Date: 2025-07-31. Stale Threshold Days: 14.** These are model measures. The fixed date deliberately replaces the metric dictionary's TODAY() examples so the demonstration is reproducible. “At risk” means an open delivery item is blocked, On Hold, overdue, or stale; overlapping conditions count the item once. Every open item meets at least one condition at this cutoff, which is a property of this fictional snapshot.

## Changes in the public version

- Replaced corporate OData queries with 60 synthetic rows in each legacy table, joined by WorkItemId.
- Removed corporate branding, fixed person selections, saved filters and remote artifact references.
- Replaced original project names with five synthetic workstreams.
- Standardized executable KPI scope to User Story, Task, Bug and Enabler.
- Corrected completion denominators, workload scope, risk logic and elapsed open-item age.
- Preserved blank closure dates in the closed-week calculation.
- Added DueDate and IsBlocked fields to support the documented risk rule.

## Boundaries and remaining work

The file retains ADO_WorkItems and DG_WorkItems, their legacy relationship structure and some Portuguese internal names. It is not the proposed FactWorkItems star schema. The source is an embedded snapshot, not a live CSV import.

The four SVG assets illustrate design requirements and are not exact screenshots of this release. The dedicated risks page is still unimplemented. [Actual Desktop screenshots](../README.md#dashboard-screenshots) are now published. Complete English legends/tooltips, dynamic Top 5 ranking and layout polish remain follow-up work. The operational card labeled DELAYED ITEMS displays the broader at-risk measure; rename it AT RISK ITEMS. Executive In Progress includes Active plus In Validation, so these cards overlap. Review visual titles and scope when interpreting any legacy chart.

The description inside the tested PBIT retains candidate/validation wording from the earlier export. It has been left unchanged to preserve the Desktop-reviewed bytes.

No Power BI Service deployment, scheduled refresh, production security audit or independent metric certification is claimed. Public custom visual code and generic icons are retained; the sanitization review is not a security audit of those packages.
