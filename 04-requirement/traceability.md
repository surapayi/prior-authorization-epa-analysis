# Traceability

**Project:** Streamlining Prior Authorization (outpatient MRI order, automated ePA with HL7 Da Vinci)
**Status:** Draft

This page connects each pain point to the requirements, user stories, and KPI that relate to it. It shows why each requirement exists and which number it is meant to move.

## How to read it

Read each row left to right: a **pain point** in the as-is flow is fixed by a **requirement**, is described by a **user story**, happens at a **swimlane step** in the to-be flow, and is measured by a **KPI**.

*KPI IDs are placeholders: KPI-01 = turnaround (T0 to T2), KPI-02 = clinic staff effort per PA. Match them to your metrics file.*

## Main table

| Pain point | To-be swimlane step | Requirements | User stories | KPI |
|---|---|---|---|---|
| PP-01 Coverage and PA rules looked up by hand | CRD: Active coverage? / CRD: PA required? / Resolve coverage with patient | FR-01 to FR-06 | US-01, US-02 | KPI-02 |
| PP-02 Packet put together by hand | Display CRD card with DTR link / Clicks the link and launches DTR app | FR-06, FR-07, FR-08 | US-03 | KPI-02 |
| PP-03 Same data typed into each payer's portal | DTR app auto-populates questionnaire / Client PAS constructs FHIR Claim bundle | FR-08, FR-11, FR-12, FR-13 | US-03, US-05 | KPI-02 |
| PP-04 Missing information found after submission | Reviews, completes missing info and clicks submit in EHR | FR-07, FR-09, FR-10 | US-04, US-09 | KPI-01, KPI-02 |
| PP-05 Calling or checking for status | Payer PAS evaluates / Receives ClaimResponse | FR-16, FR-20 | US-08 | KPI-01, KPI-02 |
| PP-06 Decision typed in by hand, scheduling told manually | Receives ClaimResponse / Approved or Denied? / Contact patient | FR-16, FR-17, FR-18 | US-06 | KPI-02 |
| PP-07 Scan waits for the response | Meets criteria automatically? / Final evaluation / Contact patient | FR-14, FR-15, FR-18 | US-06, US-09 | KPI-01 |

## Requirements without a pain point

| Requirement | Where it comes from | To-be swimlane step | User stories | KPI |
|---|---|---|---|---|
| FR-19 Notify clinician on denial | Denial path in the swimlane | Determine next steps / Modify or cancel order | US-07 | None |
| FR-21 Record T0, T1, and T2 timestamps | The KPIs | T0, T1, T2 markers | None | KPI-01 (makes it measurable) |


## Notes

- The swimlane step names match the to-be diagram. If you rename a step in the diagram, update it here.
- Payer-side items are assumptions. See [limits-and-risks](../01-scope/limits-and-risks.md). *(Update this path when the folders are final.)*
