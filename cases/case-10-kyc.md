# Case 10 — Fake KYC verification

| Field | Value |
|---|---|
| Pattern | KYC verification sent via real telecom infrastructure |
| Verdict | **Phishing** |

## Indicators
- Attacker-registered domain: `xvx3[.]sa[.]com`
- Abused company: `tpg[.]com[.]au` (private Australian telecom)

## What I did right
Decoded the attachment and confirmed it was clean; inspected the link.

## What I missed
Considered TPG a government body (it is a private telecom).

## Lesson
`.sa.com` is an open registration space, so the domain was bought by the attacker, not a compromised company. `bestguesspass` is weaker than an explicit pass. In the report, do not block a real company's whole domain; notify its security team.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
