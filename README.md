# Tray.ai (tray-ai)

Tray.ai (formerly Tray.io) is an AI-ready enterprise orchestration platform for data and AI, combining a Merlin Agent Builder for no-code AI agent creation, an Agent Gateway for governed MCP server management, and an intelligent iPaaS with 700+ pre-built connectors. It exposes a REST Platform API (Connectivity API) and a GraphQL Embedded API for building, embedding, and operating AI agents and integration automations at enterprise scale.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Automation
- Integration
- iPaaS
- AI Agents
- MCP

## Timestamps

- **Created:** 2025-06-05
- **Modified:** 2026-05-22

## APIs

### Tray.ai Embedded API

The Tray.ai Embedded API is a GraphQL-based API that allows partners and customers to present in-app embedded integration experiences. It provides programmatic access to manage users, solutions, solution instances, authentications, workflows, and connector operations via HTTP POST to the GraphQL endpoint with Bearer token authentication. Two token types are supported, master tokens for admin operations and user tokens generated via the authorize mutation for user-scoped operations. All endpoints are rate limited to 30 requests per second.

- **Human URL:** [https://tray.ai/documentation/developer/openapi/embeddedapi-introduction/](https://tray.ai/documentation/developer/openapi/embeddedapi-introduction/)
- **Base URL:** `https://tray.io/graphql`

#### Tags

- Automation
- Embedded
- GraphQL
- Integration

#### Properties

- [Documentation](https://tray.ai/documentation/developer/openapi/embeddedapi-introduction/)
- [OpenAPI](openapi/tray-ai-embedded-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tray-ai-embedded-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/tray-ai-embedded-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](https://www.postman.com/tray-docs/tray-io-s-public-workspace/collection/uo51x8u/tray-embedded-apis-graphql) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [JSON Schema](json-schema/user.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/solution.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/solution-instance.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/authentication.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/tray-ai-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [JSON Structure](json-structure/tray-ai-solution-instance-structure.json)
- [Example](examples/tray-ai-create-solution-instance-example.json)

### Tray.ai Platform API

The Tray.ai Platform API (also known as the Connectivity API) provides direct programmatic REST access to Tray's 700+ pre-built service connectors, authentication management, trigger subscriptions, user and workspace administration, and project/solution lifecycle operations. It is grouped into Core, CDK (Connector Development Kit), and On Premise endpoint families served from the US, EU, and APAC regions. All endpoints require a Bearer token and are rate limited to 30 requests per second (burst 50), with the Call Connector endpoint additionally capped at 1,000 concurrent requests.

- **Human URL:** [https://tray.ai/documentation/developer/openapi/trayapi/overview/](https://tray.ai/documentation/developer/openapi/trayapi/overview/)
- **Base URL:** `https://api.tray.io/core/v1`

#### Tags

- Automation
- Connectors
- Integration
- iPaaS

#### Properties

- [Documentation](https://tray.ai/documentation/developer/openapi/trayapi/overview/)
- [OpenAPI](openapi/tray-ai-platform-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tray-ai-platform-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/tray-ai-platform-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/connector.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/authentication.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/subscription.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/user.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/workspace.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/tray-ai-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [JSON Structure](json-structure/tray-ai-connector-structure.json)
- [Example](examples/tray-ai-list-connectors-example.json)
- [Example](examples/tray-ai-call-connector-example.json)
- [Example](examples/tray-ai-create-authentication-example.json)
- [Spectral Ruleset](rules/tray-ai-rules.yml)

## Common Properties

- [GitHub Organization](https://github.com/trayio)
- [LinkedIn](https://www.linkedin.com/company/tray-ai)
- [Vocabulary](vocabulary/tray-ai-vocabulary.yml)
- [Plans](https://tray.ai/packages)
- [Plans Spec](plans/tray-ai-plans-pricing.yml)
- [Rate Limits](rate-limits/tray-ai-rate-limits.yml)
- [Fin Ops](finops/tray-ai-finops.yml)
- [Integrations](https://tray.ai/connectors?sort=alphabetical)
- [Login](https://app.tray.io/login)
- [Blog](https://tray.ai/blog)
- [Case Studies](https://tray.ai/customers)
- [Privacy Policy](https://tray.ai/privacy)
- [Terms of Service](https://tray.ai/terms)
- [Status Page](https://status.tray.ai/)
- [Atom Feed](https://status.tray.ai/history.atom)
- [R S S Feed](https://status.tray.ai/history.rss)
- [Website](https://tray.ai/)
- [Portal](https://tray.ai/documentation/developer/)
- [Product](https://tray.ai/documentation/agent-builder/)
- [Product](https://tray.ai/documentation/agent-hub/)
- [Product](https://tray.ai/)
- [Product](https://tray.ai/)
- [Product](https://tray.ai/products/embedded)
- [SDK](https://github.com/trayio/falafel)
- [SDK](https://github.com/trayio/threadneedle)
- [Samples](https://github.com/trayio/CDK-examples-public)
- [Samples](https://github.com/trayio/embedded-edition-sample-app)
- [Tools](https://github.com/trayio/connector-tester-public)
- [Tools](https://github.com/trayio/script-connector-tester)
- [Tools](https://github.com/trayio/embedded-customjs-public)
- [Postman Collection](https://www.postman.com/tray-docs/tray-io-s-public-workspace) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Use Cases](undefined)
- [Features](undefined)
- [Plan Tiers](undefined)
- [L L Ms Txt](https://tray.ai/llms.txt)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
