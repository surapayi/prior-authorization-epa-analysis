# Limits and Risks

This page lists what the project does not cover and what could weaken its conclusions. It sits with the scope statement because it describes the project's boundaries.

## Limits

**Use case**
- One use case only: an outpatient MRI order, where the payer makes the decision.
- Out of scope: appeals, peer-to-peer reviews, pharmacy/drug PA, and emergency orders.
- The appeal step appears in the as-is swimlane to show real practice, but it is not measured.
- Patient notification on the denial path is left out of both swimlanes to keep them readable.

**Evidence**
- I have no access to a real clinic. The as-is flow is built from public sources and has not been checked by clinic staff or clinicians.
- Baseline KPIs come from published sources (listed in the metrics folder). I used Washington-specific values where I could find them. Where I couldn't, the source is noted.
- The ePA (to-be) values are projections, not measurements. Each one is labeled as projected, with its assumption.

**Metrics**
- Turnaround time runs from order created (T0) to final determination received in the EHR (T2). Submission (T1) splits it into prep and payer wait.
- Operational cost per PA covers the healthcare organization only. Payer processing cost is excluded.
- Clinic staff effort excludes idle waiting time.
- Denial rate is not used as a KPI.
- Orders that don't need PA, or where coverage isn't active, never reach T1 or T2. They fall outside the turnaround measure.

**Technical**
- The Da Vinci flow (CRD, DTR, PAS) is shown at workflow level. It is not a full implementation guide conformance check.
- The FHIR to X12 278 conversion step is shown as optional and payer-internal.

## Risks

| Risk | Why it matters | How I handle it |
|---|---|---|
| Baselines don't match a real clinic | Published figures are averages and may differ by clinic, payer, and region | Show sources next to every value, prefer Washington data, treat results as reference points, not findings |
| Projected ePA values are estimates | Readers could mistake them for measured results | Label them as projected and state the assumption behind each one |
| Payer rules vary | PA requirements differ by payer and by imaging type, so one flow may not fit all | Keep to one use case and say so in the scope statement |
| Payers may not support Da Vinci APIs | Many payers still use portals, fax, or X12 | State as an assumption that the payer supports CRD, DTR, and PAS |
| Misreading the Da Vinci guides | The guides are complex and I am working at workflow level | Keep detail low, check resources against the guides, and list open questions in the requirements folder |
| Scope creep | Adding appeals, drug PA, or patient notification would blur the comparison | Keep the out-of-scope list fixed unless a later version says otherwise |
