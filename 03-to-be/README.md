# 03 To-Be: Automated PA with HL7 Da Vinci

This folder describes the future process for an outpatient MRI prior authorization (PA) when the clinic uses the HL7 Da Vinci FHIR implementation guides: CRD, DTR, and PAS.

It answers one question: **what changes in the workflow, and which KPIs should improve, compared with the manual as-is process?**

## Files

| File | What it contains |
|---|---|
| [to-be-swimlane.png](to-be-swimlane.png) | Swimlane diagram of the automated PA workflow |
| [to-be-kpis.md](to-be-kpis.md) | To-be KPI values, compared against the [as-is baseline](../02-as-is/as-is-baseline.md) |

## Scope

Same scope as the as-is process (see the [scope statement](../01-scope/scope-statement.md)):

- Use case: outpatient MRI order
- Setting: outpatient clinic orders, payer decides
- Out of scope: appeals, peer-to-peer reviews, pharmacy/drug PA, emergency orders

The appeal box stays in the diagram only to show what happens after a denial. It is not measured.

## How the workflow runs

The diagram has six lanes: Patient, Clinician, Clinic Staff, EHR, Da Vinci apps (provider side and payer side), and Payer. It has four phases.

| Phase | What happens |
|---|---|
| **Clinical initiation and verification** | The clinician places the MRI order. A CDS hook in the EHR calls the payer's CRD service. CRD checks whether coverage is active and whether PA is required. If there is no active coverage, staff resolve it with the patient. If PA is not required, staff contact the patient. |
| **Documentation gathering** | If PA is required, the EHR shows a CRD card with a DTR link. Staff click it and launch the DTR app. DTR scans the EHR and auto-populates a questionnaire. Staff review it and fill in missing information. |
| **Submission** | Staff click submit in the EHR. The client PAS builds a FHIR Claim bundle and sends it to the payer PAS. If the payer still uses X12, the bundle is translated to a 278 transaction. |
| **Final determination and next steps** | The payer PAS checks the request against its rules. If it meets the criteria, an authorization number is issued automatically. If not, it goes to an RN or medical director for review. The EHR receives a ClaimResponse. If approved, staff contact the patient and the patient schedules the MRI. If denied, the clinician decides next steps (modify or cancel the order, or appeal, which is out of scope). |

## Measurement points

I use the same three time points as the as-is process, so the KPIs compare directly.

| Point | Event |
|---|---|
| **T0** | Order created |
| **T1** | Request submitted to the payer |
| **T2** | Response received |

- **Prep and submission** = T0 to T1
- **Payer wait** = T1 to T2
- **Turnaround time** = T0 to T2

## What changes from as-is

- **Coverage and PA-required checks happen inside the EHR** at order entry. Staff no longer look them up on a payer portal or by phone.
- **Documentation is auto-populated from the EHR.** Staff review and fill gaps instead of building the packet by hand.
- **Submission is one click.** The request is sent electronically as a FHIR bundle.
- **Some requests are approved automatically.** Only requests that do not meet the criteria go to manual payer review.
- **The payer response returns directly to the EHR.** Staff do not need to follow up repeatedly.

The clinician and the patient steps stay the same. The change is mainly in clinic staff work and in payer wait time.

## KPIs

The same KPIs from the scope statement are used here. See [to-be-kpis.md](to-be-kpis.md).

## Limits

- This is a modeled future state, not a measurement from a real clinic.
- To-be values will be estimates from published sources and stated assumptions. They are not observed results.
- Real results would depend on the payer supporting Da Vinci, the EHR vendor's integration, and the clinic's setup.
