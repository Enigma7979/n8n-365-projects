# 004 - Universal AI Email Assistant

A production-style AI email automation built with **n8n** and **Groq**.

It receives incoming emails, analyzes the message and supported attachments, classifies the request, prepares a multilingual AI reply, sends the draft to Telegram for human approval, sends the final email, and logs the case in a Google Sheets CRM.

## Main Features

- IMAP email trigger
- Multilingual email analysis
- AI classification and priority detection
- PDF text extraction
- Excel/XLSX extraction and row consolidation
- Word/DOCX extraction
- Image analysis with a vision-capable Groq model
- Telegram human-in-the-loop approval
- Approve or Edit & Send workflow
- Professional HTML email replies
- Google Sheets CRM logging
- Status tracking: Pending Approval / Approved & Sent / Edited & Sent
- Spam/no-reply filtering
- Brussels timezone for shared CRM timestamps

## Architecture

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

## AI Output

The workflow produces structured fields such as:

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

## Security

This public repository contains a **sanitized workflow template**.

It does **not** contain:

- Telegram bot token
- Telegram private chat ID
- Groq API key
- IMAP password
- SMTP password
- Google OAuth credentials
- Real Google Spreadsheet ID
- n8n credential references from the original instance

You must configure your own credentials after importing the workflow.

See [docs/SECURITY.md](docs/SECURITY.md) and [docs/SETUP.md](docs/SETUP.md).

## Import

1. Download `workflow/004-Universal-AI-Email-Assistant.public.json`.
2. Import it into n8n.
3. Configure your own credentials.
4. Replace the placeholder Telegram Chat ID.
5. Select your own Google Sheet.
6. Verify the CRM column mapping.
7. Test each branch before publishing.

## Tech Stack

- n8n
- Groq
- Telegram Bot API
- IMAP / SMTP
- Google Sheets
- JavaScript
- Railway (self-hosted deployment)

## Portfolio Project

Project **#004** in a hands-on automation portfolio focused on practical, market-relevant workflows.

## License

MIT

## Required: your own accounts and API keys
- Create **your own Telegram bot** through [BotFather](https://t.me/BotFather), configure your own Telegram API credential in n8n, and replace `YOUR_TELEGRAM_CHAT_ID`.
- Get **your own Groq API key** from [Groq Console](https://console.groq.com/keys). Configure it in the **Groq model credential** and separately in the **HTTP Header Auth credential** for Groq Vision where required.
- Configure **your own IMAP, SMTP and Google Sheets OAuth credentials**, and replace the placeholder Google Spreadsheet ID. No working accounts, passwords, or API keys are bundled.
- Never paste secrets into workflow JSON or public commits. Rotate any exposed key immediately, including if it appeared in Git history.
- Test all approval, attachment and sending branches with non-sensitive sample messages before production use.
