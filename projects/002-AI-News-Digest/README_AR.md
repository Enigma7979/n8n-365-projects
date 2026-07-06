# 002 - ملخص أخبار الذكاء الاصطناعي 🤖📰

مشروع أتمتة بـ n8n يسحب آخر أخبار الأتمتة والذكاء الاصطناعي من Reddit، يلخص كل عنوان بالعربي باستخدام نموذج Llama 3.3 عبر Groq، ويرسل الملخص مباشرة على تيليجرام.

## آلية العمل
1. **Schedule Trigger** – يشتغل يومياً بوقت محدد
2. **RSS Read** – يسحب آخر المنشورات من r/automation
3. **Limit** – يحتفظ بآخر 3 أخبار فقط
4. **HTTP Request (Groq API)** – يلخص كل عنوان بالعربي
5. **Telegram** – يرسل الملخص مباشرة لمحادثتك

## الأدوات المستخدمة
- [n8n](https://n8n.io) (مستضاف ذاتياً على Railway)
- [Groq API](https://console.groq.com) (نموذج Llama 3.3 70B – نسخة مجانية)
- خاصية RSS من Reddit
- Telegram Bot API

## طريقة التشغيل
1. استورد ملف `workflow.json` لحسابك بـ n8n
2. استبدل `YOUR_GROQ_API_KEY_HERE` بمفتاح Groq الخاص بك
3. استبدل `YOUR_TELEGRAM_CHAT_ID` برقم الـ Chat ID الخاص بحسابك
4. اربط الـ Credential الخاص ببوت تيليجرام
5. فعّل الـ workflow

## الحالة
✅ مكتمل ومُختبر
