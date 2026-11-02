# User Stories

**Project:** Streamlining Prior Authorization (outpatient MRI order, automated ePA with HL7 Da Vinci)
**Status:** Draft

Each story describes what one person needs from the to-be process and why. Acceptance criteria say how to check that the story is done. Each story points to the requirements (FR-xx), pain points (PP-xx), and stakeholder (SH-xx) it relates to.

## Story format

> As a *[who]*, I want *[what]*, so that *[why]*.

Acceptance criteria use Given / When / Then.

## Stories

### US-01 See the coverage and PA result when signing an order

As a **clinician**, I want to see right away whether the patient's coverage is active and whether PA is required, so that I know what will happen to the order before I leave the screen.

**Acceptance criteria**
- Given I sign an MRI order, when the payer's CRD service responds, then the result appears as a card in the order screen.
- Given PA is not required, when I look at the card, then it says so and the order can go on to scheduling without PA steps.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-01, FR-02, FR-03, FR-04 | PP-01 | SH-02 | Must |

### US-02 Be told when coverage is not active

As **clinic staff**, I want to be flagged when the patient's coverage is not active, so that I can sort out coverage with the patient before anything else is done.

**Acceptance criteria**
- Given the CRD result shows coverage is not active, when the check finishes, then the order is flagged to clinic staff.
- Given the order is flagged, when I open it, then I can see the reason.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-05 | PP-01 | SH-03 | Must |

### US-03 Start with a pre-filled questionnaire

As **clinic staff**, I want the payer's questionnaire to open already filled in from the EHR, so that I review answers instead of typing them again.

**Acceptance criteria**
- Given PA is required, when I click the link on the CRD card, then the DTR app opens inside my EHR workflow.
- Given the questionnaire opens, when it loads, then the answers available in the EHR are already filled in.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-06, FR-07, FR-08 | PP-02, PP-03 | SH-03 | Must |

### US-04 Find missing information before submitting

As **clinic staff**, I want to see which required answers are missing before I submit, so that the request does not come back to me later for rework.

**Acceptance criteria**
- Given the questionnaire has required answers that are empty, when I review it, then those answers are clearly shown.
- Given required answers are still missing, when I try to submit, then the EHR does not let me.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-09, FR-10 | PP-04 | SH-03 | Must |

### US-05 Submit with one action

As **clinic staff**, I want to submit the request from the EHR in one step, so that I do not have to use a separate payer portal, fax, or form.

**Acceptance criteria**
- Given the questionnaire is complete, when I click submit in the EHR, then the request is sent to the payer's PAS without extra data entry.
- Given the request is sent, when I look at the order, then it shows the request was submitted.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-11, FR-12 | PP-03 | SH-03 | Must |

### US-06 Get an approval without retyping it

As **clinic staff**, I want an approval to appear on the order with its authorization number and to be told about it, so that I can contact the patient to schedule without typing anything in.

**Acceptance criteria**
- Given the payer approves the request, when the EHR receives the response, then the decision and authorization number are attached to the order.
- Given the order has been updated, when the approval arrives, then I am notified so I can contact the patient.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-17, FR-18 | PP-06, PP-07 | SH-03 | Must |

### US-07 Hear about a denial and decide next steps

As a **clinician**, I want to be told when a request is denied, so that I can decide whether to modify or cancel the order.

**Acceptance criteria**
- Given the payer denies the request, when the EHR receives the response, then I am notified.
- Given I open the notification, when I review it, then I can choose to modify or cancel the order. *(Appeal is out of scope.)*

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-19 | None (from swimlane) | SH-02 | Must |

### US-08 Check status without calling the payer

As **clinic staff**, I want to see the current status of each request in the EHR, so that I do not need to call or check a portal.

**Acceptance criteria**
- Given a request has been submitted, when I open the order, then I can see whether it is waiting, approved, or denied.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-20 | PP-05 | SH-03 | Should |

### US-09 Receive a complete case to review

As a **payer UM reviewer**, I want requests that need review to arrive with the completed questionnaire and supporting data, so that I can decide without asking the clinic for more.

**Acceptance criteria**
- Given a request cannot be approved automatically, when it is queued for me, then it includes the completed questionnaire and the data sent with the request.

| Requirements | Pain point | Stakeholder | Priority |
|---|---|---|---|
| FR-12, FR-15 | PP-04 | SH-06 | Must |

## Story coverage

| Story | Requirements covered |
|---|---|
| US-01 | FR-01, FR-02, FR-03, FR-04 |
| US-02 | FR-05 |
| US-03 | FR-06, FR-07, FR-08 |
| US-04 | FR-09, FR-10 |
| US-05 | FR-11, FR-12 |
| US-06 | FR-17, FR-18 |
| US-07 | FR-19 |
| US-08 | FR-20 |
| US-09 | FR-12, FR-15 |

**Not covered by a story:** FR-13 (X12 278 conversion), FR-14 (automatic approval), FR-16 (payer returns the ClaimResponse), FR-21 (timestamps), and the NFRs. These are technical, payer-side, or measurement items, and they don't have a user who would ask for them directly.
## Notes

- Priorities and acceptance criteria are my own draft. They have not been checked with real users.
- Payer-side behavior is an assumption. See [limits-and-risks](../01-scope/limits-and-risks.md).
