# Case 11 — Widow and inheritance

| Field | Value |
|---|---|
| Pattern | Advance-fee scam from a real Gmail account |
| Verdict | **Advance-fee (419)** |

## Indicators
- Sender: real Gmail account (auth fully passed)

## What I did right
Identified Google correctly, noticed the different Return-Path and understood it was a scam. SPF/DKIM/DMARC read correctly on the first try.

## What I missed
Precise naming: advance-fee fraud rather than generic phishing.

## Lesson
Authentication was full pass because the sender is a real Gmail account: the fraud is in the story, not the technique.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
