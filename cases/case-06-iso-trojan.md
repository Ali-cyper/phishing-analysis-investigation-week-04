# Case 06 — ISO attachment (Trojan)

| Field | Value |
|---|---|
| Pattern | ISO attachment bypassing Mark-of-the-Web |
| Verdict | **Malware** |

## Indicators
- Abused company domain: `moss[.]it` (small real Italian company)
- Attachment detection: 40/61 on VirusTotal, labelled Trojan
- Sandbox tags: `long-sleeps`, `checks-user-input` (sandbox evasion)
- Email dated 2020; a live check of the domain returns a different IP than at send time, so use the Received header

## What I did right
Spotted Paolo vs Paol, matching Return-Path, no links, and suspected the long base64 body.

## What I missed
Said SPF pass when it was not in the line; took a second IP from a live check; uploaded the whole email to VirusTotal; attachment extraction took 3 attempts.

## Lesson
ISO files avoided the Mark-of-the-Web on machines before Nov 2022, bypassing SmartScreen. I also labelled this phishing; it is malware (the victim is asked to run a file).

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
