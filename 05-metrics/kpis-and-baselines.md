# KPIs and As-Is Baselines

All values are **reference estimates from published sources**, not measured at a clinic. Sources and limits are in [sources](../01-scope/sources.md).

## Time markers

- **T0:** order created in the EHR
- **T1:** request submitted to the payer
- **T2:** response received by the clinic

## KPI definitions

| KPI | Definition | Formula |
|---|---|---|
| Turnaround time | Calendar time from order created to response received. Includes the payer's wait. | T2 − T0 |
| Clinic staff effort per PA | Active staff minutes on the Clinic staff lane steps. Waiting time is not counted. | Prep and submission minutes + (follow-up attempts × minutes per attempt) + minutes to log the decision |
| Cost per PA (clinic side) | Cost of that staff effort. | Staff effort minutes ÷ 60 × hourly labor rate |
| First-pass rate (optional) | Share of PA requests the payer accepts as complete on the first submission, with no return for missing information. | Requests accepted on the first try ÷ all requests |

## As-is values

| KPI | Washington / Seattle-area (main) | Nationwide (cross-check) | Notes |
|---|---|---|---|
| Payer decision time (the payer part of T1 to T2) | 8.3 hours, standard requests, outpatient medical/surgical, commercial plans, plan year 2024. For MRI only, filter the WA open data by MRI CPT codes. | No national MRI figure. Aetna Medicare Advantage: mean ~0.9 to 3.1 days, median 0 to 1 day. AMA 2018 survey: 65% of physicians wait at least 1 business day, 26% at least 3, 7% more than 5. | 1, 2 |
| Turnaround time (T0 to T2) | No published figure | No published figure | 3 |
| Clinic staff effort per PA | Base ~20 min. High ~26 min. | Base ~20 min. High ~26 min. | 4 |
| Cost per PA (clinic side) | $29.01 per hour. 20 min → **$9.67**. 26 min → **$12.57**. | $22.08 per hour. 20 min → **$7.36**. 26 min → **$9.57**. | 5 |
| Cost cross-check | Same as national | CAQH 2023: $10.97 average per manual PA, $15.12 for specialists | 6 |
| First-pass rate | No reliable baseline | No reliable baseline | 7 |
| Follow-up attempts per PA | No source | No source | 7 |

## Worked example (Seattle-area wage, 20 minutes)

20 minutes ÷ 60 × $29.01 per hour = **$9.67 per PA** (wage only, before any benefits load).

## Notes

1. **Washington data:** commercial fully insured plans only. Carriers report top codes, so MRI may be missing for some. If a carrier tracks days instead of hours, it may report one day as 24 hours and a same-day decision as 8 hours, so treat hours as approximate.
2. **Aetna and AMA numbers:** the Aetna report is Medicare Advantage only, by contract number, with no state label and no MRI split. It reports days, not hours, so don't compare it directly with the Washington figure. The AMA wait-time figures are from 2018. Check the 2025 survey for an update. For a benchmark, the CMS rule sets 7 calendar days for standard decisions for covered payers.
3. **Turnaround:** only the payer part is sourced. Prep time and the delay before staff see the response are assumptions. An idea to test, not a finding: payer decision time looks short (hours to a couple of days), so much of turnaround may sit on the clinic side.
4. **Staff minutes:** the AMA 2025 survey reports 40 PAs per physician per week using 13 hours of physician and staff time. The ~20 minutes is my own division (13 × 60 ÷ 40 ≈ 19.5). It mixes physician and staff time and all PA types, including drugs, so it is a rough reference. The ~26 minutes is the CAQH Index 2023 figure for specialists.
5. **Wages:** BLS OEWS median for medical secretaries and administrative assistants. Seattle-Tacoma-Bellevue about $60,350 per year, US about $45,930 per year, each divided by 2,080 hours. Figures were taken from secondary sites, so confirm on bls.gov. Wages exclude benefits. If you add a benefits load, state the percentage.
6. **CAQH costs:** national, provider-side cost per manual transaction, using CAQH's own definition. They will not match the minutes × wage formula exactly.
7. **Assumptions:** label these clearly and show a low, base, and high case.

## Before publishing

- Confirm the wage figures on bls.gov/oes.
- Confirm the $10.97 CAQH figure in the CAQH Index report.
- Confirm the AMA 2025 figures on the AMA page.
- Open every link in the sources file.
