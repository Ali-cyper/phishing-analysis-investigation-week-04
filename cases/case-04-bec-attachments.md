# Case 04 — BEC with multiple paths

| Field | Value |
|---|---|
| Pattern | Business email compromise with three attachments |
| Verdict | **BEC** |

## Indicators
- Link: `goldent[.]com`
- Attachments: two `.mobileconfig` files and one named `Inbox Rules`

## What I did right
Noticed the odd sender name and found the `goldent[.]com` link.

## What I missed
All three attachments (two `.mobileconfig`, one named Inbox Rules); also misread the authentication results.

## Lesson
The attachment itself was the real attack. This case is why the attachment step became mandatory in the template.

## Not recorded
Full hashes, full IP list and a per-event timeline were not recorded in the source report.
