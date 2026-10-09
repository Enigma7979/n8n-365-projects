# 003 - Amazon Price Tracker 🛒💰

An automated n8n workflow that monitors a product's price on Amazon on a schedule, compares it with the last saved price, and sends a Telegram alert whenever the price drops.

## How it works
1. **Schedule Trigger** – runs periodically at a set interval
2. **HTTP Request** – fetches the Amazon product page HTML
3. **Code** – pre-processes the raw HTML
4. **HTML (Extract HTML Content)** – extracts the current price from the page
5. **Edit Fields** – organizes the extracted data
6. **Code1** – additional processing/formatting
7. **Switch** – compares the new price against the last saved price
8. **Build Message** – formats the alert message
9. **Telegram** – sends the price-drop alert directly to your chat

## Tools used
- [n8n](https://n8n.io) (self-hosted on Railway)
- Amazon product page (HTML scraping via HTTP Request)
- n8n Static Data (for storing the last known price)
- Telegram Bot API

## Setup
1. Import `workflow.json` into your n8n instance
2. Replace the Amazon product URL in the HTTP Request node with your own target product
3. Replace `YOUR_TELEGRAM_CHAT_ID` in the Telegram node with your own chat ID
4. Connect your own Telegram Bot credential
5. Adjust the Schedule Trigger interval as needed
6. Activate the workflow

## Status
✅ Completed and tested

## Security and bot setup
- Create **your own Telegram bot** with [BotFather](https://t.me/BotFather), then configure your own Telegram API credential in n8n for **Send a text message**.
- Replace `YOUR_TELEGRAM_CHAT_ID` with your own chat ID. This public template provides no shared bot credentials.
- Never commit a real Telegram bot token to GitHub or workflow JSON. Rotate a token immediately if it was ever exposed.
- The Amazon product URL is an **example only**. HTML price extraction can break when Amazon changes its markup or blocks automated requests; test the workflow before activation.
