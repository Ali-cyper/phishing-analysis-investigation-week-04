# Mistake Log — Week 4

Source: end-of-week report. Each row is a mistake made during the week and the correction.

## Per case

| # | Mistake | Correction |
|---|---|---|
| 01 | Did not expand the `t.co` link; did not read the IP from Authentication-Results | Link ended at `onionquest[.]com` behind Cloudflare; the IP checked was Cloudflare's |
| 02 | Missed that the sender domain had no TLD; link broken by quoted-printable | Decode quoted-printable; everything before `@` is fake |
| 03 | Understood DMARC alignment backwards; missed the link hidden in heavy HTML | `dmarc=pass` because SPF aligned with From |
| 04 | Missed all three attachments; misread auth | Attachment step became mandatory |
| 05 | — | — |
| 06 | Claimed SPF pass (not in the line); took an IP from a live check; uploaded the full email to VirusTotal; extraction took 3 attempts; labelled it phishing | Use the Received header; upload only the attachment or search its hash; compare extracted size with the expected attachment size |
| 07 | Attributed Xserver to GoDaddy; labelled phishing as Trojan | Xserver is independent Japanese hosting; ask what the victim must do |
| 08 | Said Google when Received says Microsoft; stopped at the first hop; wrote "I don't know" for the response | Read the whole Received chain; learn response actions per type |
| 09 | Treated internal `10.10.49.81` as important; did not mention the QR code | Private ranges are ignored; QR moves the victim outside corporate protection |
| 10 | Treated TPG as government | TPG is a private telecom; verify with whois before naming a company |
| 11 | Generic "phishing" label | Advance-fee (419) fraud |

## Recurring patterns

| Pattern | Examples | Fix |
|---|---|---|
| Guessing who owns an IP/domain | Google / Microsoft / Cloudflare mixed up 4 times; TPG as "government" | Read the hostname in Received; confirm with whois before naming a company |
| Stopping at the first hop | 08 (missed `lindt[.]net`) | Read the full Received chain bottom-to-top |
| Not decoding links myself | 02, 03 | `grep -o 'href="[^"]*"'` or CyberChef first; do not rely on Ctrl+F for `.com` |
| Imprecise attack naming | 06 (Trojan → "phishing"), 07 (phishing → "Trojan") | Run a file = malware; enter data = phishing; reply and pay = 419 |
| Manual extraction / size check | succeeded once after 3 attempts | Compare output size with expected attachment size before uploading |
| Privacy when uploading | full email uploaded to VirusTotal | Upload the attachment or search its hash |
| Response step for unusual cases | 08 | 419: block Reply-To, report the abused company. BEC: verify via a second channel. Malware: isolate + EDR. Credential: reset + revoke sessions |
| Errors from rushing / fatigue | most errors of the week | Shorter, focused sessions |

## Improvement between cases

| Weakness | Early | End of week |
|---|---|---|
| Attachments | Missed completely in 04 | Mandatory step; applied correctly in 06, 07, 10 |
| Reading pass/fail | Guessed rather than read | Case 11 read correctly the first time |
| Emotional verdicts ("strange = hack") | Present | Case 05 judged Legit on written evidence |
