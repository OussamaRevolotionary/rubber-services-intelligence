# Product 2 — N8N Setup (10 minutes)

Everything is pre-built. You only add **credentials** and set **one URL** in the HTML.

---

## STEP 0 — Set your n8n base URL in the HTML (do this once)

Open `index.html`, find this line near the top of the `<script>`:

```js
const N8N_BASE_URL = "https://YOUR-N8N-INSTANCE";
```

Replace it with your n8n base address (NO trailing slash). Examples:
- n8n Cloud:   `https://oussama.app.n8n.cloud`
- Self-hosted: `https://n8n.yourdomain.com`

That's the **only** edit in the HTML. The two webhook URLs build themselves from it:
- `…/webhook/services-chatbot`  (Workflow A)
- `…/webhook/services-inquiry`  (Workflow B)

These paths already match the imported workflows — no copy/paste of webhook URLs needed.

---

## WORKFLOW A — Chatbot

1. n8n → **Workflows → Import from File** → select `workflow_A_chatbot.json`.
2. Open the **"OpenAI — Chat Completion"** node → *Credential for HTTP Header Auth* → **Create New**:
   - **Name:** `Authorization`
   - **Value:** `Bearer sk-YOUR_OPENAI_KEY`
   - Save.
3. Click **Active** (top-right toggle). Done.

> The full system prompt (all 24 services, equipment, OE rules) is already inside the "Set — Build System Prompt" node. Nothing to write.

---

## WORKFLOW B — Lead Capture

1. **Import from File** → `workflow_B_inquiry.json`.
2. **Google Sheet:** create a sheet with these column headers in row 1:
   ```
   timestamp | name | company | email | phone | material | requirements | standard | sample_qty | turnaround | notes | source
   ```
   Copy its **Sheet ID** (the long string in the URL between `/d/` and `/edit`).
3. Open **"Google Sheets — Append Lead"** node:
   - Create/select a **Google Sheets OAuth2** credential.
   - Paste your **Sheet ID** into *Document ID*.
4. Open **"Gmail — Notify You"** node:
   - Create/select a **Gmail OAuth2** credential (account: oussamabdi19@gmail.com).
   - (Notification address is already set to your email — change if needed.)
5. Click **Active**. Done.

---

## QUICK TEST

- Chatbot: open the demo, click the bot bubble → ask *"Turnaround for MDR rheometry?"* → expect "C01 … 2–3 days".
- Form: click **Submit Requirements** → fill → submit → check your Google Sheet for a new row + your inbox for the notification email.

If either fails, the most common cause is the `N8N_BASE_URL` value or a workflow not toggled **Active**.
