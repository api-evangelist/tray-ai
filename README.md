# Tray.ai (tray-ai)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
