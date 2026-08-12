# Security Notes

The workflow in this repository is a sanitized public template.

## Removed from the public JSON
- n8n credential references
- Telegram private chat ID
- Google Spreadsheet ID and gid
- cached Google Sheet URLs
- workflow instance ID
- workflow version ID
- n8n instance fingerprint
- webhook IDs from the original workflow

## Secrets that must never be committed
- Telegram bot tokens
- Groq API keys
- IMAP passwords
- SMTP passwords
- Google OAuth client secrets/tokens
- Railway secrets
- `.env` files

## Recommended practice
- Store secrets in n8n Credentials or your deployment platform's secret manager.
- Keep the public workflow inactive after import until credentials are configured.
- Rotate any secret immediately if it is accidentally committed.
- Do not rely only on deleting a secret from the latest Git commit; Git history may retain it.
