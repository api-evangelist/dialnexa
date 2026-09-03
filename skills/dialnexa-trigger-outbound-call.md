---
name: dialnexa-trigger-outbound-call
description: Place a single DialNexa Voice AI outbound call, reconcile it safely after timeouts, and read the result.
api: dialnexa:dialnexa-calls-api
operations: [createCall, getCall, listCalls]
generated: '2026-09-03'
method: generated
source: openapi/_original/dialnexa-openapi.json + https://dialnexa.com/docs/api-reference/reliability.md
---

# Trigger an outbound Voice AI call

Base URL `https://api.dialnexa.com`. Authenticate every request with `Authorization: Bearer YOUR_API_KEY` (the full `key_id:secret` value).

1. **Create the call** — `POST /v1/calls` (`createCall`) with `agent_id`, `phone_number` in E.164 form (`+919876543210`, never bare digits), and a `metadata` object. Put your own stable correlation value in `metadata`: the v1 contract has NO idempotency header, and this is the documented duplicate-protection pattern.
2. **Never retry a create blindly.** `createCall` is billable — a timeout can land AFTER the call was accepted. On timeout, `GET /v1/calls` (`listCalls`) and reconcile by your correlation metadata before deciding to submit again.
3. **Read the result** — `GET /v1/calls/{id}` (`getCall`) for status, transcript, summary, and post-call analysis. Prefer webhooks (`call_initiated`, `call_ended`) over aggressive polling; verify the `x-dialnexa-signature` HMAC-SHA256 hex digest over the raw body before trusting a payload.
4. **Errors** come as `{statusCode, message, error}` (message may be an array of validation strings). Do not retry 400/401/403/404/409; retry 429 with backoff honoring `Retry-After` when present.
5. **403 on a valid number** means the destination route is not enabled for the workspace (Telephony Config), not a bad request.
