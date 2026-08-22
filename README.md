# WordPress (wordpress)

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

WordPress is an open-source content management system (CMS) that powers a significant portion of websites on the internet. Its REST API enables applications to interact with WordPress sites by sending and receiving data as JSON, allowing developers to build decoupled frontends, mobile apps, and integrations in any language. The extensive plugin and theme ecosystem, block editor, and AI capabilities make it accessible for building everything from personal blogs to complex enterprise websites.

**APIs.json:** [https://developer.wordpress.org/rest-api/](https://developer.wordpress.org/rest-api/)

## Scope

- **Type:** Index

## Tags

- CMS
- Content Management
- Open Source
- WordPress

## Timestamps

- **Created:** 2025
- **Modified:** 2026-05-19

## APIs

### WordPress REST API

The WordPress REST API provides endpoints for WordPress data types that allow developers to interact with sites remotely by sending and receiving JSON objects. The REST API is the backbone of the WordPress Block Editor (Gutenberg) and enables building decoupled applications, headless CMS setups, and third-party integrations.

- **Human URL:** [https://developer.wordpress.org/rest-api/](https://developer.wordpress.org/rest-api/)
- **Base URL:** `https://{site}/wp-json`

#### Tags

- CMS
- Content
- Posts
- REST
- WordPress

#### Properties

- [Documentation](https://developer.wordpress.org/rest-api/)
- [API Reference](https://developer.wordpress.org/rest-api/reference/)
- [Authentication](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/)
- [Getting Started](https://developer.wordpress.org/rest-api/using-the-rest-api/)
- [OpenAPI](openapi/wordpress-rest-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/wordpress-rest-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/wordpress-rest-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/wordpress-post-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-page-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-media-item-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-comment-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-user-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-term-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-settings-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-theme-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-plugin-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-block-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-block-type-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-post-type-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-search-result-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/wordpress-rendered-content-schema.json) — [JSON Schema](https://json-schema.org/specification)

### WP-CLI

WP-CLI is the command-line interface for WordPress. It provides commands for managing WordPress installations, plugins, themes, users, content, and more without using a web browser. WP-CLI is widely used for automation, deployment, and development workflows.

- **Human URL:** [https://wp-cli.org/](https://wp-cli.org/)

#### Tags

- CLI
- Command Line
- DevOps
- WordPress

#### Properties

- [Documentation](https://wp-cli.org/)
- [API Reference](https://developer.wordpress.org/cli/commands/)
- [GitHub Repository](https://github.com/wp-cli/wp-cli)
- [C L I](https://wp-cli.org/)
- [Postman Collection](collections/wordpress-rest-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/wordpress-rest-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### WordPress Block Editor API

The Block Editor API (Gutenberg) enables developers to create custom blocks, block patterns, block templates, and editor plugins for the WordPress Block Editor. It includes JavaScript and PHP APIs for registering block types, modifying editor behavior, and extending the editing experience.

- **Human URL:** [https://developer.wordpress.org/block-editor/](https://developer.wordpress.org/block-editor/)

#### Tags

- Block Editor
- Gutenberg
- JavaScript
- WordPress

#### Properties

- [Documentation](https://developer.wordpress.org/block-editor/)
- [API Reference](https://developer.wordpress.org/block-editor/reference-guides/)
- [GitHub Repository](https://github.com/WordPress/gutenberg)
- [Getting Started](https://developer.wordpress.org/block-editor/getting-started/)
- [Postman Collection](collections/wordpress-rest-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/wordpress-rest-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### WordPress AI API

WordPress AI API provides a provider-agnostic interface for integrating generative AI capabilities into WordPress plugins and themes. It supports multiple AI providers (OpenAI, Google, Anthropic) through a unified PHP client interface and includes an MCP adapter for bridging to the Model Context Protocol.

- **Human URL:** [https://github.com/WordPress/wp-ai-client](https://github.com/WordPress/wp-ai-client)

#### Tags

- AI
- Generative AI
- MCP
- WordPress

#### Properties

- [Documentation](https://github.com/WordPress/wp-ai-client)
- [GitHub Repository](https://github.com/WordPress/wp-ai-client)
- [Tools](https://github.com/WordPress/mcp-adapter)
- [Postman Collection](collections/wordpress-rest-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/wordpress-rest-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Arazzo Workflows](arazzo/) — [Arazzo Specification](https://spec.openapis.org/arazzo/latest.html)
- [Portal](https://developer.wordpress.org/)
- [GitHub Organization](https://github.com/WordPress)
- [GitHub Repository](https://github.com/WordPress/wordpress-develop)
- [Documentation](https://developer.wordpress.org/)
- [Getting Started](https://developer.wordpress.org/rest-api/using-the-rest-api/)
- [Blog](https://developer.wordpress.org/news/)
- [Changelog](https://wordpress.org/documentation/article/wordpress-versions/)
- [Support](https://wordpress.org/support/)
- [Status Page](https://www.incsub.com/status/)
- [Terms of Service](https://wordpress.org/about/license/)
- [Privacy Policy](https://automattic.com/privacy/)
- [Security](https://wordpress.org/about/security/)
- [Training](https://learn.wordpress.org/)
- [Support](https://wordpress.org/support/forums/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/wordpress)
- [SDK](https://github.com/WordPress/php-toolkit)
- [Spectral Rules](rules/wordpress-spectral-rules.yml)
- [Vocabulary](vocabulary/wordpress-vocabulary.yml)
- [JSON-LD](json-ld/wordpress-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Features](undefined)
- [Use Cases](undefined)
- [Integrations](undefined)
- [M C P Server](https://github.com/WordPress/mcp-adapter)
- [Agent Skill](https://github.com/WordPress/agent-skills)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
