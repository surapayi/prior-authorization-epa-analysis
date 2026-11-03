# To-Be KPIs

Reference values for the automated PA process (HL7 Da Vinci CRD, DTR, and PAS). These are published estimates, not measurements from a real clinic. KPI definitions and formulas are in the [scope statement](../01-scope/scope-statement.md). The as-is values are in [as-is-baseline.md](../02-as-is/as-is-baseline.md).

| KPI | Washington-based (main) | National (cross-check) | Notes |
|---|---|---|---|
| Turnaround time (T0 to T2) | About 26 hours (pilot figure) | About 26 hours (pilot figure) | 1 |
| Clinic staff effort per PA | About 12 min | About 12 min | 2 |
| Cost per PA (clinic side) | $28.20/hr × 12 min = **$5.64** | $22.50/hr × 12 min = **$4.50** | 3 |

## Change from as-is

| KPI | As-is | To-be | Change |
|---|---|---|---|
| Turnaround time (T0 to T2) | No data | About 26 hours | Cannot calculate |
| Clinic staff effort per PA | About 26 min | About 12 min | About 14 min less (54%) |
| Cost per PA, Washington | $12.22 | $5.64 | $6.58 less |
| Cost per PA, national | $9.75 | $4.50 | $5.25 less |

## Notes

1. **Turnaround.** The only published Da Vinci figure I found is from a Humana, athenahealth, and Availity pilot. From October to December 2023, the average time for a request to reach approval or denial was 26 hours. This is a vendor-published case study with one payer and one EHR, and about 70% of requests were auto-approved. The source does not say whether the clock starts at order creation, so it may be closer to T1 to T2 than T0 to T2. It is not specific to Washington, so both columns show the same value. The as-is has no baseline, so I do not calculate a change. For context, CMS-0057-F sets decision deadlines of 72 hours (expedited) and 7 days (standard) for covered payers. These are payer deadlines, not a baseline for T2 − T0.
2. **Staff minutes.** The 12 minutes is the average that specialists reported for a fully electronic PA in the 2023 CAQH Index (11.90 min, 2022 data). "Fully electronic" in CAQH means the HIPAA standard X12 278 transaction, not Da Vinci specifically. I use it as a stand-in because no published source measures Da Vinci staff time per PA. Da Vinci could be faster because DTR auto-populates the form, but staff still review and complete it. CAQH says its figures cover the time to conduct the transaction, not gathering information or follow-up. This is the same source and definition as the as-is 26 minutes, so the two are comparable.
3. **Wages.** Same wages and same role assumption as the as-is baseline. Washington: mean of $28.20/hr (Washington ESD, OEWS, May 2025). National: mean of $22.50/hr (BLS OEWS, May 2025). Wages exclude benefits. The formula is wage × minutes ÷ 60, with 12 min.

## Sources for these values

| Value | Source | Link |
|---|---|---|
| Staff minutes (12) and CAQH cost ($6.61) | CAQH Index 2023, Administrative Transaction Costs by Provider Specialty | [caqh.org](https://www.caqh.org/hubfs/CAQH%20Insights_2023%20Index%20Report_Provider%20Specialty%20Issue%20Brief_Final.pdf) |
| Turnaround time (26 hours) | Availity case study: End-to-End Prior Authorizations Using FHIR APIs (Humana, athenahealth, Availity pilot) | [availity.com](https://www.availity.com/case-studies/end-to-end-prior-authorizations-using-fhir-apis/) |
| Washington wage | Washington State Employment Security Department, OEWS (May 2025) | [esd.wa.gov](https://esd.wa.gov/jobs-and-training/labor-market-information/employment-and-wages/occupational-employment-and-wage-statistics-oews) |
| National wage | U.S. Bureau of Labor Statistics, OEWS (May 2025) | [bls.gov](https://data.bls.gov/oes/#/area/0000000/2025) |
| 72-hour and 7-day decision timeframes (context only) | CMS Interoperability and Prior Authorization final rule (CMS-0057-F) | [cms.gov](https://www.cms.gov/newsroom/fact-sheets/cms-interoperability-prior-authorization-final-rule-cms-0057-f) |

Full references for the whole project are in [sources.md](../01-scope/sources.md).
