# 02 As-Is: Manual Prior Authorization for an Outpatient MRI

This folder shows how prior authorization (PA) works today for an outpatient MRI, where the process loses time and staff effort, and what the baseline looks like in numbers.

It answers one question: **how long does a manual PA take, and what does it cost the clinic?**

## Files

| File | What it contains |
|---|---|
| [as-is-swimlane.png](as-is-swimlane.png) | Swimlane diagram of the manual PA workflow |
| [pain-points.md](pain-points.md) | Where the process loses time and staff effort |
| [as-is-baseline.md](as-is-baseline.md) | Baseline KPI values, with sources and calculations |

Suggested reading order: swimlane, then pain points, then baseline.

## Scope

See the [scope statement](../01-scope/scope-statement.md).

- Use case: outpatient MRI order
- Setting: outpatient clinic orders, payer decides
- Out of scope: appeals, peer-to-peer reviews, pharmacy/drug PA, emergency orders

The appeal step is shown as a dashed box. It is not measured, but I kept it to show what happens in real practice.

## How the workflow runs

The diagram has four lanes: Patient, Clinician, Clinic Staff, and Payer. It has five phases.

| Phase | What happens |
|---|---|
| **Clinical initiation** | The patient visits the clinic. The clinician creates the MRI order in the EHR. |
| **Administrative triage and preparation** | Staff check whether the patient has active coverage. If not, the clinician resolves it with the patient. Staff then check whether PA is required. If not, staff contact the patient. If yes, staff assemble the packet from the EHR. |
| **Manual submission** | Staff enter the details on the payer's portal and upload documents, or send them by fax. They log the PA reference number and submission date in the EHR. |
| **Payer review** | The payer screens the submission for completeness. If it is incomplete, it goes back to staff to fix and resubmit. If it is complete, an RN or physician does a clinical review for medical necessity. Meanwhile, staff follow up with the payer until a response arrives. |
| **Final determination and next step** | If approved, the payer issues an authorization number. Staff log it in the EHR and billing system, contact the patient, and the patient schedules the MRI. If denied, the payer sends a denial letter. The clinician decides next steps: modify or cancel the order, or appeal (out of scope). |

Orange boxes in the diagram are staff effort. These steps are counted in the clinic staff effort KPI. Waiting time is not counted as effort.

## Measurement points

| Point | Event |
|---|---|
| **T0** | Order created |
| **T1** | Request submitted to the payer |
| **T2** | Response received |

- **Prep and submission** = T0 to T1
- **Payer wait** = T1 to T2 (the clinic follows up during this time)
- **Turnaround time** = T0 to T2

The [to-be process](../03-to-be/) uses the same three points, so the KPIs compare directly.

## Where the process breaks

The main problems are in [pain-points.md](pain-points.md). In short, they come from manual data entry and repeated follow-up. They show up as long turnaround time and high clinic staff effort.

## KPIs

KPI definitions are in the [scope statement](../01-scope/scope-statement.md). The baseline values and their sources are in [as-is-baseline.md](as-is-baseline.md).

## How this was built

- The flow comes from public sources and general knowledge. It has not been checked by clinic staff or clinicians.
- The baseline values are reference estimates from published sources, not measurements from a real clinic.
- Where I could not find a reliable source, the baseline says "no data" instead of filling the gap.

## Next

The future-state design is in [03-to-be](../03-to-be/).
