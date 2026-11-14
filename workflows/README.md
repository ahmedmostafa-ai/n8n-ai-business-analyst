# n8n Workflows

This directory contains two sanitized n8n workflow exports.

## Form Submission

**File:** `form-submission.json`

Collects business information through an n8n form and sends the submitted data to the analysis workflow using an HTTP Request.

## Business Analysis & Chat Agent

**File:** `business-analysis-chat.json`

Receives business information through a webhook, generates an AI-powered business analysis, and stores the result in Google Sheets.

The chat interface retrieves stored business information and uses an AI Agent with conversation memory to answer follow-up questions.

## Import Notes

- Import both JSON files into n8n.
- Configure the required LLM and Google Sheets credentials.
- Configure the Google Sheets document and columns.
- Update the Form Submission HTTP Request node with the analysis workflow's webhook URL.
- Review the fixed `ABC Academy` lookup in the chat workflow before using another business.

The exports have been sanitized for public sharing. The original implementation was tested, but these sanitized copies require configuration after importing.
