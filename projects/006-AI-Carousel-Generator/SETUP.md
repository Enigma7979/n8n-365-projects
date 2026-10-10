# Setup and deployment | الإعداد والنشر

## User-supplied values | بيانات يضعها المستخدم بنفسه

| Setting | Where | Example / placeholder |
|---|---|---|
| Telegram bot token | n8n Telegram API credential | `YOUR_TELEGRAM_BOT_TOKEN` |
| Groq API key | n8n HTTP Header Auth credential | `Bearer YOUR_GROQ_API_KEY` |
| Renderer endpoint | n8n server environment or HTTP node URL | `CAROUSEL_RENDERER_URL=http://YOUR_RENDERER_HOST:8080/function` |
| Telegram allowed chat/user IDs (optional) | Add your own filtering node | `YOUR_ALLOWED_CHAT_ID` |
| Renderer network/IP | Your own private network and firewall | `YOUR_RENDERER_HOST` |

**Never put actual credentials in the public workflow JSON or GitHub.**

## Deployment notes
- The renderer is a separate Chromium/Browserless service. Installing only n8n is not sufficient.
- The template calls `POST /function`, expecting a JSON object containing screenshot image bytes, which the next node validates as PNG.
- The renderer must have enough memory and time for seven 1080×1920 screenshots; HTTP batching is configured.
- Keep renderer networking private where possible. Do not expose an unauthenticated browser service on the public Internet.
- Ensure the n8n instance permits `$env.CAROUSEL_RENDERER_URL`, or enter your own endpoint in the HTTP node.
- The Telegram bot token must not simultaneously be attached to another active Telegram Trigger if webhooks conflict.
- After import, check the Groq model name, credentials, Telegram nodes and renderer connectivity, then publish.

## بالعربية
كل مستخدم يُدخل بياناته الخاصة داخل n8n: توكن Telegram، مفتاح Groq، عنوان خدمة Chromium، وأرقام السماح بالمحادثات إن استخدمها. لا يوجد في المشروع العام عنوان IP خاص بالمطور أو رقم مجموعته. لا ترفع الأسرار إلى GitHub. اختبر وصول الصور السبع قبل استخدام المشروع مع الجمهور.
