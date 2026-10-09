# 002 - AI News Digest 🤖📰

An automated n8n workflow that fetches the latest automation & AI news from Reddit, summarizes each headline in Arabic using Groq's Llama 3.3 model, and delivers the digest straight to Telegram.

## How it works
1. **Schedule Trigger** – runs daily at a set time
2. **RSS Read** – pulls the latest posts from r/automation
3. **Limit** – keeps only the top 3 most recent items
4. **HTTP Request (Groq API)** – summarizes each headline in Arabic
5. **Telegram** – sends the summary directly to your chat

## Tools used
- [n8n](https://n8n.io) (self-hosted on Railway)
- [Groq API](https://console.groq.com) (Llama 3.3 70B – free tier)
- Reddit RSS feed
- Telegram Bot API

## Setup
1. Import `ai-news-digest.json` into n8n.
2. Create an HTTP Header Auth credential for your own Groq API key and select it in the HTTP Request node (see security section below).
3. Replace `YOUR_TELEGRAM_CHAT_ID` with your own chat ID.
4. Connect your own Telegram Bot credential.
5. Test before activating.

## Status
✅ Completed and tested

## Required: configure your own API credentials
- Get **your own Groq API key** from [Groq Console](https://console.groq.com/keys). In n8n, create an **HTTP Header Auth credential** with name `Authorization` and value `Bearer YOUR_ACTUAL_GROQ_API_KEY` (replace the placeholder with your actual key **inside n8n only**). Select it in **HTTP Request**.
- Create **your own Telegram bot** with [BotFather](https://t.me/BotFather), add your own Telegram API credential in n8n, and select it in **Send a text message**.
- Replace `YOUR_TELEGRAM_CHAT_ID` with your own chat ID. No shared Telegram or Groq keys are provided.
- **Never commit actual tokens or API keys** to workflow JSON or GitHub. Rotate any credential that was previously exposed, including in Git history.
- Verify the chosen Groq model remains available to your account before activating; model names and provider limits can change.
- The public workflow now uses an n8n credential instead of an embedded Groq Authorization header.
