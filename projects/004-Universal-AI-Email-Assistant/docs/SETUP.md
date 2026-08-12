# Setup Guide

## 1. Import the workflow
Import `workflow/004-Universal-AI-Email-Assistant.public.json` into n8n.

## 2. Configure credentials
Create/select your own credentials for:
- IMAP
- SMTP
- Groq
- Telegram
- Google Sheets OAuth2
- HTTP Header Auth for the Groq Vision HTTP Request

## 3. Telegram
In both Telegram nodes:
- Select your own Telegram credential.
- Replace `YOUR_TELEGRAM_CHAT_ID` with your own chat ID.

Never place the Telegram bot token directly inside the workflow JSON.

## 4. Google Sheets
Create a CRM sheet and configure the Google Sheets nodes to use your spreadsheet.

The template expects a sheet named `CRM v2` and fields similar to:
- Received Date
- Message ID
- Sender Name
- Sender Email
- Summary
- Subject
- Language
- Category
- Sender Type
- Priority
- Status
- Action Required
- Intent
- Original Email
- AI Draft
- Final Reply
- Notes

## 5. Groq
Configure:
- Main Groq Chat Model credential.
- Header Auth credential used by the image-analysis HTTP Request.

Do not hard-code API keys in node fields.

## 6. Email
Configure your own IMAP and SMTP accounts.

## 7. Test
Test:
- Plain email
- PDF
- DOCX
- XLSX
- JPG/PNG
- Approve
- Edit & Send
- Spam/no-reply route

## 8. Publish
Publish only after every credential and branch has been tested.
