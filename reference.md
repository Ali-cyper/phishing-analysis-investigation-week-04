# Reference — Phishing Analysis (Week 4)

Built only from lessons recorded in the Week 4 report.

## Authentication

- `pass` = identity confirmed, **not** content safe. A domain owned by the attacker, or a compromised real account, passes SPF/DKIM/DMARC legitimately (cases 03, 08, 09, 10, 11).
- Trust the raw `Authentication-Results` line over any website's summary (case 05).
- `bestguesspass` is weaker than an explicit `pass` (case 10).
- SRS in Return-Path means a relay rewrote the sender address so SPF stays valid (case 08).

## IPs and infrastructure

- A clean IP does not mean safe: Cloudflare (01), Microsoft 365 (03, 08), Google (04, 11) are shared infrastructure; the IP reputation is the platform's. Check the domain.
- Private ranges `10.x.x.x`, `192.168.x.x`, `172.16–31.x.x` are internal and useless for tracing (09).
- A live check on an old domain can mislead (06, dated 2020); use what is written in Received.
- Read the hostname in Received before naming an IP's owner.
- Xserver is independent Japanese hosting, not GoDaddy (07).
- `.sa.com` is an open registration space: anyone can register under it, so the domain was bought by the attacker (10).

## Links and attachments

- Techniques seen: `@` trick, subdomain abuse, quoted-printable-broken links, short links (`t.co`, `420[.]bio`), QR codes.
- Extract links with `grep -o 'href="[^"]*"'` or CyberChef; expand short links safely (WhereGoes).
- Hash the **attachment**, not the whole `.eml`; uploading the full email leaks information.
- VirusTotal: *Execution Parents* (files that contain yours) vs *Contained Files* (files inside yours) are opposite directions.
- ISO files avoided Mark-of-the-Web before Microsoft's Nov 2022 update; tie attack effectiveness to the incident date.
- Legitimate services are abused to look clean: Netlify scripts (07), Google Cloud Run (02).
- Sandbox-evasion tags: `long-sleeps`, `checks-user-input` (06).

## Classification

| Victim is asked to | Type |
|---|---|
| Run a file | Malware |
| Enter data | Phishing |
| Reply and pay | Advance-fee (419) |

Absence of technical evidence ≠ clean: verdicts for 08, 10, 11 came from content and context.

## Response actions by type

- **419:** block the Reply-To; report the abused company.
- **BEC:** verify through a second channel.
- **Malware:** isolate the host; use EDR.
- **Credential phishing:** reset the password; revoke sessions.
- When a real company's infrastructure is abused (`moss[.]it`, `lindt[.]net`, `tpg[.]com[.]au`), do not block the whole domain; notify the company's security team.

## Tools

| Tool | Use |
|---|---|
| MXToolbox | header analysis |
| VirusTotal | files and URLs |
| CyberChef | base64 / quoted-printable decoding |
| WhereGoes | expand short links |
| urlscan.io | safe page inspection |
| AbuseIPDB | IP reputation |
| whois | domain age and ownership |
| crt.sh | TLS certificates |
