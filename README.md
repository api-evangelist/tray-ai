# Tray.ai

Tray.ai (formerly Tray.io) is an AI-ready enterprise orchestration platform for data and AI, combining a Merlin Agent Builder for no-code AI agent creation, an Agent Gateway for governed MCP server management, and an intelligent iPaaS with 700+ pre-built connectors. It exposes a REST Platform API (Connectivity API) and a GraphQL Embedded API for building, embedding, and operating AI agents and integration automations at enterprise scale.

**URL:** [https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

Automation, Integration, iPaaS, AI Agents, MCP

## Timestamps

- **Created:** 2025-06-05
- **Modified:** 2026-05-22

## APIs

### Tray.ai Embedded API

The Tray.ai Embedded API is a GraphQL-based API that allows partners and customers to present in-app embedded integration experiences. It provides programmatic access to manage users, solutions, solution instances, authentications, workflows, and connector operations via HTTP POST to the GraphQL endpoint with Bearer token authentication. Two token types are supported: master tokens for admin operations and user tokens generated via the `authorize` mutation for user-scoped operations. All endpoints are rate limited to 30 requests per second.

**Human URL:** [https://tray.ai/documentation/developer/openapi/embeddedapi-introduction/](https://tray.ai/documentation/developer/openapi/embeddedapi-introduction/)
**Base URL:** `https://tray.io/graphql`

#### Tags

Automation, Embedded, GraphQL, Integration

#### Properties

- [Documentation](https://tray.ai/documentation/developer/openapi/embeddedapi-introduction/)
- [OpenAPI](openapi/tray-ai-embedded-api-openapi.yml)
- [PostmanCollection](https://www.postman.com/tray-docs/tray-io-s-public-workspace/collection/uo51x8u/tray-embedded-apis-graphql)
- [JSONSchema - User](json-schema/user.json)
- [JSONSchema - Solution](json-schema/solution.json)
- [JSONSchema - Solution Instance](json-schema/solution-instance.json)
- [JSONSchema - Authentication](json-schema/authentication.json)
- [JSONLD](json-ld/tray-ai-context.jsonld)
- [JSONStructure](json-structure/tray-ai-solution-instance-structure.json)
- [Example - Create Solution Instance](examples/tray-ai-create-solution-instance-example.json)

### Tray.ai Platform API

The Tray.ai Platform API (also known as the Connectivity API) provides direct programmatic REST access to Tray's 700+ pre-built service connectors, authentication management, trigger subscriptions, user and workspace administration, and project/solution lifecycle operations. It is grouped into Core, CDK (Connector Development Kit), and On Premise endpoint families served from the US, EU, and APAC regions. All endpoints require a Bearer token and are rate limited to 30 requests per second (burst 50), with the Call Connector endpoint additionally capped at 1,000 concurrent requests.

**Human URL:** [https://tray.ai/documentation/developer/openapi/trayapi/overview/](https://tray.ai/documentation/developer/openapi/trayapi/overview/)
**Base URL:** `https://api.tray.io/core/v1`

#### Tags

Automation, Connectors, Integration, iPaaS

#### Properties

- [Documentation](https://tray.ai/documentation/developer/openapi/trayapi/overview/)
- [OpenAPI](openapi/tray-ai-platform-api-openapi.yml)
- [JSONSchema - Connector](json-schema/connector.json)
- [JSONSchema - Authentication](json-schema/authentication.json)
- [JSONSchema - Subscription](json-schema/subscription.json)
- [JSONSchema - User](json-schema/user.json)
- [JSONSchema - Workspace](json-schema/workspace.json)
- [JSONLD](json-ld/tray-ai-context.jsonld)
- [JSONStructure](json-structure/tray-ai-connector-structure.json)
- [Example - List Connectors](examples/tray-ai-list-connectors-example.json)
- [Example - Call Connector](examples/tray-ai-call-connector-example.json)
- [Example - Create Authentication](examples/tray-ai-create-authentication-example.json)
- [SpectralRuleset](rules/tray-ai-rules.yml)

## Naftiko Capabilities

### Embedded API

| Capability | File |
|---|---|
| Authentication (authorize) | [capabilities/embedded-authentication.yaml](capabilities/embedded-authentication.yaml) |
| Authentications | [capabilities/embedded-authentications.yaml](capabilities/embedded-authentications.yaml) |
| Call Connector | [capabilities/embedded-call-connector.yaml](capabilities/embedded-call-connector.yaml) |
| Solution Instances | [capabilities/embedded-solution-instances.yaml](capabilities/embedded-solution-instances.yaml) |
| Solutions | [capabilities/embedded-solutions.yaml](capabilities/embedded-solutions.yaml) |
| Users | [capabilities/embedded-users.yaml](capabilities/embedded-users.yaml) |
| Workflows | [capabilities/embedded-workflows.yaml](capabilities/embedded-workflows.yaml) |

### Platform API

| Capability | File |
|---|---|
| Authentications | [capabilities/platform-authentications.yaml](capabilities/platform-authentications.yaml) |
| Connectors | [capabilities/platform-connectors.yaml](capabilities/platform-connectors.yaml) |
| Deployments (CDK) | [capabilities/platform-deployments.yaml](capabilities/platform-deployments.yaml) |
| Projects | [capabilities/platform-projects.yaml](capabilities/platform-projects.yaml) |
| Triggers | [capabilities/platform-triggers.yaml](capabilities/platform-triggers.yaml) |
| Users | [capabilities/platform-users.yaml](capabilities/platform-users.yaml) |
| Workspaces | [capabilities/platform-workspaces.yaml](capabilities/platform-workspaces.yaml) |

## Commercial Surface

- [Plans & Pricing (human)](https://tray.ai/packages) — Pro, Team, Enterprise. List prices are **not published**; Tray quotes by usage and feature mix and routes all tiers to "Talk to sales".
- [Plans (machine-readable)](plans/tray-ai-plans-pricing.yml) — API Commons Plans 0.1
- [Rate Limits](rate-limits/tray-ai-rate-limits.yml) — 30 RPS steady-state, burst 50, 1,000 concurrent Call Connector
- [FinOps Profile](finops/tray-ai-finops.yml) — FOCUS 1.3 aligned

## Vocabulary & Semantics

- [tray-ai-vocabulary.yml](vocabulary/tray-ai-vocabulary.yml) — Domain vocabulary for connectors, solutions, embedded integrations, and iPaaS concepts
- [tray-ai-context.jsonld](json-ld/tray-ai-context.jsonld) — JSON-LD context for Tray entities

## Common Properties

- [Website](https://tray.ai/) — "Stop wrangling AI. Start orchestrating it."
- [Developer Portal](https://tray.ai/documentation/developer/)
- [Connector Hub](https://tray.ai/connectors?sort=alphabetical) — 700+ connectors
- [Login](https://app.tray.io/login)
- [Blog](https://tray.ai/blog)
- [Status Page](https://status.tray.ai/) — Atlassian Statuspage with [Atom](https://status.tray.ai/history.atom) and [RSS](https://status.tray.ai/history.rss) feeds
- [Case Studies](https://tray.ai/customers)
- [Privacy](https://tray.ai/privacy)
- [Terms](https://tray.ai/terms)
- [GitHub Org](https://github.com/trayio) — Falafel, Threadneedle, CDK-examples-public, embedded-edition-sample-app, connector-tester-public, script-connector-tester

## Products

- **Merlin Agent Builder** — No-code AI agent creation with reasoning, guardrails, and a composable hub.
- **Agent Gateway for MCP** — Managed MCP servers exposing Tray's 700+ connectors as governed agent tools with audit and observability.
- **Agent Hub** — Catalog of agent tools, accelerators, and data sources for building intelligent agents.
- **Universal Automation Cloud / Intelligent iPaaS** — Process automation, data integration, and API management on 700+ connectors.
- **Tray.ai Embedded** — Embedded iPaaS for SaaS vendors to ship in-app integration experiences.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
