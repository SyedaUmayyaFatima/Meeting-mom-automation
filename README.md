# Meeting MoM Automation (n8n)

An end-to-end meeting automation built with **n8n**, **Recall.ai**, **OpenAI**, **Supabase/Postgres** and **Gmail**.
It schedules a meeting bot, tracks attendance in real time, generates Minutes of Meeting (MoM) with AI,
gets admin approval, and distributes the MoM to participants with acknowledgement tracking.

## Workflows

| # | File | What it does |
|---|------|--------------|
| 1 | `workflow-1-meeting-scheduled.json` | Triggers on a new Google Calendar event, saves the meeting + participants, schedules a Recall.ai bot, sends check-in emails |
| 2 | `workflow-2-mom-generation.json` | Receives the Recall.ai webhook, fetches the transcript, generates the MoM with OpenAI, emails the admin for approval |
| 3 | `workflow-3-distribution-ack.json` | On approval, emails the MoM to participants with an "I have read the MoM" acknowledgement link |
| 4 | `workflow-4-attendance-tracking.json` | Real-time join/leave attendance tracking via Recall.ai webhooks |

## Tech stack
n8n · Recall.ai · OpenAI API · Supabase (Postgres) · Gmail OAuth2 · Google Calendar

## Setup
1. Import each workflow `.json` file into n8n (**Workflows → Import from file**).
2. Create your own credentials in n8n: Postgres/Supabase, Gmail OAuth2, Google Calendar OAuth2, Header Auth (Recall.ai).
3. In workflows 1 and 2, find the **Edit Fields** node and replace `YOUR_RECALL_API_KEY` / `YOUR_OPENAI_API_KEY` with your keys
   (better: store them as n8n credentials or environment variables).
4. Replace the webhook base URL (`https://<your-instance>.app.n8n.cloud`) and the example emails with your own.
5. Activate the workflows.

> Credentials are **not** included in this repo.Never commit API keys.
