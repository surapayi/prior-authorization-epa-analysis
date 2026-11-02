# Requirements

**Project:** Streamlining Prior Authorization (outpatient MRI order, automated ePA with HL7 Da Vinci)
**Status:** Draft

This page lists what the to-be process needs to do. Each requirement points back to the pain point it fixes (PP-xx) and the stakeholder it serves (SH-xx).

## How to read this page

| Prefix | Meaning |
|---|---|
| BR | Business requirement |
| FR | Functional requirement |
| NFR | Non-functional requirement |
| PP | Pain point (see the as-is folder) |
| SH | Stakeholder (see stakeholders page) |
| KPI | Metric (see the metrics folder) |

**Priority** uses MoSCoW: Must, Should, Could. **Side** shows who builds or runs it: Provider (clinic and EHR) or Payer. Payer-side requirements are assumptions about what the payer supports.

## Business requirements

| ID | Requirement | KPI |
|---|---|---|
| BR-01 | Reduce the time from order created (T0) to final determination received (T2) | KPI-01 *(turnaround)* |
| BR-02 | Reduce clinic staff effort per PA request, excluding idle waiting time | KPI-02 *(staff effort)* |

*KPI IDs are placeholders. Match them to your metrics file.*

## Functional requirements

### A. Order and coverage check

| ID | Requirement | Pain point | Stakeholder | Priority | Side |
|---|---|---|---|---|---|
| FR-01 | The EHR shall call the payer's CRD service through a CDS hook when an MRI order is signed. | PP-01 | SH-02, SH-04 | Must | Provider |
| FR-02 | The CRD service shall return whether coverage is active and whether PA is required for the order. | PP-01 | SH-05 | Must | Payer |
| FR-03 | The EHR shall show the CRD result as a card in the order screen. | PP-01 | SH-02, SH-03 | Must | Provider |
| FR-04 | If PA is not required, the EHR shall let the order go on to scheduling without any PA steps. | PP-01 | SH-03 | Must | Provider |
| FR-05 | If coverage is not active, the EHR shall flag the order to clinic staff so they can resolve coverage with the patient. | PP-01 | SH-03 | Must | Provider |
| FR-06 | If PA is required, the CRD card shall include a link that launches the DTR app. | PP-02 | SH-03 | Must | Provider |

### B. Documentation gathering

| ID | Requirement | Pain point | Stakeholder | Priority | Side |
|---|---|---|---|---|---|
| FR-07 | The DTR app shall load the payer's questionnaire for the order. | PP-02, PP-04 | SH-03 | Must | Provider |
| FR-08 | he DTR app shall fill in questionnaire answers from EHR data using Clinical Quality Language (CQL). | PP-02, PP-03 | SH-03 | Must | Provider |
| FR-09 | The DTR app shall show staff which required answers are still missing before submission. | PP-04 | SH-03 | Must | Provider |
| FR-10 | The EHR shall not allow submission until required answers are complete and staff have marked the questionnaire complete. | PP-04 | SH-03, SH-06 | Must | Provider |

### C. Submission

| ID | Requirement | Pain point | Stakeholder | Priority | Side |
|---|---|---|---|---|---|
| FR-11 | Staff shall be able to submit the request from the EHR with one action. | PP-03 | SH-03 | Must | Provider |
| FR-12 | Upon completion, the DTR app shall save a FHIR QuestionnaireResponse back to the EHR. The PAS client shall use this saved response to build the FHIR Claim bundle. | PP-03 | SH-04 | Must | Provider |
| FR-13 | The payer shall accept the bundle and, if its systems need it, convert it to an X12 278 transaction for internal processing, and translate the response back to a FHIR ClaimResponse for transmission to the provider. | PP-03 | SH-05 | Could | Payer |

### D. Payer decision

| ID | Requirement | Pain point | Stakeholder | Priority | Side |
|---|---|---|---|---|---|
| FR-14 | The payer's PAS shall check the request against utilization management criteria and approve it automatically when the criteria are met. | PP-07 | SH-05 | Must | Payer |
| FR-15 | Requests that are not approved automatically shall be queued for a payer UM reviewer (RN or Medical Director). | PP-07 | SH-06 | Must | Payer |
| FR-16 | The payer shall return the final decision electronically as a ClaimResponse (approved with an authorization number, or denied). | PP-05, PP-06 | SH-05 | Must | Payer |

### E. Response handling

| ID | Requirement | Pain point | Stakeholder | Priority | Side |
|---|---|---|---|---|---|
| FR-17 | The EHR shall receive the ClaimResponse and attach the decision and authorization number to the order without manual entry. | PP-06 | SH-03, SH-04 | Must | Provider |
| FR-18 | When a request is approved, the EHR shall notify clinic staff so they can contact the patient to schedule. | PP-06, PP-07 | SH-03 | Must | Provider |
| FR-19 | When a request is denied, the EHR shall notify the clinician so they can decide next steps (modify or cancel the order). Appeals are out of scope. | None (from swimlane) | SH-02 | Must | Provider |

### F. Status and measurement

| ID | Requirement | Pain point | Stakeholder | Priority | Side |
|---|---|---|---|---|---|
| FR-20 | The EHR shall show the current status of each PA request (submitted, waiting for decision, approved, denied) so staff do not need to call or check a portal. | PP-05 | SH-03 | Should | Provider |
| FR-21 | The EHR shall record timestamps for order created (T0), request submitted (T1), and final determination received (T2). | None (from KPIs) | SH-07 | Must | Provider |

## Non-functional requirements

| ID | Requirement | Stakeholder | Priority |
|---|---|---|---|
| NFR-01 | Patient data shall be protected in transit and access shall be authorized. Calls between the EHR, DTR app, and payer shall use secure, authorized connections. | SH-04, SH-05 | Must |
| NFR-02 | The system shall keep an audit trail of what was sent, when, by whom, and what came back. | SH-04, SH-07 | Must |
| NFR-03 | Exchanges shall use FHIR and the Da Vinci CRD, DTR, and PAS implementation guides. (v2.1.0, or latest version supported by the target payer) | SH-04, SH-05 | Must |
| NFR-04 | The CRD check happens synchronously during the ordering workflow. | SH-02 | Must |
| NFR-05 | The DTR app shall launch as a native SMART on FHIR application inside the EHR workflow, utilizing OAuth2 for seamless authentication without a separate login. | SH-03 | Should |
| NFR-06 | If the CRD call fails, or the payer does not support these APIs, the order shall go on and the clinic shall use the as-is process. | SH-03, SH-07 | Must |

## Pain point coverage

| Pain point | Requirements that address it | Note |
|---|---|---|
| PP-01 Coverage and PA rules looked up by hand | FR-01 to FR-06 | |
| PP-02 Packet put together by hand | FR-06, FR-07, FR-08 | |
| PP-03 Same data typed into each payer's portal | FR-08, FR-11, FR-12, FR-13 | |
| PP-04 Missing information found after submission | FR-07, FR-09, FR-10 | |
| PP-05 Calling or checking for status | FR-16, FR-20 | |
| PP-06 Decision typed in by hand, scheduling told manually | FR-16, FR-17, FR-18 | |
| PP-07 Scan waits for the response | FR-14, FR-15, FR-18 | Mostly depends on the payer, so the clinic controls only part of it |

## Note

- **No pain point behind FR-19 and FR-21.** FR-19 comes from the denial path in the swimlane, and FR-21 comes from the KPIs. 
- **Pended status.** The PAS can return an interim “pended” response when the payer needs more information. It is not modeled here because it would add extra steps and loops to a diagram meant to show the main path. A pended request would lengthen turnaround and add staff effort, so the results may understate both.
- **Priorities are my judgment.** They have not been checked with real stakeholders.
