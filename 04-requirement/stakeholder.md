# Stakeholders

**Project:** Streamlining Prior Authorization (outpatient MRI order, automated ePA with HL7 Da Vinci)
**Status:** Draft

This page lists who is involved in the PA process, what each group needs, and where they appear in the swimlane. Stakeholder IDs (SH-xx) are used in the requirements and user stories.

## Stakeholder list

| ID | Stakeholder | Swimlane lane | Role in the PA process | What they care about | Involvement |
|---|---|---|---|---|---|
| SH-01 | Patient | Patient | Gets the MRI visit, then schedules once PA is approved | Fast scheduling, no surprise delays or costs | Affected by the process, not a system user |
| SH-02 | Clinician | Clinician | Signs the MRI order, decides next steps if PA is denied | Less time on paperwork, a clear answer on denials | Direct user (EHR order screen) |
| SH-03 | Clinic staff | Clinic Staff | Opens the DTR app, completes missing info, submits, contacts the patient | Fewer manual steps, less rework, no phone or fax follow-up | Main user of the new workflow |
| SH-04 | EHR / IT team | EHR, Da Vinci apps (provider side) | Supports the CDS hook, DTR launch, PAS client, and ClaimResponse in the EHR | Stable integration, security, easy upkeep | Builds and maintains the integration |
| SH-05 | Payer systems team | Da Vinci apps (payer side) | Runs the CRD, DTR questionnaire, and PAS services | Correct, complete requests; standard formats | Provides the payer-side services |
| SH-06 | Payer UM reviewer (RN / Medical Director) | Payer | Reviews cases the system can't approve automatically and makes the final decision | Complete clinical documentation, clear criteria | Decision maker on flagged cases |
| SH-07 | Clinic operations manager *(optional)* | Not in swimlane | Owns staff workload and the cost of PA work | Lower cost per PA, shorter turnaround | Sponsor of the change |

*SH-07 does not have a swimlane lane. Keep it if you want a business owner for the cost KPI, or delete it to match the swimlane exactly.*

## Stakeholder notes

Fill this in for each stakeholder you want to explain further. Keep it to 2 or 3 lines each.

### SH-03 Clinic staff
- **Current pain (as-is):** *(link to PP-xx)*
- **What changes in the to-be:** *(for example, DTR pre-fills the questionnaire, so staff review instead of re-enter)*
- **Related requirements:** *(FR-xx, filled in later)*

### SH-06 Payer UM reviewer
- **Current pain (as-is):** *(link to PP-xx)*
- **What changes in the to-be:** *(for example, cases arrive with structured data)*
- **Related requirements:** *(FR-xx, filled in later)*

*(Repeat for the others as needed.)*

## Influence and interest

A quick view of who needs the most attention when designing the change.

| Group | Influence on the outcome | Interest in the outcome |
|---|---|---|
| SH-03 Clinic staff | High | High |
| SH-02 Clinician | Medium | High |
| SH-04 EHR / IT team | High | Medium |
| SH-06 Payer UM reviewer | High | Medium |
| SH-05 Payer systems team | High | Medium |
| SH-07 Clinic operations manager | Medium | High |
| SH-01 Patient | Low | High |

## Assumptions

- The ratings above are my own judgment, based on public sources and the swimlane. They have not been checked with real stakeholders.
- See [limits-and-risks](../01-scope/limits-and-risks.md) for the project's other limits. *(Update this path when the folders are final.)*
