# 001 - Smart Morning Notifier

## Description
An automated system that sends your daily tasks to Telegram every morning at 8:00 AM. Tasks are organized by day of the week with random motivational quotes.

## Tools Used
- N8N
- Telegram Bot
- JavaScript / Python

## How to Use
1. Download smart-morning-notifier.json.
2. Import it into N8N.
3. Add your Telegram Bot Token and Chat ID.
4. Customize tasks and quotes in the Code/Python node.
5. Activate the workflow.

## Schedule
- Monday to Sunday at 8:00 AM.

## Customization
Edit the tasks array in the Code node to match your weekly routine. Change quotes as you like.

## Video Tutorial
[YouTube Link]

## License
MIT - Open Source

## Security and setup before activation
- Create **your own Telegram bot** using [BotFather](https://t.me/BotFather). Configure your own Telegram API credential in n8n and select it in **Send a text message**.
- Replace `YOUR_TELEGRAM_CHAT_ID` with **your own** Telegram chat ID.
- Never put your bot token into the public workflow JSON or GitHub. The public template has no preconfigured credentials.
- If a real token was ever exposed, revoke/rotate it immediately; deleting it from the latest commit does not remove Git history.
- Confirm your timezone and schedule, and test a message before activation.
