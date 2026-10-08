# 005 — Smart Content AI Studio

[العربية](README_AR.md)

A reusable **Telegram + Groq + n8n** workflow that transforms a content topic into **three Instagram Reel ideas** in Arabic. Each idea includes a hook, concept, ~20-second script, CTA and a short English caption.

## Tools
- n8n (with AI Agent and Groq Chat Model nodes)
- Telegram bot (created using [@BotFather](https://t.me/BotFather))
- Groq API account (subject to provider usage limits)

## Quick setup
1. Download [the workflow JSON](workflow/Smart-Content-AI-Studio.json).
2. In n8n, **Import from File** and choose the JSON.
3. Create a **Telegram API** credential using **your own** bot token. Set it in **Telegram Incoming Message** and **Reply on Telegram**.
4. Create a **Groq API** credential using **your own** API key. Set it in **Groq Chat Model**.
5. Verify the model `openai/gpt-oss-20b` is available to your Groq account (the model name does not require OpenAI API billing).
6. Use **Listen for test event** on Telegram Trigger, send your bot a topic, and confirm the response. Once tested, activate/publish the workflow.

Example message: `Why do my Instagram Reels stop at 300 views?`

## Flow
`Telegram Incoming Message → Prepare Telegram Topic → Generate 3 Reel Ideas → Reply on Telegram`

`Groq Chat Model` connects to the AI Agent via the language-model input.

## Security and limitations
- **No API keys, bot tokens, credentials, or personal chat IDs** are included in the template.
- Credentials must be configured after importing; the workflow is disabled by default.
- Telegram Trigger should not share the same bot token with another active Telegram Trigger workflow.
- The template responds to text messages; consider filtering commands/non-text events and adding rate limits before sharing publicly.
- Generated scripts are suggestions; verify factual claims before publishing.
- This public template intentionally includes only the Telegram branch of the working project; the experimental webhook branch is excluded.

MIT License — see the repository [LICENSE](../../LICENSE).
