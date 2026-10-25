# Case 07 — HTML attachment

| Field | Value |
|---|---|
| Pattern | HTML attachment impersonating Capital One |
| Verdict | **Phishing** |

## Indicators
- Form posts to `data.php`
- Page scripts loaded from Netlify (legitimate free service)
- Sending host: Xserver (independent Japanese hosting), matching a Japanese IP (Kagoya)

## What I did right
Trusted the raw header over the secondary table and extracted the hash myself.

## What I missed
Attributed Xserver to GoDaddy (it is independent Japanese hosting); labelled it Trojan instead of phishing.

## Lesson
Phishing = the victim is asked to enter data. Loading scripts from a legitimate service makes the file look cleaner under static scanning.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
