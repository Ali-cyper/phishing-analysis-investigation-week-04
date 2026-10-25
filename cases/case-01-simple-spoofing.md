# Case 01 — Simple spoofing

| Field | Value |
|---|---|
| Pattern | Simple spoofing; SPF, DKIM and DMARC all failed |
| Verdict | **Phishing** |

## Indicators
- Final domain: `onionquest[.]com` (behind Cloudflare), reached via a `t.co` short link

## What I did right
Compared From with Return-Path, noticed SPF/DKIM/DMARC failures, and wrote a complete response plan.

## What I missed
Expanding the `t.co` link before judging; reading the IP from Authentication-Results.

## Lesson
The link ended at `onionquest[.]com` behind Cloudflare, so the IP reputation I checked was Cloudflare's, not the attacker's.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
