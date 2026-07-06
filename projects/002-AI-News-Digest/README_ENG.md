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
1. Import `workflow.json` into your n8n instance
2. Replace `YOUR_GROQ_API_KEY_HERE` in the HTTP Request node with your own [Groq API key](https://console.groq.com/keys)
3. Replace `YOUR_TELEGRAM_CHAT_ID` in the Telegram node with your own chat ID
4. Connect your own Telegram Bot credential
5. Activate the workflow

## Status
✅ Completed and tested
