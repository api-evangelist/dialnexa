---
name: dialnexa-run-batch-campaign
description: Create a DialNexa batch calling campaign, monitor recipient outcomes, and pause, resume, or cancel it.
api: dialnexa:dialnexa-batch-calls-api
operations: [createBatchCall, listBatchCalls, getBatchCall, updateBatchCallStatus]
generated: '2026-09-03'
method: generated
source: openapi/_original/dialnexa-openapi.json + https://dialnexa.com/docs/api-reference/reliability.md
---

# Run a batch calling campaign

Base URL `https://api.dialnexa.com`, `Authorization: Bearer YOUR_API_KEY`.

1. **Create the campaign** — `POST /v1/batch-calls` (`createBatchCall`). This is a billable action: never retry a timed-out create without first listing (`listBatchCalls`) and matching on your own business data.
2. **Monitor** — `GET /v1/batch-calls` (`listBatchCalls`) filters by status (draft, waiting, scheduled, running, paused, completed, cancelled, deleted); records live under `items` with top-level `total`, `page`, `limit`. `GET /v1/batch-calls/{id}` (`getBatchCall`) returns one campaign with retry counters and result counts.
3. **Control** — `PATCH /v1/batch-calls/{id}/status` (`updateBatchCallStatus`) pauses, resumes, or cancels the campaign. Pause/resume are reversible; cancel is terminal for remaining recipients. This is a state transition: after an uncertain timeout, re-read the campaign and confirm the transition did not happen before retrying.
4. **Per-call outcomes** arrive on the `call_ended` webhook with `hangup_reason` (`user_did_not_pick_up`, `user_busy`, `voicemail_detected`, ...). Treat unknown reason values as valid.
5. **Errors** use the `{statusCode, message, error}` envelope; `409` means the status action is not valid for the campaign's current state.
