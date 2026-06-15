# WordPress (wordpress)

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
