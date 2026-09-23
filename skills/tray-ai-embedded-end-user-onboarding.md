---
name: tray-ai-embedded-end-user-onboarding
description: >-
  Register one of your customers as a Tray end user, issue them a scoped user token, and stand up a
  configured Solution Instance so they can run a Tray integration from inside your own product. This
  is the Tray Embedded (GraphQL) flow — the partner-facing API, not the platform admin API.
api: Tray.ai Embedded API
base_url: https://tray.io/graphql
auth: 'Authorization: Bearer <master token, then user token>'
operations:
  - create-user
  - create-user-token
  - create-config-wizard-auth-code
  - get-solutions
  - create-solution-instance
  - get-solution-instances
  - update-solution-instance
  - get-authentications
  - delete-solution-instance
generated: '2026-09-02'
method: generated
source: openapi/_original/tray-ai-embedded-api-published-openapi.yaml, components/tray-ai-components.yml
---

# Onboard an end user onto a Tray Embedded solution

Every operation is a `POST https://tray.io/graphql` (EU: `https://eu1.tray.io/graphql`, APAC:
`https://ap1.tray.io/graphql`) with a GraphQL document in the body and a bearer token in the header.

The token you send decides what you are allowed to do:

- **master token** — acts as your organization. Needed to create users and mint user tokens.
- **user token** — acts as one end user. Needed for anything touching that user's authentications or
  solution instances.

Switching tokens mid-flow is the normal shape of this API, not a mistake.

## Step 1 — register the end user (master token)

`create-user` — the `createExternalUser` mutation. Send your own `externalUserId` (your internal
user id) and a `name`. You get back a Tray `userId`. Store the mapping; `externalUserId` is how you
find this user again.

```bash
curl --location 'https://tray.io/graphql' \
  --header 'Authorization: Bearer <master token>' \
  --header 'Content-Type: application/json' \
  --data '{"query":"mutation($externalUserId: String!, $name: String!) { createExternalUser(input: { name: $name, externalUserId: $externalUserId }) { userId } }","variables":{"name":"myCustomersName","externalUserId":"my-apps-internal-user-id"}}'
```

## Step 2 — mint a user token (master token)

`create-user-token` — the `authorize` mutation. Exchange the master token plus the `userId` for a
short-lived user token. Every subsequent step uses this token.

Never ship the master token to a browser. Mint the user token server-side and hand only that to your
front end.

## Step 3 — list what the user can install (user token)

`get-solutions` — returns the Solutions published to your partner account, each with its
`configSlots` (values the user must supply) and `authSlots` (services the user must authenticate).

## Step 4 — create the Solution Instance (user token)

`create-solution-instance` — creates the user's own copy of the solution. This is the object that
actually runs; the Solution itself is a template.

## Step 5 — let the user fill in the slots

Two options:

- **Config Wizard (hosted).** Open `https://embedded.tray.io/external/solutions/...` for the new
  instance and let Tray's own UI collect auths and config values. Region-specific hosts:
  `embedded.eu1.tray.io`, `embedded.ap1.tray.io`.
- **Custom form (yours).** Render the slots yourself and use `create-config-wizard-auth-code` to open
  Tray's auth-only dialog per auth slot. Listen for `tray.authpopup.finish` on
  `window.addEventListener("message", ...)` and capture the returned `authId`; also handle
  `tray.authPopup.error` and `tray.authpopup.close`. Open the popup from a real user gesture or the
  browser will block it.

See `components/tray-ai-components.yml` for the URL shapes and the full event list.

## Step 6 — enable and verify

`update-solution-instance` to set `enabled: true`, then `get-solution-instances` to confirm the
instance's state and read its workflow instances. Each workflow instance has an auto-generated public
URL (`{uuid}.trayapp.io`, or your own `*.integration-hook.com` if you have de-branded it) that third
parties call to trigger it.

## Step 7 — tear down

`delete-solution-instance`, and `delete-authentication` for any auth you created. Both are
irreversible — no restore, no retention window is documented. Export anything you need first.

## Conventions that apply to this whole flow

- No idempotency keys. A retried `createExternalUser` creates a second user.
- No pagination on any of these queries.
- Errors are `{"message": "...", "code": null}` with 401 / 403 / 500 the only statuses the Embedded
  spec declares. A GraphQL-shaped `errors[]` array can also come back inside a 200 — check the body.
- 30 requests/second, 1,800/minute. No rate-limit response headers.
