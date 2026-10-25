# Case 09 — Quishing

| Field | Value |
|---|---|
| Pattern | QR code impersonating a digital wallet |
| Verdict | **Phishing** |

## Indicators
- Short link: `420[.]bio`
- `10.10.49.81` is a private (internal) IP — not an IOC

## What I did right
Found the short link `420[.]bio` and checked the sender reputation.

## What I missed
Treated `10.10.49.81` as an important IP though it is internal; did not mention the QR code.

## Lesson
A QR code moves the victim to a personal phone outside corporate protection. Private ranges (10.x, 192.168.x, 172.16–31.x) are useless for tracing.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
