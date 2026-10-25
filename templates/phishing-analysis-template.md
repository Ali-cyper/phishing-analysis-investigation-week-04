# Phishing Analysis Template

Fixed order — do not change it, apply it to every email.

## 1. Headers
- From:
- Return-Path:
- Reply-To:
- Message-ID:
- Why do they differ?

## 2. Authentication
Copy verbatim before interpreting:
```
spf=
dkim=
dmarc=
```
Interpretation (pass = identity confirmed, not content safe):

## 3. Links
- Extracted (`grep -o 'href="[^"]*"'` / CyberChef):
- Expanded / final domain:

## 4. Attachments (mandatory — no verdict if left empty)
- Name / type:
- Hash (of the attachment, not the .eml):
- Result:

## 5. IP / Domain
- Hostname in Received (read before checking reputation):
- Owner confirmed by (whois / hostname):
- Shared infrastructure? (reputation = platform's)

## 6. Verdict
- Verdict:
- Confidence:
- Specific evidence:
- Type check: run a file = malware / enter data = phishing / reply and pay = 419
- Response action:

## IOCs (defanged)
- Domains:
- URLs:
- Hashes:
