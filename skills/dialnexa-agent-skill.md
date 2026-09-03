# DialNexa Agent Skill

Use this skill when an agent needs to understand, evaluate, or integrate with DialNexa Voice AI workflows.

DialNexa builds Voice AI agents for sales calls, lead qualification, follow-ups, meeting booking, collections, support workflows, and multilingual customer conversations.

## Discovery Resources

- Website overview: https://dialnexa.com/llms.txt
- Documentation index: https://dialnexa.com/docs/llms.txt
- API reference: https://dialnexa.com/docs/api-reference/introduction
- OpenAPI specification: https://dialnexa.com/docs/api-reference/openapi.json
- API catalog: https://dialnexa.com/.well-known/api-catalog
- Authentication instructions: https://dialnexa.com/auth.md

## Authentication

DialNexa public API access uses API keys passed as bearer credentials.

1. Sign in to the DialNexa dashboard.
2. Open Dashboard -> Workspace settings -> Developer -> Add key.
3. Create a named API key for the integration or agent.
4. Store the raw key securely. It is shown once.
5. Send requests with `Authorization: Bearer YOUR_API_KEY`.

Do not expose DialNexa API keys in browser code, public repositories, prompts, or logs.

## API Use

Use the stable v1 base URL for new integrations:

```text
https://api.dialnexa.com/v1
```

Use the OpenAPI specification before calling endpoints. The API supports agents, calls, call logs, batch calls, campaigns, workflows, phone numbers, voices, transcribers, LLMs, languages, webhooks, and API keys.

## Useful Tasks

- Discover API endpoints and schemas from the OpenAPI specification.
- Read authentication requirements before generating code.
- Use docs pages ending in `.md` when markdown is preferred.
- Use `llms.txt` indexes to discover site and docs pages.
- For webhook receivers, verify DialNexa signatures as documented before trusting payloads.

## Boundaries

- Do not attempt to create accounts or API keys without explicit user approval.
- Do not guess credentials, workspace IDs, agent IDs, campaign IDs, or webhook secrets.
- Do not run destructive API operations unless the user explicitly asks for that action and provides the required identifiers.
