# Delivery Dashboard Release Checklist

[← Back to the case overview](README.md) · [Synthetic dataset](data/synthetic-work-items.csv) · [Metric dictionary](metric-dictionary.md) · [Semantic model](semantic-model.md) · [Data preparation](data-preparation.md)

## Purpose

This checklist supports controlled validation and release of the Data Governance Delivery Dashboard.

It separates:

1. validation of the Power BI solution;
2. deployment and operational readiness;
3. additional safeguards required before public portfolio publication.

A release should not proceed when a blocking check fails or required evidence is unavailable.

## Release record

Complete this section for each release.

| Field | Value |
| --- | --- |
| Release version | |
| Release type | Development / Test / Production / Public portfolio |
| Power BI file | |
| Target workspace or repository | |
| Change summary | |
| Release owner | |
| Business approver | |
| Technical reviewer | |
| Validation date | |
| Planned release date | |
| Result | Approved / Conditionally approved / Rejected |
| Evidence location | |
| Rollback version | |

## Result legend

| Result | Meaning |
| --- | --- |
| **Pass** | Requirement was tested and evidence is available. |
| **Fail** | Requirement was tested and did not meet the approved expectation. |
| **N/A** | Requirement does not apply and the reason is documented. |
| **Not tested** | No valid evidence is available. Treat as a release risk. |

## Blocking release gates

Do not release when any applicable condition is true:

- [ ] A private endpoint, credential, tenant identifier, or token is embedded in a public artifact.
- [ ] Real personal, client, employee, or confidential delivery data is present in the portfolio version.
- [ ] Required source credentials or refresh configuration fail in the target environment.
- [ ] Critical DAX reconciliation checks do not equal the expected result.
- [ ] Executive cards do not reconcile with their detail views.
- [ ] A material classification, access, or privacy requirement is unresolved.
- [ ] Report pages contain hidden filters that materially change the intended default view.
- [ ] A critical visual, navigation element, or refresh process is broken.
- [ ] The rollback version or recovery procedure is unavailable.
- [ ] A blocking exception lacks an accountable owner, approval, compensating control, and expiry date.

## 1. Scope and change control

- [ ] Release scope and purpose are documented.
- [ ] Changed queries, tables, relationships, measures, visuals, filters, parameters, and pages are listed.
- [ ] Affected business rules are identified.
- [ ] Metric-definition changes are approved by the accountable owner.
- [ ] Historical-comparison impact is documented.
- [ ] Source-schema changes are assessed.
- [ ] Dependencies and downstream consumers are identified.
- [ ] Release version is assigned.
- [ ] Previous stable version is retained.
- [ ] Rollback criteria and steps are documented.
- [ ] Open defects and accepted limitations are recorded.

### Evidence

- change record;
- updated metric dictionary;
- test cases and results;
- approval record;
- version history;
- rollback reference.

## 2. Source and privacy validation

### Public portfolio release

- [ ] Only the approved synthetic dataset is used.
- [ ] No real work-item title remains.
- [ ] No real assignee or email remains.
- [ ] No organization, customer, client, or internal project name remains.
- [ ] No internal iteration path remains.
- [ ] No internal URL or API endpoint remains.
- [ ] No tenant, workspace, subscription, project, or environment identifier remains.
- [ ] No credentials, tokens, keys, connection strings, or secrets remain.
- [ ] Company and client branding is removed or explicitly authorized.
- [ ] Cached data and preview values have been reviewed.
- [ ] Hidden pages, bookmarks, tooltips, filters, and drill-through targets have been reviewed.
- [ ] File properties, parameters, query names, model descriptions, and resources have been reviewed.
- [ ] Screenshots have been inspected at full resolution.
- [ ] Public files are classified and approved for external disclosure.

### Production release

- [ ] Source ownership is confirmed.
- [ ] Source-system access is approved.
- [ ] Data classification is documented.
- [ ] Privacy and contractual requirements are assessed.
- [ ] Export and sharing conditions are defined.
- [ ] Non-production data is synthetic, masked, or formally approved.
- [ ] Data retention and disposal requirements are documented.

## 3. Power Query and source validation

- [ ] Source parameters point to the correct environment.
- [ ] Credentials use the approved identity and storage method.
- [ ] Required gateway is available and correctly configured.
- [ ] Queries connect successfully.
- [ ] Required source columns are selected explicitly.
- [ ] Data types match the documented schema.
- [ ] Text fields are cleaned and trimmed.
- [ ] Blank assignees map to `Unassigned`.
- [ ] Status mapping is centralized.
- [ ] Every source state maps to an approved normalized status or `Other`.
- [ ] Workstream mapping is controlled.
- [ ] Phase mapping does not depend on the position of a tag.
- [ ] Duplicate source queries have been removed or justified.
- [ ] Staging queries have load disabled.
- [ ] Query folding is preserved where applicable and useful.
- [ ] Privacy levels are configured appropriately.
- [ ] Row volume is within the expected range.
- [ ] Source schema matches the approved contract.
- [ ] Refresh completes without Power Query errors.

### Required reconciliation

| Check | Expected result | Actual result | Evidence |
| --- | --- | --- | --- |
| Source row count | Within approved range | | |
| FactWorkItems row count | Reconciles to unique source items | | |
| Duplicate WorkItemId | 0 | | |
| Missing required identifiers | 0 | | |
| Unmapped status exceptions | 0 or approved exceptions | | |
| Invalid date sequences | 0 | | |
| Unknown workstreams | 0 or approved exceptions | | |

## 4. Semantic-model validation

- [ ] `FactWorkItems` contains one row per current `WorkItemId`.
- [ ] Dimension keys are unique.
- [ ] Every fact key resolves to a valid dimension member.
- [ ] Unknown and Unassigned members are intentional and visible.
- [ ] Relationship cardinalities match the documented model.
- [ ] Filter direction is single by default.
- [ ] No ambiguous relationship path exists.
- [ ] Bidirectional relationships are removed or justified by a tested requirement.
- [ ] `DimDate` is complete and marked as the date table.
- [ ] Auto date/time is disabled.
- [ ] Created Date is the intentional active date relationship.
- [ ] Inactive date relationships are used through explicit measures.
- [ ] `IsDeliveryItem` matches the metric dictionary.
- [ ] Work-item hierarchy behaves as expected.
- [ ] Technical columns not needed by consumers are hidden.
- [ ] User-facing columns have clear names and descriptions.
- [ ] Measures are stored in the approved measures table and display folders.

## 5. DAX and business-rule validation

- [ ] Total Portfolio Items matches the modeled inventory.
- [ ] Total Delivery Items includes only approved delivery types.
- [ ] Completed Items uses the normalized Closed state.
- [ ] Completion Rate uses compatible numerator and denominator scopes.
- [ ] Completion Rate remains between 0% and 100%.
- [ ] New, Active, In Validation, On Hold, Closed, and Other are mutually exclusive.
- [ ] Status Reconciliation Difference equals 0.
- [ ] At Risk Items counts each qualifying item once.
- [ ] Blocked, overdue, and stale concepts are tested separately.
- [ ] The stale threshold matches the approved parameter.
- [ ] On Hold treatment matches the approved rule.
- [ ] Unassigned Open Items includes blank ownership.
- [ ] Average Open Item Age uses open delivery items.
- [ ] Average Cycle Time uses valid activation and close dates.
- [ ] Story-point completion is labeled separately from item-count completion.
- [ ] Dynamic Top N changes with filters and contains no fixed names.
- [ ] Measures return appropriate values for empty filter contexts.
- [ ] Totals reconcile across workstream, assignee, phase, type, and status.

### Metric regression record

| Metric | Previous expected result | Current result | Difference explained? | Evidence |
| --- | ---: | ---: | --- | --- |
| Total Delivery Items | | | | |
| Completed Items | | | | |
| Completion Rate | | | | |
| Active Items | | | | |
| Items In Validation | | | | |
| On Hold Items | | | | |
| At Risk Items | | | | |
| Unassigned Open Items | | | | |

## 6. Report-page validation

### Landing page

- [ ] Report title and purpose are clear.
- [ ] Navigation buttons open the intended pages.
- [ ] Hidden pages do not appear unexpectedly in navigation.
- [ ] Branding is approved for the target audience.
- [ ] Version or last-update information is visible where required.

### Executive overview

- [ ] Cards match the metric dictionary.
- [ ] Status distribution reconciles with the total scope.
- [ ] Workstream progress uses the approved denominator.
- [ ] Risk indicators reconcile to detail.
- [ ] Trend direction and comparison period are clear.
- [ ] Executive visuals lead to actionable detail.
- [ ] Colors follow a documented and accessible meaning.

### Operational overview

- [ ] Workload by assignee includes Unassigned.
- [ ] Top N is dynamic.
- [ ] Work-item type and status scopes reconcile.
- [ ] Slicers affect the intended visuals.
- [ ] Cross-highlighting and cross-filtering behavior is tested.
- [ ] Detail tables show enough context to take action.

### Backlog

- [ ] Default state is neutral or visibly disclosed.
- [ ] Workstream, type, status, and search filters work.
- [ ] A clear reset-filters action is available.
- [ ] Saved filters do not imply that excluded items do not exist.
- [ ] IDs and titles reconcile to the synthetic or approved source.
- [ ] Date, ageing, parent, owner, and risk context are visible where required.

### Risks and bottlenecks

- [ ] Risk cards use the same logic as the metric dictionary.
- [ ] Risk-detail rows reconcile to the cards.
- [ ] Blocked, overdue, stale, and unassigned categories are distinguishable.
- [ ] Ageing values are correct.
- [ ] Heatmaps or rankings respond to current filters.
- [ ] Users can identify the responsible role and required action.
- [ ] Empty states communicate that no matching risk was found rather than displaying a broken visual.

## 7. Filters, bookmarks, and navigation

- [ ] Report-level filters are documented.
- [ ] Page-level filters are documented.
- [ ] Visual-level filters are intentional.
- [ ] No residual filter references a deleted or renamed measure.
- [ ] No personal-name filter is saved in the public version.
- [ ] Default slicer selections are approved.
- [ ] Reset buttons restore the intended default state.
- [ ] Bookmarks capture only intended display, filter, and navigation properties.
- [ ] Drill-through filters behave as expected.
- [ ] Tooltip pages show the correct context.
- [ ] Navigation works after renaming, hiding, or adding pages.
- [ ] Mobile layout is reviewed when it is part of the release scope.

## 8. Visual quality and accessibility

- [ ] Titles describe the metric and context.
- [ ] Units, percentages, and date formats are consistent.
- [ ] Labels are not clipped.
- [ ] Tooltips explain definitions and denominators.
- [ ] Visual density supports quick interpretation.
- [ ] Color is not the only method used to communicate status.
- [ ] Text and visual contrast are legible.
- [ ] Tab order follows a logical reading sequence.
- [ ] Alternative text is added to important visuals where supported.
- [ ] Decorative objects are excluded from assistive reading where supported.
- [ ] Keyboard navigation is tested for intended consumer scenarios.
- [ ] Focus mode and data-table views remain understandable.
- [ ] Custom visuals are approved, supported, and necessary.
- [ ] Empty and zero states are distinguished from unavailable data.

## 9. Performance validation

- [ ] Unused source columns are removed.
- [ ] Duplicate work-item imports are eliminated.
- [ ] Automatic date tables are disabled.
- [ ] High-cardinality columns are not used unnecessarily in visuals.
- [ ] Relationships and measures follow the recommended model.
- [ ] Visual count per page is reasonable.
- [ ] Interactions that do not add value are disabled.
- [ ] Slow visuals are identified through Performance Analyzer.
- [ ] Representative filter interactions complete within the approved expectation.
- [ ] Dataset refresh duration is within the operational threshold.
- [ ] Model size is recorded and reviewed.
- [ ] Custom visual performance is tested in the target service.

### Performance record

| Test | Expected | Actual | Result | Evidence |
| --- | ---: | ---: | --- | --- |
| Desktop refresh duration | | | | |
| Service refresh duration | | | | |
| Executive page render | | | | |
| Operational page render | | | | |
| Risk page render | | | | |
| Model size | | | | |

## 10. Security and access

- [ ] Workspace is the correct environment.
- [ ] Workspace roles follow least privilege.
- [ ] Dataset and report permissions are reviewed.
- [ ] Application audiences are correct.
- [ ] Sharing links are reviewed.
- [ ] Build permission is granted only where required.
- [ ] Export permissions match data classification.
- [ ] Row-level security is implemented and tested where required.
- [ ] RLS tests include representative roles and a denied-access scenario.
- [ ] Service principals and gateways use approved identities.
- [ ] Credentials are valid and not embedded in the report.
- [ ] Sensitivity labels are applied where required.
- [ ] Audit and usage monitoring are enabled according to policy.
- [ ] A consumer account has validated the released experience.

## 11. Power BI Service readiness

- [ ] Dataset or semantic model is published to the correct workspace.
- [ ] Report is connected to the intended semantic model.
- [ ] Data-source credentials are valid.
- [ ] Gateway binding is correct where required.
- [ ] Scheduled refresh is configured.
- [ ] Refresh timezone is documented.
- [ ] Refresh failure notifications have an owner.
- [ ] A manual refresh completed successfully.
- [ ] Last-refresh timestamp appears correctly in the report.
- [ ] Application content is updated.
- [ ] Application navigation and audiences are tested.
- [ ] Subscription, alert, or export behavior is validated when used.
- [ ] Lineage view matches the expected deployment.
- [ ] Deployment-pipeline stage and rules are correct when used.

## 12. Documentation and support

- [ ] README reflects the released scope.
- [ ] Metric dictionary matches current measures.
- [ ] Semantic-model documentation matches current tables and relationships.
- [ ] Data-preparation documentation matches current queries and parameters.
- [ ] Data dictionary is updated.
- [ ] Known limitations are visible.
- [ ] Operational owner is identified.
- [ ] Support and escalation path is documented.
- [ ] Refresh recovery steps are documented.
- [ ] Change history is updated.
- [ ] Release evidence is stored in the approved location.

## 13. Approval decision

| Decision question | Yes / No / N/A | Evidence or comment |
| --- | --- | --- |
| Are all applicable blocking gates cleared? | | |
| Do executive metrics reconcile with detail? | | |
| Are privacy and security requirements satisfied? | | |
| Has representative consumer testing passed? | | |
| Is the release supportable and recoverable? | | |
| Is public publication approved, when applicable? | | |

### Final decision

- [ ] **Approved** — release may proceed.
- [ ] **Conditionally approved** — release may proceed under documented, time-bound exceptions.
- [ ] **Rejected** — release must not proceed.

| Approval | Name or role | Decision | Date |
| --- | --- | --- | --- |
| Business owner | | | |
| Technical reviewer | | | |
| Privacy / Security, when applicable | | | |
| Release owner | | | |

## 14. Post-release validation

Complete immediately after release:

- [ ] Correct version is visible.
- [ ] Landing and navigation work.
- [ ] Executive totals match pre-release validation.
- [ ] Filters and bookmarks use the intended defaults.
- [ ] Refresh status is healthy.
- [ ] Consumer access is correct.
- [ ] No unauthorized consumer can access the content.
- [ ] Application content is current.
- [ ] Audit or usage events are generated where expected.
- [ ] No critical error was reported during the observation period.
- [ ] Release record is closed or rollback is initiated.

## Rollback triggers

Initiate rollback or emergency remediation when:

- a material data disclosure occurs;
- executive indicators are materially incorrect;
- critical detail does not reconcile to summary;
- intended users lose access or unauthorized users gain access;
- refresh failure makes the published result unreliable;
- source or model changes break required visuals;
- performance prevents normal report use;
- a blocking security, privacy, or compliance issue is identified.

## Disclaimer

This checklist is an anonymized portfolio artifact and a configurable baseline. It does not replace an organization's release-management, security, privacy, accessibility, records-management, or Power BI administration requirements.
