# Architecture

## Main flow

1. **Receive New Email / Email Trigger (IMAP)**
2. **Switch** routes the message according to attachment MIME type.
3. Attachment branches:
   - PDF → Extract from File
   - DOCX → custom JavaScript extraction
   - XLSX → Extract from File → JavaScript row consolidation
   - Image → Base64 preparation → Groq Vision HTTP Request → text preparation
   - Fallback → normal body processing
4. **Prepare Email Data** combines the email body and extracted attachment content.
5. **Generate AI Reply** classifies the email and drafts a multilingual response.
6. **Should Request Review** prevents spam/no-reply items from entering Telegram.
7. **Telegram Review** requests human approval.
8. Approved path sends the AI draft.
9. Edit path collects a manual replacement and sends the edited reply.
10. Google Sheets CRM records and updates the final status.

## Design principle

The workflow keeps AI generation separate from human authorization. No customer reply is sent from the review route until the human approval step is completed.
