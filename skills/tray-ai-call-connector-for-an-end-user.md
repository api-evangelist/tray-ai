---
name: tray-ai-call-connector-for-an-end-user
description: >-
  Call any of Tray.ai's 700+ third-party connector operations on behalf of a stored end-user
  authentication, using the Tray Platform (Connectivity) API. Use this when an agent needs to read
  or write data in Salesforce, Slack, Google Sheets, NetSuite or any other Tray-supported service
  without building a direct integration.
api: Tray.ai Platform API
base_url: https://api.tray.io/core/v1
auth: 'Authorization: Bearer <master token or user token>'
operations:
  - get-connectors
  - get-connector-operations
  - get-service-environments
  - create-user-authentication
  - get-user-authentication
  - call-connector
generated: '2026-09-02'
method: generated
source: openapi/_original/tray-ai-platform-api-published-openapi.yaml, conventions/tray-ai-conventions.yml, errors/tray-ai-problem-types.yml
---

# Call a Tray connector on behalf of an end user

Tray's Call Connector endpoint is a single door onto every service Tray has a connector for. You
never learn the third party's API — you learn Tray's, once.

## Before you start

- Region is chosen by HOST, not by a header: `https://api.tray.io/core/v1` (US),
  `https://api.eu1.tray.io/core/v1` (EU), `https://api.ap1.tray.io/core/v1` (APAC). A token issued
  in one region does not work in another.
- Every request is `Authorization: Bearer <token>`. A **master token** acts as the organization; a
  **user token** acts as one end user. Use a user token for anything that touches an end user's
  data.
- There are no OAuth scopes on this API. Authority comes from the token type and the RBAC role.

## Step 1 — find the connector

`get-connectors` → `GET /core/v1/connectors`

Record the exact `name` and the `version` you intend to pin. Connector versions are a first-class
concept in Tray and operations change between them; pin the version, do not float.

## Step 2 — read the operation's input schema

`get-connector-operations` → `GET /core/v1/connectors/{connector-name}/versions/{connector-version}/operations`

This is the contract you actually have to satisfy. Read:

- `inputSchema.required` — the fields you must send.
- `inputSchema.properties` — types. Tray validates types strictly; sending `"100"` where an integer
  is expected returns 400.
- `hasDynamicOutput` — whether the output shape depends on the input.
- any `lookup` object on a field — that field is a DDL (dynamic drop-down list) whose allowed values
  come from another connector operation, not from a static enum.

Do not guess field names from the vendor's own API documentation. Tray's input schema is Tray's, and
it is frequently different.

## Step 3 — make sure an authentication exists

If you already have an `authId`, confirm it with `get-user-authentication` →
`GET /core/v1/authentications/{authentication-id}`.

If you need a new one:

1. `get-service-environments` → `GET /core/v1/services/{service-name}/versions/{service-version}/environments`
   to find the `serviceEnvironmentId`.
2. `create-user-authentication` → `POST /core/v1/authentications`.

For an end-user flow, send the user through Tray's hosted auth dialog instead and capture the
`authId` from the `tray.authpopup.finish` postMessage event — see
`components/tray-ai-components.yml`.

## Step 4 — call the operation

`call-connector` → `POST /core/v1/connectors/{connector-name}/versions/{connector-version}/call`

```json
{
  "operation": "send_message",
  "authId": "af75xxxx-xxxx-xxxx-xxxx-xxxx58c494c5",
  "input": {
    "channel": "#general",
    "text": "Hello",
    "as_user": true
  },
  "returnOutputSchema": false
}
```

Set `returnOutputSchema: true` on the first call of a new operation if you need the output shape
back; set it false afterwards to keep responses small.

## Step 5 — read the result CORRECTLY

**This is the step agents get wrong.** A `200` means Tray's input validation and the authentication
passed. It does **not** mean the third-party call succeeded — the vendor's error comes back inside
the 200 body. Branch on the body's `outcome` field, not on the HTTP status.

```json
{ "outcome": "success", "output": { "total": 31, "next_page_offset": null, "records": [ ... ] } }
```

## Errors you will actually hit

| Status | Meaning | What to do |
|---|---|---|
| 400 | `Connector input validation failed. Schema validation errors: [...]` | Re-read the input schema. Do not retry unchanged. |
| 400 | `Couldn't decode a valid UUID at 'authId'` | The authId is malformed or does not exist. |
| 403 | `The request is forbidden` | The authId exists but has no access to that service. |
| 404 | Not found | Wrong connector name, wrong version, or wrong authId. |
| 408 / 409 | Timeout / concurrency conflict | Retryable with backoff. |
| 413 | Content too large | Reduce the payload; use Tray's temporary file storage for large files. |
| 429 | Limit exceeded | See rate limits below. |

Every error body is `{"message": "...", "code": null}`. `code` is null in every published example,
so you have to string-match `message`. There is no RFC 9457 problem+json here.

## Rate limits and retries

- 30 requests/second, 1,800 requests/minute across all endpoints.
- Burst tolerance up to 50 requests/second.
- Call Connector is governed by a **1,000 concurrent request** ceiling rather than a rate limit.
- Tray publishes **no** `RateLimit-*` or `Retry-After` response headers. You cannot read your
  remaining budget at runtime — model the published ceiling and back off exponentially with jitter.

## Pagination

Tray's own endpoints are not paginated. Pagination on a Call Connector result belongs to the third
party: look for `batch_size`, `page_offset` or `next_page_token` in the operation's input schema and
for `next_page_offset` / `total` in the output. The exact names differ per service.

## Idempotency

There is none. No `Idempotency-Key`, no idempotent retry semantics. A retried write re-executes.
Dedupe on your side before you retry a write.
