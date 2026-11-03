This is a design-level study. It is not tested in a real EHR or with a real payer.
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
| `03-to-be` | Future-state swimlane with ePA, to-be KPI targets | Done |
| `04-requirements` | Stakeholders, requirements, user stories, FHIR data mapping, traceability | To review |

## A note on the numbers

This is a self-directed portfolio project. I did not work with a real clinic or real patient data. The as-is flow is built from public sources and general knowledge. The baseline numbers are reference estimates from published sources (listed in `01-scope/sources.md`), not measurements. The to-be numbers are targets, not results. ePA should reduce manual work, not remove it. Some requests will always need clinical review.

----------------------------------------------------------------------------------------------------------
## About this project

I built this project to apply what I learned in healthcare IT courses (EHR and FHIR) to a real business problem in healthcare workflow: prior authorization for an outpatient MRI order. It compares the manual process today with an automated process using HL7 Da Vinci.

## How I used AI tools

I used AI tools (Claude and Gemini) to help research and draft the documents in this repo. This is part of how I practice business analysis work with AI. I chose the use case, the scope, and the structure. I reviewed the drafts and checked part of the FHIR mapping against the HL7 guides. Some parts are not checked yet, and each folder lists its limits. The numbers come from published sources, not from a real clinic.

## What I learned

- How prior authorization works today, step by step, and where time and staff effort go
- How the automated process works with Da Vinci (CRD, DTR, and PAS), and which steps it changes
- The outpatient journey from order to scheduling, and who does what: patient, clinician, clinic staff, EHR, and payer
- How to build as-is and to-be swimlane diagrams
- How to pick KPIs, find baseline values from published sources, and say "no data" when there is none
- How to write requirements and user stories, and trace each one from pain point to KPI
- How to explore FHIR artifacts: reading Da Vinci guides, profiles, and extensions, and mapping order, coverage, questionnaire, and claim data to FHIR resources
- How to use AI tools for research and drafting while checking the output against the sources
