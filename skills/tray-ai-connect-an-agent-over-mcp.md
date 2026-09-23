---
name: tray-ai-connect-an-agent-over-mcp
description: >-
  Connect an MCP client (Claude Code, Claude Desktop, Cursor, Windsurf, Codex, or a custom agent) to
  Tray's hosted MCP server so it can build, validate, run and debug Tray workflows, and call any of
  Tray's 700+ connectors as tools. Use this when an agent needs to operate Tray itself rather than
  call the REST API.
api: Tray MCP Server
endpoint: https://api.tray.io/mcp
auth: OAuth 2.1 authorization_code + PKCE S256, dynamic client registration
operations:
  - list_connectors
  - list_connector_operations
  - call_connector
  - list_authentications
  - list_service_environments
  - create_auth_collection
  - check_auth_completion
  - create_project
  - list_projects
  - create_workflow
  - get_workflow
  - add_workflow_steps
  - update_workflow_steps
  - update_workflow_structure
  - update_workflow_metadata
  - remove_workflow_step
  - validate_workflow
  - trigger_workflow
  - list_workflow_executions
  - get_workflow_execution
  - get_workflow_step_detail
generated: '2026-09-02'
method: generated
source: mcp/tray-ai-mcp.yml, mcp/tray-ai-tool-crosswalk.yml, scopes/tray-ai-scopes.yml, skills/_published/
---

# Connect an agent to Tray over MCP

Tray runs a first-party hosted MCP server. This is the agent-native door onto Tray, and it is a
different surface from the REST API — see `mcp/tray-ai-tool-crosswalk.yml` for exactly where they
overlap (they barely do).

## Pick an endpoint — by region

| Region | Endpoint |
|---|---|
| US | `https://api.tray.io/mcp` |
| EU | `https://api.eu1.tray.io/mcp` |
| APAC | `https://api.ap1.tray.io/mcp` |

Point at the endpoint that matches your workspace's region. The `tray-workflows` plugin for Claude
Code and Codex is **US-only** and is not region-aware; use the raw server for EU/APAC.

## Authenticate — OAuth2, and do not shortcut it

**Do not send an `Authorization` header.** A static token bypasses the interactive sign-in and you
will not get a workspace bound to your session.

The server is a conformant RFC 9728 protected resource. An unauthenticated call returns:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer error="invalid_token",
  error_description="Missing Authorization header",
  scope="mcp:list_tools mcp:call_tools",
  resource_metadata="https://api.tray.io/.well-known/oauth-protected-resource/mcp"
```

Follow it:

- Protected resource metadata: `https://api.tray.io/.well-known/oauth-protected-resource/mcp`
- Authorization server: `https://auth.tray.io`
- Metadata: `https://auth.tray.io/.well-known/oauth-authorization-server`
- Authorize: `https://auth.tray.io/server/oauth2/authorize`
- Token: `https://auth.tray.io/server/oauth2/token`
- Register (DCR, RFC 7591): `https://auth.tray.io/server/oauth2/register`
- Revoke: `https://auth.tray.io/server/oauth2/revoke`
- PKCE: **S256 required**. `plain` is not offered.
- Scopes: `mcp:list_tools`, `mcp:call_tools` (and `api:full` for the broader API grant).

There is **no OIDC discovery document** — `/.well-known/openid-configuration` 404s on both hosts.
This is OAuth 2.0/2.1 only.

You choose the target workspace during sign-in and it is bound to the session. Since 2026-07-08
there is no `workspaceId` argument on tool calls. To switch workspaces, sign in again.

Minimal client config:

```json
{ "mcpServers": { "tray": { "type": "http", "url": "https://api.tray.io/mcp" } } }
```

## The API-token alternative (Agent Gateway)

For clients that cannot do OAuth2, Tray supports a static bearer token against a per-workspace
Agent Gateway server at `https://{workspace-id}.mcp.tray.ai`. Configure it with
`npx @trayio/tray-mcp --workspace-id <UUID> --api-token <TOKEN> --client claude|cursor|windsurf|vscode`.

The trade-off is real: **API-token connections cannot use dynamic (user-provided) tool
authentication**, so every tool must run under a shared service account. Use OAuth2 when actions
need to execute with the end user's own permissions and be auditable back to that person.

## What the tools do

Discover with `tools/list` once authenticated. The published surface groups as:

- **Connectors** — `list_connectors` (search), `list_connector_operations` (schemas; compacted by
  default, pass `expand: ['<prop>']` to open a `_collapsed` branch, `include_advanced: true` only
  when needed), `call_connector`.
- **Authentication** — `list_authentications` (filter on `service_name`, not keyword `search`),
  `list_service_environments` (`service_name` + integer `service_version`), `create_auth_collection`
  (`service` UUID + `service_environment_id` + `scopes`), `check_auth_completion`.
- **Projects** — `create_project`, `list_projects`.
- **Workflows** — `create_workflow`, `get_workflow`, `add_workflow_steps`, `update_workflow_steps`,
  `update_workflow_structure`, `update_workflow_metadata`, `remove_workflow_step`.
- **Validation** — `validate_workflow` (whole-workflow structural audit: jsonpath resolution,
  output-shape rules, structural conventions).
- **Run and debug** — `trigger_workflow`, `list_workflow_executions`, `get_workflow_execution`,
  `get_workflow_step_detail`.

## Guardrails you must set yourself

Tray states it plainly: **these tools act in your Tray organization as you.** They can create,
modify and delete projects, workflows and authentications, and run workflows with real side
effects. The packaged `tray-workflows` plugin surfaces destructive actions for confirmation. A raw
client applies only the guardrails you give it.

At minimum, require confirmation for `remove_workflow_step`, any workflow deletion, and
`trigger_workflow` against a production workspace. None of those has a documented undo through the
API.

## Limits to design around

- Callable depth ≤ 5 levels; ≤ 20 cumulative callables across all levels (Agent Gateway workflow
  tools). Exceeding either fails the tool call immediately and breaks the Authentication Management
  tab.
- No hard tool-count limit, but Tray documents noticeable degradation in client tool-selection
  accuracy beyond 15–20 tools. Split into multiple servers per use case or team.
- A user's dynamic-authentication credential mapping is valid for 7 days; the only reset before
  expiry is to disconnect and reconnect the server.
- OAuth2 client support is expanding but Tray currently names Claude Desktop as the supported OAuth2
  client for Agent Gateway; the API-token path works with all MCP-compatible clients.

## Provider-published skills

Tray publishes its own Agent Skills for this server in `github.com/trayio/tray-plugins`
(Apache-2.0). Verbatim copies live in `skills/_published/` in this repo: `build-workflow`,
`research-connector`, `tray-connectors`, `tray-gotchas`, `tray-patterns`. Prefer those over
improvising a build process.
