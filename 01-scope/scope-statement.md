# Scope Statement

**Project:** Streamlining Prior Authorization for Outpatient MRI Orders

## Problem

Before an outpatient MRI, the clinic often has to get prior authorization (PA) from the patient's health plan. The process is mostly manual, so patients wait longer for care and staff spend hours on paperwork.

## Use case and setting

- **Use case:** One outpatient MRI order.
- **Setting:** An outpatient clinic places the order. The payer reviews it and decides.
- **Why MRI:** Advanced imaging is a common PA request. In Washington's annual prior authorization report, MRI codes are among the most requested services.

## Main question

How much could automated ePrior Authorization (ePA), using FHIR standards, reduce:

1. the time from order creation to payer response, and
2. the clinic's staff effort and cost per PA?

## Time markers

- **T0:** order created in the EHR
- **T1:** request submitted to the payer
- **T2:** response received by the clinic

## Measures (KPIs)

| KPI | Definition | Formula |
|---|---|---|
| Turnaround time | Calendar time from order created to response received. Includes the payer's wait. | T2 − T0 |
| Clinic staff effort per PA | Active staff minutes on the Clinic staff lane steps. Waiting time is not counted. | Prep and submission minutes + (follow-up attempts × minutes per attempt) + minutes to log the decision |
| Cost per PA (clinic side) | Cost of that staff effort. | Staff effort minutes ÷ 60 × hourly labor rate |
| First-pass rate (optional) | Share of PA requests the payer accepts as complete on the first submission, with no return for missing information. | Requests accepted on the first try ÷ all requests |

## Out of scope

- Appeals and peer-to-peer reviews (shown in the swimlane as an end point only)
- Pharmacy and drug PA
- Emergency orders

## Why now

CMS's Interoperability and Prior Authorization final rule (CMS-0057-F) set faster decision timeframes for covered payers starting in 2026: 72 hours for expedited requests and 7 calendar days for standard ones. It also requires FHIR-based prior authorization APIs by 2027. As I understand it, the rule applies to certain government-program plans, such as Medicare Advantage, Medicaid, and CHIP, and covers medical items and services, not drugs. See [sources](sources.md).

## Planned future state

Automated ePA using HL7 FHIR, with the Da Vinci implementation guides:

- **CRD** (Coverage Requirements Discovery): does this order need PA for this patient's plan?
- **DTR** (Documentation Templates and Rules): what information does the payer need?
- **PAS** (Prior Authorization Support): submit the request and get the answer back.

The future-state design will be in `03-to-be`.

## Assumptions and limits

- No real clinic data. The as-is flow is built from public sources and general knowledge.
- Baseline values are reference estimates from published sources, not measured.
- Washington-based inputs are used where data exists (payer decision time, labor cost). National figures are shown as a cross-check.
- ePA reduces manual work but does not remove the need for clinical review on some requests.
- Payer behavior varies by plan and payer type.
