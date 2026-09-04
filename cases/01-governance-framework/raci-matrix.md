# Data Governance RACI Matrix

[← Back to the case overview](README.md) · [View the complete framework](framework.md)

## Purpose

This matrix defines decision ownership and participation across the core processes of the Tool-Agnostic Data Governance Framework. It is a reusable baseline and should be adapted to each organization's structure, risk profile, and regulatory context.

## RACI legend

| Code | Meaning | Description |
| --- | --- | --- |
| **R** | Responsible | Performs or coordinates the work. |
| **A** | Accountable | Owns the decision and final outcome. Ideally, each activity has one accountable role. |
| **C** | Consulted | Provides expertise or input before the decision or work is completed. |
| **I** | Informed | Receives relevant decisions, progress, or outcomes. |

## Roles

| Abbreviation | Role |
| --- | --- |
| **DGO** | Data Governance Office / Team |
| **DO** | Data Owner |
| **DS** | Data Steward |
| **DP** | Data Producer |
| **DC** | Data Custodian |
| **DA** | Data Architect |
| **P/DPO** | Privacy / Data Protection Officer |
| **SEC** | Information Security |
| **AUD** | Internal Audit / Compliance |
| **DU** | Data User |

## Core RACI matrix

| Governance activity | DGO | DO | DS | DP | DC | DA | P/DPO | SEC | AUD | DU |
| --- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Define and maintain the governance framework | **A/R** | C | C | I | C | C | C | C | C | I |
| Assign Data Owners and Data Stewards | **R** | **A** | I | I | I | I | I | I | I | I |
| Define the business purpose of a data asset | C | **A/R** | C | C | I | C | C | I | I | I |
| Classify data and approve criticality | C | **A** | **R** | C | C | C | C | C | I | I |
| Register and maintain business metadata | C | **A** | **R** | C | I | C | C | I | I | I |
| Validate technical metadata and lineage | I | C | **R** | C | C | **A** | I | I | I | I |
| Define authoritative sources and master-data rules | C | **A** | **R** | C | C | **R** | I | I | I | I |
| Define and monitor data-quality rules | C | **A** | **R** | **R** | C | C | I | I | I | I |
| Remediate data-quality issues at source | I | **A** | **R** | **R** | C | C | I | I | I | I |
| Approve data access based on business need | I | **A/R** | C | I | C | I | C | C | I | I |
| Implement and revoke technical access | I | **A** | I | I | **R** | C | I | C | I | I |
| Define access-control and security standards | C | C | I | I | **R** | C | C | **A** | C | I |
| Conduct periodic access reviews | C | **A** | **R** | I | **R** | I | C | C | I | I |
| Define retention and disposal requirements | **R** | **A** | C | I | C | C | **R** | C | C | I |
| Execute archival or secure disposal | I | **A** | C | I | **R** | C | C | C | I | I |
| Validate privacy requirements and legal basis | I | C | C | I | I | I | **A/R** | C | C | I |
| Approve external data sharing | C | **A** | R | I | C | I | **R** | C | I | I |
| Respond to privacy rights or consent revocation | C | **A** | **R** | I | **R** | C | **R** | C | I | I |
| Monitor governance KPIs and exceptions | **A/R** | C | **R** | I | C | C | C | C | I | I |
| Preserve governance and control evidence | **A** | C | **R** | I | **R** | C | C | **R** | C | I |
| Assess control design and effectiveness | C | I | C | I | C | C | C | C | **A/R** | I |
| Escalate material governance risks | **R** | **A** | **R** | I | C | C | C | C | I | I |

## Decision-rights guidance

### Data Owner

The Data Owner is accountable for decisions tied to business purpose, classification, acceptable use, data quality, access, sharing, retention, and risk acceptance for the asset.

### Data Steward

The Data Steward coordinates day-to-day governance activities, maintains metadata, monitors quality, prepares decisions, and follows remediation through completion.

### Data Custodian

The Data Custodian implements technical controls but does not independently determine business purpose, classification, or acceptable access.

### Data Architect

The Data Architect owns technical validation of data models, lineage, integration patterns, and architecture standards while supporting master-data design.

### Privacy and Information Security

Privacy and Security provide specialist authority in their respective domains. They may become accountable when a decision is explicitly delegated to them by policy or law.

### Data Governance Office

The Data Governance Office owns the governance system, standards, oversight, indicators, and escalation process. It does not replace the accountability of business Data Owners.

### Internal Audit / Compliance

Audit or Compliance independently assesses control design and effectiveness. It should not operate the same controls it is expected to assess independently.

## Tailoring rules

Before adopting this matrix:

1. Replace generic roles with the organization's approved role names.
2. Confirm that each activity has one clear accountable role.
3. Separate Privacy, Legal, Compliance, and Internal Audit when their mandates differ.
4. Add platform, domain, product, or regional roles where necessary.
5. Resolve combined **A/R** assignments when accountability and execution should be segregated.
6. Define escalation paths for absent, disputed, or inactive ownership.
7. Review the matrix whenever operating models, regulations, systems, or risks materially change.

## Example application

For a new confidential customer-data asset:

1. The **Data Owner** defines its business purpose and is accountable for classification.
2. The **Data Steward** registers metadata and coordinates classification evidence.
3. **Privacy** validates the applicable personal-data requirements.
4. **Security** advises on protection requirements.
5. The **Data Architect** validates lineage and integration context.
6. The **Data Custodian** implements the approved technical access.
7. The **Data Governance Office** monitors completeness and unresolved exceptions.
8. **Audit / Compliance** may independently assess whether the controls operate effectively.

## Disclaimer

This RACI matrix is an anonymized portfolio artifact and a configurable governance baseline. It must be validated against each organization's policies, legal obligations, decision authorities, segregation-of-duties requirements, and operating model.
