---
name: tray-ai-subscribe-to-trigger-events
description: >-
  Subscribe to third-party events through the Tray.ai Trigger API and receive normalised,
  HMAC-signed webhook deliveries at your own endpoint. Use this when an agent needs to react to
  changes in a SaaS system (a new Salesforce record, a submitted form, a Slack message) without
  polling and without registering a webhook with each vendor separately.
api: Tray.ai Platform API
base_url: https://api.tray.io/core/v1
auth: 'Authorization: Bearer <master token or user token>'
operations:
  - get-triggers
  - get-trigger-operations
  - create-subscription
  - get-subscriptions
  - get-subscription-by-id
  - delete-connector-events-subscription
generated: '2026-09-02'
method: generated
source: openapi/_original/tray-ai-platform-api-published-openapi.yaml, asyncapi/tray-ai-webhooks.yml
---

# Subscribe to third-party events with the Tray Trigger API

Tray sits between you and the vendor: it registers the vendor webhook, normalises the payload to the
trigger operation's **output schema**, signs it, and posts it to an endpoint you own.

There is no MCP tool for any of this. The Trigger API is REST-only.

## Step 1 — find the trigger

`get-triggers` → `GET /core/v1/triggers`

## Step 2 — read the trigger operation

`get-trigger-operations` → `GET /core/v1/triggers/{trigger-name}/versions/{trigger-version}/operations`

Read the operation's `inputSchema` (what the subscription needs to be configured with) and its
`outputSchema` (**the shape of the events you will receive** — code against this, not against the
vendor's raw payload).

## Step 3 — create the subscription

`create-subscription` → `POST /core/v1/subscriptions`

Body fields:

| Field | Notes |
|---|---|
| `name` | Display name. |
| `externalId` | Your own unique id for this subscription. Store it — it is how you find the subscription again. |
| trigger `name` + `version` | From step 1. |
| `authenticationId` | The auth the subscription runs under. |
| `operation` | From step 2. |
| `input` | JSON matching the trigger operation's input schema. |
| `endpoint` | The URL Tray delivers events to. |

**Capture `signingKey` from the response and store it against the subscription id, in the same
transaction.** It is returned exactly once, at creation. `get-subscriptions` and
`get-subscription-by-id` will never return it. Lose it and the subscription is permanently
unverifiable — your only remedy is to delete and recreate.

## Step 4 — verify every delivery

Tray signs the raw payload with HMAC-SHA256 using the base64 `signingKey`, and sends the result in
the `x-tray-signature` header.

```js
const crypto = require("crypto");

const generateHMAC = (signingKey, requestBody) => {
  const signingKeyBuffer = Buffer.from(signingKey, "base64");
  return crypto
    .createHmac("sha256", signingKeyBuffer)
    .update(requestBody, "utf-8") // requestBody is the event payload in PLAIN TEXT
    .digest("base64");
};
```

Compare against `x-tray-signature` before you process anything. Tray calls this optional; treat it
as mandatory — the endpoint is public.

Sign over the **raw body bytes**, before any JSON parse/re-serialise round trip.

## Step 5 — size your receiver

Trigger event delivery is **not** rate limited. Tray delivers as fast as it can. If your endpoint
rate-limits, Tray retries with exponential backoff and states no events are lost — but you are the
one who has to absorb the burst.

Tray's own guidance: process events in **your** infrastructure. If you want to process them inside
Tray, use Tray Embedded directly and skip the round trip.

## Step 6 — clean up

`delete-connector-events-subscription` → `DELETE /core/v1/subscriptions/{subscription-id}`

This is irreversible. There is no restore and no way to recover the signing key.

## What is missing

No replay API, no dead-letter queue, no event-type registry, and no AsyncAPI document. If you need
to reprocess a missed window, you need your own durable log of what arrived.
