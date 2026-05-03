# Tray.ai

Tray.ai is an AI-ready integration and automation platform that helps enterprises connect systems, teams, and data. It provides 700+ pre-built connectors, a visual workflow builder, embedded integration capabilities, and programmatic APIs for building and managing integrations at scale.

**URL:** [https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Automation, Integration, iPaaS

## Timestamps

- **Created:** 2025-06-05
- **Modified:** 2026-05-03

## APIs

### Tray.ai Embedded API

The Tray.ai Embedded API is a GraphQL-based API that allows partners and customers to present in-app embedded integration experiences. It provides programmatic access to manage users, solutions, solution instances, authentications, workflows, and connector operations via HTTP POST to the GraphQL endpoint with Bearer token authentication.

**Human URL:** [https://developer.tray.ai/openapi/embeddedapi-introduction/](https://developer.tray.ai/openapi/embeddedapi-introduction/)
**Base URL:** `https://tray.io/graphql`

#### Tags

- Automation, Embedded, GraphQL, Integration

#### Properties

- [Documentation](https://developer.tray.ai/openapi/embeddedapi-introduction/)
- [OpenAPI](openapi/tray-ai-embedded-api-openapi.yml)
- [PostmanCollection](https://www.postman.com/tray-docs/tray-io-s-public-workspace/collection/uo51x8u/tray-embedded-apis-graphql)
- [JSONSchema - User](json-schema/user.json)
- [JSONSchema - Solution](json-schema/solution.json)
- [JSONSchema - Solution Instance](json-schema/solution-instance.json)
- [JSONSchema - Authentication](json-schema/authentication.json)
- [JSONLD](json-ld/tray-ai-context.jsonld)
- [JSONStructure](json-structure/tray-ai-solution-instance-structure.json)
- [Example - Create Solution Instance](examples/tray-ai-create-solution-instance-example.json)
- [NaftikoCapability](capabilities/shared/embedded-api.yaml)

### Tray.ai Platform API

The Tray.ai Platform API (also known as the Connectivity API) provides direct programmatic REST access to Tray's 700+ pre-built service connectors, authentication management, trigger subscriptions, user and workspace administration, and project/solution lifecycle operations. It enables developers to integrate third-party service operations into their own applications without using the Builder UI.

**Human URL:** [https://developer.tray.ai/openapi/trayapi/overview/](https://developer.tray.ai/openapi/trayapi/overview/)
**Base URL:** `https://api.tray.io/core/v1`

#### Tags

- Automation, Connectors, Integration, iPaaS

#### Properties

- [Documentation](https://developer.tray.ai/openapi/trayapi/overview/)
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
- [NaftikoCapability](capabilities/shared/platform-api.yaml)

## Naftiko Capabilities

### Workflow Capabilities

| Capability | Description | Tools |
|------------|-------------|-------|
| [Integration Automation](capabilities/integration-automation.yaml) | Full Platform + Embedded API composition for integration automation workflows | 17 tools |

### Shared Definitions

| Capability | Description |
|------------|-------------|
| [Platform API](capabilities/shared/platform-api.yaml) | Connectors, authentication, triggers, users, workspaces |
| [Embedded API](capabilities/shared/embedded-api.yaml) | Users, solutions, solution instances, workflows |

## Vocabulary

- [tray-ai-vocabulary.yml](vocabulary/tray-ai-vocabulary.yml) — Domain vocabulary for connectors, solutions, embedded integrations, and iPaaS concepts

## Common Properties

- [Plans](https://tray.ai/packages)
- [Integrations](https://tray.ai/connectors?sort=alphabetical)
- [Login](https://app.tray.io/login)
- [Blog](https://tray.ai/blog)
- [CaseStudies](https://tray.ai/customers)
- [PrivacyPolicy](https://tray.ai/privacy)
- [TermsOfService](https://tray.ai/terms)
- [Status](https://status.tray.ai/)
- [Website](https://tray.ai/)
- [Portal](https://developer.tray.ai/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
