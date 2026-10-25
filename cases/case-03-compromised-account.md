# Case 03 — Compromised real account

| Field | Value |
|---|---|
| Pattern | Real school account compromised and used to send spam |
| Verdict | **Spam / compromised account** |

## Indicators
- Sender infrastructure: shared Microsoft IP (not attacker-owned)
- Link contains tracking for a fake health product (link was hidden in heavy HTML)

## What I did right
Noticed the different Reply-To and concluded the account was compromised, not spoofed.

## What I missed
Understood DMARC alignment backwards; did not find the link hidden in heavy HTML.

## Lesson
`dmarc=pass` because SPF aligned with the From domain, and the IP belongs to shared Microsoft infrastructure.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
