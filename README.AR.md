# تحقيق Phishing — الأسبوع الرابع

> الأسبوع الرابع من منهج SOC ذاتي مكوّن من 12 أسبوع (مسار Blue Team / SOC Analyst).
> تحليل عملي لـ **11 إيميل** (10 هجمات حقيقية + 1 سليم للمقارنة): headers، SPF/DKIM/DMARC، الروابط، المرفقات، الـ IOCs، والـ verdict.

🇬🇧 English: [README.md](README.md)

## النطاق

| البند | القيمة |
|---|---|
| العينات | 11 (.eml) |
| المصدر | 10 من مستودع `phishing_pot` العام (هجمات التقطتها honeypots)، والعينة 05 إيميل نظيف للمقارنة |
| الأنماط | credential phishing، حساب مخترق، BEC، مرفق malware (ISO / تجاوز MOTW)، quishing (QR)، احتيال 419 |
| الأدوات | MXToolbox، VirusTotal، CyberChef، WhereGoes، urlscan.io، AbuseIPDB، whois، crt.sh |

> ⚠️ العينات هجمات حقيقية، فُتحت داخل VM معزولة فقط، وهي **غير موجودة** بالمستودع.

## المنهج

كل إيميل انحلل بنفس القالب الثابت ([templates/phishing-analysis-template.md](templates/phishing-analysis-template.md)):

1. **Headers** — From / Return-Path / Reply-To / Message-ID
2. **Auth** — انسخ `spf/dkim/dmarc` حرفياً قبل التفسير
3. **Links** — استخرج، وسّع، افحص الدومين النهائي
4. **Attachments** — خطوة إجبارية، ولا verdict إذا تخطيتها
5. **IP / Domain** — اقرأ الـ hostname قبل فحص السمعة
6. **Verdict** — الحكم + مستوى الثقة + الدليل المحدد

## النتائج

| # | النمط | الحكم | الحالة |
|---|---|---|---|
| 01 | انتحال بسيط، فشل كل الـ auth | Phishing | [01](cases/case-01-simple-spoofing.md) |
| 02 | حيلة `@`، دومين بلا TLD | Phishing | [02](cases/case-02-at-trick.md) |
| 03 | حساب مدرسة حقيقي مخترق | Spam / مخترق | [03](cases/case-03-compromised-account.md) |
| 04 | BEC + مرفقات `.mobileconfig` | BEC | [04](cases/case-04-bec-attachments.md) |
| 05 | مرجع مقارنة | Legit | [05](cases/case-05-legit.md) |
| 06 | مرفق ISO يتفادى فحص ويندوز (MOTW) | Malware | [06](cases/case-06-iso-trojan.md) |
| 07 | مرفق HTML ينتحل بنك حقيقي | Phishing | [07](cases/case-07-html-attachment.md) |
| 08 | محامية وهمية عبر بنية شركة عالمية | احتيال 419 | [08](cases/case-08-419-lindt.md) |
| 09 | QR code ينتحل محفظة رقمية | Phishing | [09](cases/case-09-quishing.md) |
| 10 | تحقق KYC عبر بنية شركة اتصالات | Phishing | [10](cases/case-10-kyc.md) |
| 11 | أرملة وميراث عبر Gmail حقيقي | احتيال 419 | [11](cases/case-11-widow-inheritance.md) |

## أهم الدروس

- IP نظيف ما يعني إيميل آمن: البنية المشتركة (Cloudflare، Microsoft 365، Google) سمعتها سمعة الشركة مو المرسل.
- `pass` يعني الهوية مؤكدة، مو المحتوى آمن.
- المرفق ممكن يكون الهجوم كله (حالة 04).
- صدّق السطر الخام من `Authentication-Results` مو تلخيص أي موقع.
- غياب الدليل التقني ما يعني نظيف: الحكم بـ 08 و10 و11 جاء من المحتوى والسياق.
- صنّف حسب المطلوب من الضحية: تشغيل ملف (malware)، إدخال بيانات (phishing)، رد ودفع (419).

التفاصيل: [reference.md](reference.md) — الأخطاء: [mistake-log.md](mistake-log.md).

## القيود

هذا التوثيق مبني فقط على تقرير نهاية الأسبوع. الـ hashes الكاملة، قوائم الـ IP الكاملة، الـ timeline لكل حالة، والـ prompts الأصلية غير مسجلة فيه، لذلك **ما أضفتها** بدل التخمين. الدومينات بصيغة defanged.
