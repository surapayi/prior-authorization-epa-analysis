# FHIR Data Mapping

**Project:** Streamlining Prior Authorization (outpatient MRI order, automated ePA with HL7 Da Vinci)
**Status:** Draft

This page shows which data moves between the EHR and the payer in the to-be process, and which FHIR resource and element carries it. Each row points to the requirement (FR-xx) it supports.

It is a design-level mapping built from the public Da Vinci guides. It is not tested against a real EHR or payer.

## Versions and scope

| Item | Choice |
|---|---|
| FHIR version | R4 |
| Da Vinci guides | CRD, DTR, and PAS, version 2.1.0 (see NFR-03) |
| Base profiles | US Core, as required by each guide |
| Use case | Outpatient MRI order |
| Out of scope | X12 278 conversion (FR-13), pended responses, appeals |

## How to read this page

- **EHR data** is what the clinic already knows or enters in the EHR.
- **FHIR element** is where that data goes in a FHIR message. The profile name is in brackets.
- **Used in** shows the step in the to-be swimlane: CRD, DTR, or PAS.
- Rows marked *(example)* depend on the payer's own questionnaire or rules. The real values will differ by payer.

## 1. Exchange overview

One row per message in the to-be swimlane.

| # | Exchange | From → To | FHIR / API | Guide | Requirements |
|---|---|---|---|---|---|
| 1 | Order signed, coverage check requested | EHR → payer CRD service | CDS Hooks `order-sign` request (draft orders, plus Patient, Practitioner, and Coverage data) | CRD | FR-01, NFR-04 |
| 2 | Coverage and PA result returned | Payer CRD service → EHR | CDS Hooks response: cards, with the coverage information extension | CRD | FR-02 to FR-06 |
| 3 | DTR app launched | EHR → DTR app | SMART on FHIR app launch from the card link | CRD, DTR | FR-06, NFR-05 |
| 4 | Questionnaire and rules loaded | Payer → DTR app | Questionnaire, plus CQL Library | DTR | FR-07 |
| 5 | Questionnaire filled in and saved | DTR app ↔ EHR | QuestionnaireResponse (read EHR data, then save the response) | DTR | FR-08 to FR-10, FR-12 |
| 6 | Request submitted | EHR (PAS client) → payer PAS | `Claim/$submit` with a PAS Request Bundle | PAS | FR-11, FR-12 |
| 7 | Decision returned | Payer PAS → EHR | Response Bundle containing a ClaimResponse | PAS | FR-14, FR-16, FR-17 |
| 8 | Status and timestamps recorded | Inside the EHR | Local status, AuditEvent | None (EHR) | FR-20, FR-21, NFR-02 |

## 2. Field-level mapping

### A. Order and patient context (CRD request)

| EHR data | FHIR element | Used in | FR | Note |
|---|---|---|---|---|
| MRI order | `ServiceRequest` in the hook's `draftOrders` (US Core ServiceRequest) | CRD | FR-01 | The order is still a draft when the hook fires. |
| MRI procedure code (CPT) | `ServiceRequest.code` | CRD, PAS | FR-01, FR-02 | *(Example: 72148, MRI lumbar spine without contrast.)* Also used as the PAS item code (section D). |
| Reason for the exam | `ServiceRequest.reasonCode` or `reasonReference` (to a Condition) | CRD, PAS | FR-01 | ICD-10-CM. Feeds the PAS diagnosis (section D). |
| Order priority | `ServiceRequest.priority` | CRD, PAS | FR-01 | Routine vs urgent. The payer's decision deadline can depend on it. |
| Order created date and time | `ServiceRequest.authoredOn` | CRD | FR-21 | Used for **T0**. |
| Ordering clinician | `ServiceRequest.requester` (Practitioner or PractitionerRole); hook context `userId` | CRD, PAS | FR-01 | NPI is used in PAS (section D). |
| Patient | Hook context `patientId`; `Patient` (US Core Patient): `identifier` (MRN), `name`, `birthDate`, `gender` | CRD, PAS | FR-01 | The EHR sends or makes these available to the payer. |
| Current encounter | Hook context `encounterId` | CRD | FR-01 | Optional. |
| Patient's insurance | `Coverage`: `status`, `period`, `payor`, `subscriberId`, `beneficiary`, `relationship`, `class` | CRD, PAS | FR-01, FR-02, FR-05 | Sent with the hook as prefetch data, or fetched by the payer. |

### B. Coverage and PA result (CRD response)

| EHR data (what staff and clinicians see) | FHIR element | Used in | FR | Note |
|---|---|---|---|---|
| Active coverage? | `Coverage.status` and `Coverage.period` in the data sent | CRD | FR-02, FR-05 | Not a single CRD field. The payer checks the Coverage it receives. |
| Service covered? | Coverage information extension: `covered` | CRD | FR-02 | Describes the service, not the patient's plan status. |
| PA required? | Coverage information extension: `pa-needed` | CRD | FR-02, FR-04, FR-06 | A "no authorization needed" value lets the order go on to scheduling (FR-04). |
| Documentation needed | Coverage information extension: `doc-needed` | CRD, DTR | FR-06 | Tells the EHR that DTR is needed. |
| Card in the order screen | `Card.summary`, `detail`, `indicator` | CRD | FR-03 | Shown to the clinician at signing. |
| Link to launch DTR | `Card.links` (type `smart`, `url`, `appContext`) | CRD, DTR | FR-06 | `appContext` carries what DTR needs to start, such as the order and the questionnaire. |
| Flag for staff when coverage is not active | EHR rule, based on the CRD result | CRD | FR-05 | EHR behavior (see section 3). |

### C. Documentation (DTR)

| EHR data | FHIR element | Used in | FR | Note |
|---|---|---|---|---|
| Payer's questionnaire | `Questionnaire` (found through the launch context) | DTR | FR-07 | Written by the payer. |
| Auto-fill rules | `Library` (CQL), linked from the Questionnaire | DTR | FR-08 | The DTR app runs the rules against EHR data. |
| Patient details | `Patient` (US Core Patient) | DTR | FR-08 | Name, date of birth, and similar. |
| Diagnoses and history | `Condition` (US Core) | DTR | FR-08 | |
| Clinical findings *(example)* | `Observation` (US Core) | DTR | FR-08 | For example, symptom findings or measurements the payer asks for. |
| Prior treatment *(example)* | `Procedure`, `MedicationRequest` | DTR | FR-08 | For example, therapy or medicines tried before imaging. |
| Prior imaging *(example)* | `DiagnosticReport` or `ImagingStudy` | DTR | FR-08 | |
| Clinic notes | `DocumentReference` (US Core) | DTR, PAS | FR-08, FR-12 | Only if the payer asks for them. |
| Required answer still empty | `Questionnaire.item.required` with no matching answer in `QuestionnaireResponse.item` | DTR | FR-09 | The DTR app shows staff what is missing. |
| Staff mark it complete | `QuestionnaireResponse.status` = `completed` | DTR | FR-10 | The EHR does not submit before this. |
| Who completed it, and when | `QuestionnaireResponse.author`, `authored` | DTR | FR-10, NFR-02 | |
| Completed questionnaire saved | `QuestionnaireResponse` (DTR / SDC profile) created on the EHR's FHIR server | DTR | FR-12 | PAS reads this to build the request. |

### D. Submission (PAS request)

| EHR data | FHIR element | Used in | FR | Note |
|---|---|---|---|---|
| The request package | `Bundle` (PAS Request Bundle), with the Claim as the first entry | PAS | FR-11, FR-12 | |
| What the request is | `Claim.use` = `preauthorization`, `Claim.status` = `active` | PAS | FR-11 | |
| Claim type | `Claim.type` | PAS | FR-11 | Assumed to be `professional` for an outpatient imaging order. Confirm in the guide. |
| Request date and time | `Claim.created` | PAS | FR-21 | Used for **T1**. |
| Standard or urgent | `Claim.priority` | PAS | FR-11 | From the order priority. |
| Patient | `Claim.patient` → `Patient` (PAS Beneficiary Patient) | PAS | FR-12 | |
| Insurance | `Claim.insurance` (focal) → `Coverage` | PAS | FR-12 | |
| Payer | `Claim.insurer` → `Organization` (PAS Insurer Organization) | PAS | FR-12 | |
| Clinic | `Claim.provider` → `Organization` (PAS Requestor Organization) | PAS | FR-12 | NPI and contact details. |
| Ordering clinician | `Claim.careTeam` → `Practitioner` or `PractitionerRole` | PAS | FR-12 | NPI. |
| Diagnosis | `Claim.diagnosis.diagnosisCodeableConcept` | PAS | FR-12 | ICD-10-CM, from the order's reason. |
| Requested service | `Claim.item.productOrService` (CPT) and `Claim.item.serviced[x]` | PAS | FR-12 | |
| Link to the order | `Claim.item` extension `requestedService` → `ServiceRequest` | PAS | FR-12 | |
| Completed questionnaire | `Claim.supportingInfo` → `QuestionnaireResponse` (included in the bundle) | PAS | FR-12, FR-15 | The UM reviewer sees this (US-09). |
| Extra documents | `Claim.supportingInfo` → `DocumentReference` | PAS | FR-12 | Only if the payer asks for them. |
| Send the request | `POST Claim/$submit` on the payer's PAS endpoint | PAS | FR-11 | One action from the EHR. |

### E. Decision and status (PAS response and EHR)

| EHR data | FHIR element | Used in | FR | Note |
|---|---|---|---|---|
| Response package | `Bundle` with a `ClaimResponse` (PAS Claim Response) | PAS | FR-16 | |
| Which request it answers | `ClaimResponse.request` → `Claim` | PAS | FR-17 | The EHR uses this to attach the decision to the right order. |
| Decision (approved or denied) | `ClaimResponse.item.adjudication` extension `reviewAction`, plus `ClaimResponse.outcome` | PAS | FR-14, FR-16, FR-17 | The review action uses X12 codes. Approved and denied are the two cases modeled here. |
| Authorization number | `ClaimResponse.preAuthRef`, or the item-level authorization number extension | PAS | FR-16, FR-17 | Confirm which element the target payer uses. |
| Approval period | `ClaimResponse.preAuthPeriod` | PAS | FR-17 | |
| Denial reason | `reviewActionReasonCode` extension and `ClaimResponse.disposition` | PAS | FR-19 | Shown to the clinician on a denial. |
| Response received time | EHR receipt time (stored as `AuditEvent.recorded`) | EHR | FR-21 | Used for **T2**. Use the time the EHR received it, not `ClaimResponse.created`, which is the payer's time. |
| Request status in the EHR | Derived: submitted (no response yet), approved, denied | EHR | FR-20 | |
| Audit trail | `AuditEvent` (`agent`, `action`, `recorded`, `entity`) | EHR | NFR-02 | What was sent, when, by whom, and what came back. |

## 3. Requirements with no FHIR mapping

These are behavior in the EHR or the payer, not data in a message.

| Requirement | Why there is no mapping |
|---|---|
| FR-04, FR-05 | EHR rules. They react to the CRD result mapped in section B. |
| FR-10 | EHR rule. It reacts to `QuestionnaireResponse.status`. |
| FR-13 | Out of scope. X12 278 conversion is not mapped. |
| FR-14, FR-15 | Payer-internal decision and review queue. Only the result is mapped (section E). |
| FR-18, FR-19 | EHR notifications to staff and clinician. The data behind them is in section E. |
| NFR-01 | Security setup (secure and authorized connections, SMART on FHIR and OAuth2). |
| NFR-03, NFR-04, NFR-06 | Standards choice, timing, and fallback. These are design rules, not data. |

## 4. Not mapped

- **X12 278.** The to-be swimlane shows the optional X12 278 step for payers that need it. It is not mapped here.
- **Pended responses.** The payer can return an interim "pended" response when it needs more information. It is left out for the same reason as in the requirements page.
- **Appeals.** Out of scope for the project.

## 5. Limits

- This mapping comes from the public guides, not from a working EHR or payer system. No message was tested.
- Element names and profile names should be checked against the exact guide version before anyone builds from this page. Items to check first: the authorization number element, the claim type, and the exact CRD and DTR versions that match PAS 2.1.0.
- HL7 has published newer PAS versions than 2.1.0. This page follows the version chosen in NFR-03.
- Rows marked *(example)* use a typical imaging questionnaire. A real payer's questionnaire will ask for different items.
- Payer-side behavior is an assumption. See [limits-and-risks](../01-scope/limits-and-risks.md). *(Update this path when the folders are final.)*

## Related pages

- [Requirements](requirements.md)
- [User stories](user-stories.md)
- [Traceability](traceability.md)
- [To-be swimlane](../03-to-be/to-be-swimlane.png)

