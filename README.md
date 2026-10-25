# Phishing Analysis Investigation — Week 4

> Week 4 of a self-designed 12-week SOC investigation curriculum (Blue Team / SOC Analyst track).
> Hands-on analysis of **11 email samples** (10 real captured attacks + 1 legitimate email for comparison): headers, SPF/DKIM/DMARC, links, attachments, IOCs and verdicts.

🇮🇶 Arabic version: [README.AR.md](README.AR.md)

## Scope

| Item | Value |
|---|---|
| Samples | 11 (.eml) |
| Source | 10 from the public `phishing_pot` repository (attacks captured by honeypots); sample 05 is a clean email created for comparison |
| Attack patterns covered | Credential phishing, compromised account, BEC, malware attachment (ISO / MOTW bypass), quishing (QR), advance-fee (419) fraud |
| Tools used | MXToolbox, VirusTotal, CyberChef, WhereGoes, urlscan.io, AbuseIPDB, whois, crt.sh |

> ⚠️ Samples are real attacks. They were only opened inside an isolated VM. They are **not** included in this repository.

## Method

Every email was analysed with the same fixed workflow ([templates/phishing-analysis-template.md](templates/phishing-analysis-template.md)):

1. **Headers** — From / Return-Path / Reply-To / Message-ID
2. **Auth** — copy `spf` / `dkim` / `dmarc` verbatim before interpreting
3. **Links** — extract, expand, inspect the final domain
4. **Attachments** — mandatory step; no verdict if skipped
5. **IP / Domain** — read the hostname before checking reputation
6. **Verdict** — decision + confidence + specific evidence

Flow of the week: foundation (TryHackMe phishing material + a 9-level guide) → first self-assessment → real samples with a "decision log" (observation, inference, weight, verdict) → three batches of samples (01–05, 06–08, 09–11) → fixed-template consolidation.

## Results

| # | Pattern | Verdict | Case |
|---|---|---|---|
| 01 | Simple spoofing, all auth failed | Phishing | [01](cases/case-01-simple-spoofing.md) |
| 02 | `@` trick, sender domain without a TLD | Phishing | [02](cases/case-02-at-trick.md) |
| 03 | Compromised real school account | Spam / compromised account | [03](cases/case-03-compromised-account.md) |
| 04 | BEC + `.mobileconfig` attachments | BEC | [04](cases/case-04-bec-attachments.md) |
| 05 | Reference email | Legit | [05](cases/case-05-legit.md) |
| 06 | ISO attachment evading Windows check (MOTW) | Malware | [06](cases/case-06-iso-trojan.md) |
| 07 | HTML attachment impersonating a real bank | Phishing | [07](cases/case-07-html-attachment.md) |
| 08 | Fake lawyer via a real global company's infrastructure | Advance-fee (419) | [08](cases/case-08-419-lindt.md) |
| 09 | QR code impersonating a digital wallet | Phishing | [09](cases/case-09-quishing.md) |
| 10 | KYC verification via real telecom infrastructure | Phishing | [10](cases/case-10-kyc.md) |
| 11 | Widow / inheritance via real Gmail | Advance-fee (419) | [11](cases/case-11-widow-inheritance.md) |

## Key takeaways

- A clean IP does not mean a safe email: shared infrastructure (Cloudflare, Microsoft 365, Google) carries the platform's reputation, not the sender's.
- `pass` means the identity is confirmed, **not** that the content is safe.
- The attachment can be the whole attack (case 04).
- Read the raw `Authentication-Results` line, not a summarising website.
- No technical evidence ≠ clean: verdicts for 08, 10 and 11 came from content and context.
- Classify by what the victim is asked to do: run a file (malware), enter data (phishing), reply and pay (419).

Full list: [reference.md](reference.md). Mistakes and fixes: [mistake-log.md](mistake-log.md).

## Repository structure

```
.
├── README.md
├── README.AR.md
├── mistake-log.md
├── reference.md
├── cases/        # one file per sample (01–11)
└── templates/    # fixed analysis workflow
```

## Limitations

This write-up is built only from the end-of-week report. Full hashes, full IP lists, per-case timelines and the original raw prompts were not recorded in it and are therefore **not included** rather than guessed. IOC domains are defanged.
