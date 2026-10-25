# Case 08 — 419 via Lindt

| Field | Value |
|---|---|
| Pattern | Fake lawyer, sent through a real global company's infrastructure |
| Verdict | **Advance-fee (419)** |

## Indicators
- Abused company domain: `lindt[.]net` (real Swiss company)
- Infrastructure: Microsoft 365
- Return-Path shows SRS (relay rewrote the sender address to keep SPF valid)

## What I did right
Noticed the odd Return-Path and Reply-To and understood the content was a scam.

## What I missed
Said Google while the Received header says Microsoft; stopped at the first hop and missed `lindt[.]net`; wrote "I don't know" in the response step.

## Lesson
Read the whole Received chain bottom-to-top in one pass. Response for 419: block the Reply-To and report the abused company.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
