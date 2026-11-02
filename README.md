# Streamlining Prior Authorization: Outpatient MRI Orders

![As-is swimlane: manual prior authorization for an outpatient MRI](02-as-is/as-is-swimlane.png)

**Status:** In progress. The scope, as-is process, pain points, baseline KPIs, and to-be swimlane are done. The to-be KPI targets, requirements, and FHIR data mapping are next.

**Author:** Surapa Yi

## The problem

Before an outpatient MRI, the clinic often needs prior authorization (PA) from the patient's health plan. The process is mostly manual. Staff look up the rules, build a packet, submit it by portal or fax, and keep following up until a decision comes back. This delays care and uses a lot of staff time.

## What this project looks at

One use case: an outpatient MRI order placed at a clinic, with the health plan (payer) making the decision.

**Main question:**

> How much could automated ePrior Authorization (ePA), using FHIR standards, reduce (1) the time from order creation to payer response, and (2) the clinic's staff effort and cost per PA?

## How to read this repo

Start with the scope, then follow the story: how PA works today, how it could work with ePA, and what a system would need to do.

| Folder | What's inside | Status |
|---|---|---|
| `01-scope` | Scope statement and KPI definitions, limits and risks, sources | Done |
| `02-as-is` | Current-state swimlane, pain points, baseline KPI values | Done |
| `03-to-be` | Future-state swimlane with ePA, to-be KPI targets | In progress |
| `04-requirements` | Stakeholders, requirements, user stories, FHIR data mapping, traceability | In progress |

## A note on the numbers

This is a self-directed portfolio project. I did not work with a real clinic or real patient data. The as-is flow is built from public sources and general knowledge. The baseline numbers are reference estimates from published sources (listed in `01-scope/sources.md`), not measurements. The to-be numbers are targets, not results. ePA should reduce manual work, not remove it. Some requests will always need clinical review.
