# 006 — AI Carousel Generator

[العربية](README_AR.md) · [Workflow JSON](workflow/006-AI-Carousel-Generator.public.json)

Generate **seven Arabic 1080 × 1920 PNG carousel slides** from a topic sent to your own Telegram bot, using n8n, Groq and a self-hosted Chromium/Browserless renderer. The slide header reflects the requested topic; no project watermark is printed.

## Requirements
- n8n with Telegram Trigger, Telegram, HTTP Request and Code nodes
- Your own Telegram bot token, created with [BotFather](https://t.me/BotFather)
- Your own [Groq API key](https://console.groq.com/keys) (HTTP Header Auth, `Authorization: Bearer YOUR_GROQ_API_KEY`)
- A **Chromium/Browserless service** reachable from your n8n instance, supporting `POST /function`. Deploy your own service; the original creator's private renderer is **not** shared.
- Set `CAROUSEL_RENDERER_URL` in your n8n server environment to the full endpoint, for example `http://YOUR_RENDERER_HOST:8080/function`. The imported HTTP node uses `{{ $env.CAROUSEL_RENDERER_URL }}`. If your n8n instance blocks environment-variable access, replace the URL expression in that node with your own reachable renderer endpoint. Do **not** use the example address unchanged.

## Installation
1. Download and import [the sanitized JSON](workflow/006-AI-Carousel-Generator.public.json) into **your own n8n**.
2. Create a **Telegram API** credential with your **own bot token**, and select it in **006 Telegram Topic**, **Telegram - Review Draft** and **006 - Send PNG to Telegram**.
3. Create an **HTTP Header Auth** credential for Groq with header `Authorization` and value `Bearer YOUR_GROQ_API_KEY`. Select it in **Groq - Generate Arabic Carousel Copy**.
4. Deploy your own Browserless/Chromium renderer. Set `CAROUSEL_RENDERER_URL` (including `/function`) on your n8n deployment and restart n8n if required. Ensure the n8n server can reach the renderer; configure network/firewall authentication for your environment.
5. Verify the Groq model `allam-2-7b` is available to your account, or choose a supported model. Review the prompt and the Arabic font availability in your renderer.
6. Save and activate/publish your imported workflow, send **your own bot** a text topic, and check that all seven PNG files arrive and display correctly.

**Chat IDs:** This workflow reads the incoming Telegram chat ID dynamically from the message. No private chat ID or group ID needs to be copied from the original project. To restrict access, add your **own** allowlist of Telegram user/chat IDs and rate limits before making the bot public.

## Workflow
`Telegram topic → Prepare topic → Groq Arabic copy → Split into 7 slides → SVG template → Chromium PNG renderer → Validate PNG → Telegram documents`

A parallel Telegram message sends a text draft for review. Output PNGs are suitable for import into Canva Free; this template **does not connect to Canva's API** and does not produce native editable Canva designs.

## Security and privacy
- The public JSON includes **no original credential bindings, bot token, Groq API key, Telegram chat/group ID, private Railway host, public IP, or webhook ID**.
- The renderer endpoint is a placeholder configured by each user. Do not commit real `.env` files, tokens, private hosts, chat IDs, logs or screenshots.
- Each user must supply **their own** Telegram bot token, Groq key and renderer address. Never reuse the creator's infrastructure.
- Secure your renderer with private networking and/or access controls. Telegram bots are reachable by others unless you implement allowlisting.
- Import is **disabled by default**. Inspect nodes and test before activating.
- If any real credential was previously exposed in Git history, rotate it; deleting a line in a later commit is insufficient.

See [SETUP.md](SETUP.md) and [.env.example](.env.example). MIT License: [repository LICENSE](../../LICENSE).
