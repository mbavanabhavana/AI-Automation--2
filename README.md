🤖 AI Email Reply Bot — n8n Workflow

A webhook-triggered n8n workflow that receives a contact-form submission, generates a personalized AI reply using Google Gemini, and emails the response via Gmail.

✨ What it does
🌐 Webhook — Listens for incoming POST requests at /ai-email-reply (e.g. from a website contact form).
📝 Edit Fields — Extracts name, email, and message from the incoming request body.
🧠 AI Agent (Google Gemini) — Generates a professional, friendly, personalized HTML email reply based on the customer's message.
📧 Send a message (Gmail) — Sends the AI-generated reply out via Gmail.
🔀 Flow diagram
🌐 Webhook → 📝 Edit Fields → 🧠 AI Agent (Gemini) → 📧 Send a message (Gmail)
📋 Requirements
An n8n instance (self-hosted or cloud)
🔑 Google Gemini (PaLM) API credential connected in n8n
🔑 Gmail OAuth2 credential connected in n8n
A form or system that can POST JSON to the webhook with this shape:
json
{
  "name": "Customer Name",
  "email": "customer@example.com",
  "message": "Customer's inquiry text here"
}
⚙️ Setup
📥 Import My_workflow_2.json into your n8n instance (Workflows → Import from File).
🔌 Open the Google Gemini Chat Model node (feeds the AI Agent) and reconnect it to your own Gemini API credential.
🔌 Open the Send a message node and reconnect it to your own Gmail credential.
✏️ Update the sendTo field in Send a message — it's currently hardcoded to a single email address rather than the customer's email.
▶️ Activate the workflow, then copy the webhook's Production URL from n8n and point your form/integration to it.
⚠️ Notes
🚫 The workflow is currently active: false — activate it in n8n before going live.
📤 Heads up: the sendTo field is hardcoded to one address, so replies currently go to a fixed inbox rather than back to the customer. Change it to ={{ $('Edit Fields').item.json.Email }} if you want the AI reply sent to the customer instead.
🎨 The AI Agent is prompted to return HTML-only email body content — no subject line, no Markdown, no placeholders.
🖋️ The signature is hardcoded to "Bhavana" inside the AI prompt — update this if needed.
🛡️ No input validation is included — consider adding checks for missing name/email/message fields before they hit the AI Agent.
🔐 Credentials used
Credential	Type
Gmail account 2	gmailOAuth2
Google Gemini (PaLM) Api account 3	googlePalmApi
