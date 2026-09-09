# Data Governance Maturity — v2.2 English edition

Four-page Power BI project with local synthetic data.

## Open

1. Extract the entire download into a short local Windows path, such as `C:\PowerBI\Maturity`.
2. Keep `Maturity.pbip`, `Maturity.Report`, and `Maturity.SemanticModel` together.
3. Open `Maturity.pbip` in Power BI Desktop, outside the ZIP.
4. Select **Refresh** to load the included fictional assessment.
5. Save as PBIX in Desktop if you prefer a single report file.

See [Microsoft's Power BI project documentation](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-overview) for project support and settings.

## Pages

| Page | Purpose |
| --- | --- |
| 01 Executive overview | Latest score, maturity level, pillar scores and lowest-scoring pillar |
| 02 Pillar profile | Eight-pillar radar with a fixed 0–3 scale |
| 03 Assessment history | Valid assessment count, historical average and record traceability |
| 04 Quality and methodology | Structural quality checks, maturity thresholds and scope |

## Expected synthetic baseline

| Check | Expected |
| --- | --- |
| Organization / Unit | Synthetic Organization / Unit A |
| Assessment date and time | 2026-09-01 10:00 |
| Latest score | 1.75 / 3.00 |
| Percentage of maximum | 58.3% |
| Maturity level | Defined |
| Change | No previous |
| Valid assessments / total records | 1 / 1 |
| Quality exception cards | All zero |
| Pillar scores in methodology order | 2.00, 1.50, 2.00, 1.00, 2.50, 1.00, 2.25, 1.75 |
| Lowest-scoring pillar | Master and Reference Data (1.00); tie resolved by pillar order |

## Language and validation

The Portuguese v2.2 source was opened and visually approved by the author. This English edition translates report captions, page names, pillar values, maturity levels, status messages and explanatory text. Explicit text-number formatting uses `en-US`; date fields use ISO-style formatting. Native Power BI interface strings, such as the slicer's “All” selection, and some automatic numeric/date rendering follow Desktop language and regional settings. Use English Desktop settings for an entirely English viewing experience.

Technical model identifiers remain unchanged to preserve bindings. Visual positions, styles, IDs, relationships, calculation thresholds and synthetic numeric inputs are unchanged. Static validation covers JSON parsing, references, unchanged layout and calculation structure, and package contents. The translated edition has not been executed or rendered in Power BI Desktop in the publishing environment; English Desktop screenshots remain pending.

## Interpretation

The scale maximum is not an approved target. Percentage of maximum is not compliance or assessment coverage. The five aggregate maturity bands on the report are distinct from the four response scores used by the questionnaire. `Validated` denotes a structurally valid aggregate record, not independently verified question-level evidence.

The latest and previous assessments are selected within the period for one organization/unit, ordered by timestamp then highest ID. With only one valid record, change is unavailable. Each page has independent filters.

Only local inline synthetic data is loaded. This project does not import the separate control-level CSV, contain question-level evidence, or claim a Power BI Service deployment.
