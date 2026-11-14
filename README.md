# AI Business Analyst & Chat Agent (n8n)

An n8n automation project that turns submitted business information into an AI-generated analysis and lets users ask follow-up questions about the stored results. Created as a student automation project; the original workflow was tested, but these **sanitized exports require configuration** before they will run in another n8n instance.

## How it works

```text
Workflow 1 — Form Submission
n8n Form Trigger → HTTP Request (POST)
                             ↓
Workflow 2 — Business Analysis & Chat
Webhook → Basic LLM Chain → Google Sheets (append analysis)

Chat Trigger → Google Sheets (read business record) → AI Agent → Chat response
                                                ↳ Chat Model + Simple Memory
```

Both the webhook analysis path and the chat path live on the same canvas in Workflow 2.

## Features

- Business intake form covering business description, audience, goals, marketing channels, challenges, leads, registrations, and pricing.
- Webhook-based handoff between the form workflow and analysis workflow.
- LLM-generated business overview, metrics, opportunities, recommendations, and missing-data notes.
- Google Sheets storage of the submitted business data and generated summary.
- Conversational questions grounded in the retrieved business record and saved analysis, with short-term chat memory.

## Technologies

n8n · HTTP/Webhooks · LLM Chain · AI Agent · Google Sheets · Chat Model · Simple Memory

## Repository files

- [`workflows/form-submission.json`](workflows/form-submission.json) — form trigger and HTTP handoff.
- [`workflows/business-analysis-chat.json`](workflows/business-analysis-chat.json) — analysis webhook, LLM chain, Google Sheets storage, and conversational chat.

## Setup

1. Import both JSON files into n8n.
2. Configure the chat-model credentials in the analysis and chat nodes.
3. Create a Google Sheet with the columns `businessId`, `businessName`, `businessData`, and `Aisummary`. Set its document ID in both Google Sheets nodes, and verify the sheet tab name.
4. Configure the form workflow's HTTP Request URL to point to the analysis workflow's **production** webhook URL when published, or the **test** webhook URL during an active editor test. The exported URL is a placeholder.
5. Review the `Get row(s) in sheet` node: the original project filters `businessName = ABC Academy`. Change that filter to your target business before demonstrating other companies. The current chat does **not** automatically select the newest submitted business.
6. Test form submission and confirm a row is written; then open the chat trigger and ask a question about the saved business analysis.

## Sample questions

- What are the main challenges facing this business?
- What is the lead-to-registration conversion rate?
- What should the business improve first?
- Which details are missing from the analysis?

## Limitations and future improvements

- The existing chat lookup uses a fixed business name, rather than per-user or per-business record selection.
- Google Sheets is a lightweight storage choice rather than a full application database.
- The original exports were tied to a specific n8n workspace and Google Sheet; both have been anonymized here.
- Additional validation, error handling, credential configuration, and regression tests are appropriate before deployment.

## Author

Ahmed Mostafa — [GitHub](https://github.com/ahmedmostafa-ai)
