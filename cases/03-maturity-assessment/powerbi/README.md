# Maturity Assessment — Power BI demonstration

[Back to the case](../README.md)

[Download the template](DataGovernance_Maturity_Assessment.pbit?raw=true).

## Open and inspect

1. Download the PBIT and open it in Power BI Desktop.
2. Allow the model to load and refresh.
3. Inspect the organization/unit and assessment-date slicers; use CLEAR FILTERS to reset selections.
4. Check the eight-domain radar and the expected values below.

The model queries contain inline synthetic values and require no original Excel workbook, corporate credentials, or external source connection. Rendering the packaged radar visual depends on your Desktop configuration and visual policies.

| Check | Expected |
| --- | --- |
| Fictional organization/unit | Synthetic Organization / Unit A |
| Assessment date | 2026-09-01 |
| Overall score | 1.75 |
| Maximum score | 3 |
| Percentage of maximum | 58.3% |
| Domain scores D01–D08 | 2.00, 1.50, 2.00, 1.00, 2.50, 1.00, 2.25, 1.75 |

## Scope and limitations

This is the aggregate SYN-MAT-BASE-001 scenario. It is not connected to [synthetic-assessment-results.csv](../data/synthetic-assessment-results.csv). Importing that CSV requires the separate [data dictionary](../data-dictionary.md) and a model adapted to its control-level grain.

Do not interpret the percentage as compliance, coverage, or certification. Internal model identifiers retain some Portuguese names to preserve visual bindings; report-facing labels are in English.

## Review status

The author successfully tested the sanitized candidate in Desktop and returned a reviewed export. ZIP integrity, source queries, saved report metadata and known original identifiers were checked again before publication. No Service deployment or scheduled-refresh verification is claimed.

The tested file is published unchanged. Its description retains the earlier phrase “Desktop validation required”; this wording predates the author's successful test.

## Screenshot capture

Open the reviewed public template, reset slicers, and capture the full report canvas with all eight domains readable. Capture a second filtered view only if useful. Exclude account menus, local paths, desktop notifications and unrelated windows. Store approved images in the root assets directory, then embed them in the case README.
