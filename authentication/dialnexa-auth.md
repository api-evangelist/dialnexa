# DialNexa auth.md

DialNexa supports agent and integration access through dashboard-provisioned API keys. Public OAuth client registration and token issuance are not currently available for the DialNexa public API.

## Agent Audience

This file is for AI agents, automation systems, and developer tools that need to discover how to authenticate with DialNexa APIs.

## Registration And Provisioning

Create API credentials from the DialNexa dashboard:

1. Sign in at https://app.dialnexa.com/auth/login.
2. Open https://app.dialnexa.com/dashboard/workspace.
3. Open Dashboard -> Workspace settings -> Developer -> Add key.
4. Create a named API key for the agent, integration, or environment.
5. Copy the raw API key immediately and store it in a secret manager.
6. Use one key per environment and rotate keys intentionally.

Registration URI:

```text
https://app.dialnexa.com/dashboard/workspace
```

API authentication docs:

```text
https://dialnexa.com/docs/api-reference/authentication.md
```

## Credential Use

Send the full API key in the HTTP Authorization header:

```http
Authorization: Bearer YOUR_API_KEY
```

The production v1 API base URL is:

```text
https://api.dialnexa.com/v1
```

## Machine-Readable Auth Metadata

- OAuth Protected Resource Metadata: https://dialnexa.com/.well-known/oauth-protected-resource
- OAuth Authorization Server Metadata: https://dialnexa.com/.well-known/oauth-authorization-server
- API catalog: https://dialnexa.com/.well-known/api-catalog
- OpenAPI specification: https://dialnexa.com/docs/api-reference/openapi.json

## agent_auth

```yaml
agent_auth:
  skill: https://dialnexa.com/.well-known/agent-skills/dialnexa/SKILL.md
  register_uri: https://app.dialnexa.com/dashboard/workspace
  registration_instructions: Sign in at https://app.dialnexa.com/auth/login, then open Dashboard -> Workspace settings -> Developer -> Add key.
  methods:
    - type: api_key_bearer
      identity_types_supported:
        - account_api_key
      credential_types_supported:
        - api_key
      documentation_uri: https://dialnexa.com/docs/api-reference/authentication.md
      authorization_header: "Authorization: Bearer YOUR_API_KEY"
```

## Security Requirements

- Do not put API keys in client-side website code.
- Do not commit API keys to source control.
- Do not paste API keys into prompts, tickets, or logs.
- Revoke and replace any key that may have been exposed.
