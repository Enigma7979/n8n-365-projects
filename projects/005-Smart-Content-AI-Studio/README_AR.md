# 005 — استوديو أفكار المحتوى الذكي

[English](README.md)

مشروع تعليمي مجاني ومفتوح المصدر يعتمد على **n8n + Telegram + Groq**. ترسل موضوعًا إلى بوت تيليغرام، فيُنتج لك الذكاء الاصطناعي **3 أفكار Reels بالعربية**؛ كل فكرة تتضمن هوك، وفكرة الفيديو، وسيناريو يقارب 20 ثانية، وCTA، ووصفًا إنجليزيًا قصيرًا.

## المتطلبات
- منصة n8n مع عقد AI Agent وGroq Chat Model.
- بوت تيليغرام خاص بك تنشئه باستخدام [BotFather](https://t.me/BotFather).
- حساب Groq API (قد توجد حدود مجانية للاستخدام).

## طريقة التشغيل
1. حمّل ملف [Workflow JSON](workflow/Smart-Content-AI-Studio.json).
2. افتح n8n ثم اختر **Import from File** لاستيراد الملف.
3. أنشئ **Telegram API Credential** برمز البوت الخاص بك، واربطه بعقدتي **Telegram Incoming Message** و**Reply on Telegram**.
4. أنشئ **Groq API Credential** بمفتاحك الخاص واربطه بعقدة **Groq Chat Model**.
5. تحقق من توفر النموذج `openai/gpt-oss-20b` في حساب Groq؛ اسمه لا يعني أنك تحتاج اشتراك OpenAI API.
6. اضغط **Listen for test event** في Telegram Trigger، ثم أرسل موضوعًا للبوت. بعد نجاح الاختبار فعّل المشروع.

مثال: `لماذا تتوقف فيديوهات Reels عند 300 مشاهدة؟`

## مسار التنفيذ
`Telegram Incoming Message → Prepare Telegram Topic → Generate 3 Reel Ideas → Reply on Telegram`

وترتبط عقدة **Groq Chat Model** بعقدة **AI Agent** كمدخل نموذج اللغة.

## تنبيهات
- **لا يحتوي المشروع على API Keys أو Telegram Tokens أو بيانات دخول أو Chat IDs شخصية.**
- يجب إعداد Credentials الخاصة بك بعد الاستيراد؛ المشروع غير مفعل تلقائيًا.
- لا تستخدم نفس البوت مع Telegram Trigger نشط في Workflow آخر في الوقت نفسه.
- قبل نشر البوت للعامة، أضف قيود استخدام وتحققًا من الرسائل والأوامر.
- راجع المعلومات الناتجة عن الذكاء الاصطناعي قبل نشرها.
- النسخة العامة تتضمن مسار Telegram فقط؛ تم استبعاد مسار Webhook التجريبي من التصدير.

الرخصة: MIT حسب [رخصة المستودع](../../LICENSE).
