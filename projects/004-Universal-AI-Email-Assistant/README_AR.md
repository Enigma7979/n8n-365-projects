# 004 - Universal AI Email Assistant

مشروع أتمتة احترافي للبريد الإلكتروني باستخدام **n8n** و **Groq**.

يستقبل النظام الإيميلات الجديدة، يحلل نص الرسالة والمرفقات المدعومة، يصنّف الطلب ويحدد الأولوية، ينشئ ردًا بالذكاء الاصطناعي بنفس لغة المرسل، ثم يرسل المسودة إلى Telegram للمراجعة البشرية قبل إرسال الرد النهائي وتسجيل الحالة في Google Sheets CRM.

## أهم المميزات

- استقبال الإيميلات عبر IMAP
- تحليل متعدد اللغات
- تصنيف الإيميلات وتحديد الأولوية
- قراءة ملفات PDF
- قراءة Excel/XLSX وتجميع الصفوف قبل إرسالها إلى الذكاء الاصطناعي
- قراءة Word/DOCX
- تحليل الصور باستخدام نموذج Vision عبر Groq
- مراجعة بشرية من خلال Telegram
- خيار Approve أو Edit & Send
- إرسال رد HTML احترافي
- تسجيل الحالات في Google Sheets CRM
- حالات: Pending Approval / Approved & Sent / Edited & Sent
- منع Spam والرسائل التي لا تحتاج ردًا من الوصول إلى Telegram
- استخدام توقيت Brussels في الـCRM

## بنية النظام

```text
Incoming Email
      |
      v
     Switch
      |
      +--> PDF  --------> Extract PDF --------+
      +--> DOCX --------> Extract DOCX -------+
      +--> XLSX --------> Extract + Combine --+
      +--> Image -------> Base64 -> Vision ---+
      +--> Fallback --------------------------+
                                             |
                                             v
                                  Prepare Email Data
                                             |
                                             v
                                      Main AI Model
                                             |
                                             v
                                  Should Request Review?
                                             |
                                             v
                                      Telegram Review
                                        /         \
                                   Approve      Edit & Send
                                      |             |
                                      v             v
                                  Send Email    Send Edited Email
                                      |             |
                                      +-------> CRM Update
```

## مخرجات الذكاء الاصطناعي

يقوم النظام بإنتاج بيانات منظمة مثل:

- Language
- Category
- Sender Type
- Intent
- Priority
- Urgent
- Requires Reply
- Follow Up
- Summary
- Suggested Reply

## الأمان

نسخة الـWorkflow الموجودة في هذا المستودع هي **نسخة Public منظفة**.

لا تحتوي على:

- Telegram Bot Token
- Telegram Chat ID الحقيقي
- Groq API Key
- كلمة مرور IMAP
- كلمة مرور SMTP
- Google OAuth Credentials
- Google Spreadsheet ID الحقيقي
- Credential IDs الخاصة بنسخة n8n الأصلية

بعد استيراد المشروع يجب على كل مستخدم إدخال Credentials الخاصة به.

راجع:
- `docs/SECURITY.md`
- `docs/SETUP.md`

## طريقة الاستيراد

1. نزّل الملف:
   `workflow/004-Universal-AI-Email-Assistant.public.json`
2. استورده إلى n8n.
3. أضف Credentials الخاصة بك.
4. ضع Telegram Chat ID الخاص بك.
5. اختر Google Sheet الخاص بك.
6. تأكد من مطابقة أعمدة CRM.
7. اختبر جميع المسارات قبل Publish.

## التقنيات المستخدمة

- n8n
- Groq
- Telegram Bot API
- IMAP / SMTP
- Google Sheets
- JavaScript
- Railway للاستضافة الذاتية

## Portfolio

هذا هو المشروع رقم **004** ضمن سلسلة مشاريع أتمتة عملية موجهة لبناء Portfolio قوي في سوق العمل.

## الترخيص

MIT
