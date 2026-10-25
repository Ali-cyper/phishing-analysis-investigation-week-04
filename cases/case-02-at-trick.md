# Case 02 — The @ trick

| Field | Value |
|---|---|
| Pattern | URL obfuscation with `@`; sender domain with no TLD |
| Verdict | **Phishing** |

## Indicators
- Real destination: `run[.]app` (Google Cloud Run)

## What I did right
Noticed the name/domain mismatch and found the href myself.

## What I missed
The sender domain had no TLD at all (random text); the link was broken by quoted-printable encoding.

## Lesson
Everything before `@` in a URL is fake; the real destination is what follows.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
