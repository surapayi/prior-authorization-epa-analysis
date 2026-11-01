# Scope Statement

**Project:** Streamlining Prior Authorization for Outpatient MRI Orders

## Problem

Before an outpatient MRI, the clinic often has to get prior authorization (PA) from the patient's health plan. The process is mostly manual, so patients wait longer for care and staff spend hours on paperwork.

## Use case and setting

- **Use case:** One outpatient MRI order.
- **Setting:** An outpatient clinic places the order. The payer reviews it and decides.
- **Why MRI?:** Advanced imaging is a common PA request. In Washington's annual prior authorization report, MRI codes are among the most requested services.

## Main question

How much could automated ePrior Authorization (ePA), using FHIR standards, reduce:

1. the time from order creation to payer response, and
2. the clinic's staff effort and cost per PA?

## Time markers

- **T0:** Order created in the EHR
- **T1:** Request submitted to the payer
- **T2:** Response received by the payer

## Measures (KPIs)

Full definitions, formulas, and as-is values are in [kpis-and-baselines](../05-metrics/kpis-and-baselines.md).

- **Turnaround time:** T0 to T2
- **Clinic staff effort per PA:** active staff minutes only. Waiting time is not counted.
- **Cost per PA (clinic side):** staff minutes × hourly labor rate
- **First-pass rate (optional):** share of requests accepted as complete on the first submission

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
