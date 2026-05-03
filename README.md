# WordPress (wordpress)
WordPress is an open-source content management system (CMS) that powers a significant portion of websites on the internet. Its REST API enables applications to interact with WordPress sites by sending and receiving data as JSON, allowing developers to build decoupled frontends, mobile apps, and integrations in any language. The extensive plugin and theme ecosystem, block editor, and AI capabilities make it accessible for building everything from personal blogs to complex enterprise websites.

**URL:** [Visit Developer Portal](https://developer.wordpress.org/rest-api/)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - CMS, Content Management, Open Source, WordPress

## Timestamps

- **Created:** 2025
- **Modified:** 2026-05-03

## APIs

### WordPress REST API
The WordPress REST API provides endpoints for WordPress data types that allow developers to interact with sites remotely by sending and receiving JSON objects. The REST API is the backbone of the WordPress Block Editor (Gutenberg) and enables building decoupled applications, headless CMS setups, and third-party integrations.

**Human URL:** [https://developer.wordpress.org/rest-api/](https://developer.wordpress.org/rest-api/)

#### Tags:

 - CMS, Content, Posts, REST, WordPress

#### Properties

- [Documentation](https://developer.wordpress.org/rest-api/)
- [APIReference](https://developer.wordpress.org/rest-api/reference/)
- [Authentication](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/)
- [GettingStarted](https://developer.wordpress.org/rest-api/using-the-rest-api/)
- [OpenAPI](openapi/wordpress-rest-api-openapi.yml)
- [JSONSchema - Post](json-schema/wordpress-post-schema.json)
- [JSONSchema - Page](json-schema/wordpress-page-schema.json)
- [JSONSchema - MediaItem](json-schema/wordpress-media-item-schema.json)
- [JSONSchema - Comment](json-schema/wordpress-comment-schema.json)
- [JSONSchema - User](json-schema/wordpress-user-schema.json)
- [JSONSchema - Term](json-schema/wordpress-term-schema.json)
- [JSONSchema - Settings](json-schema/wordpress-settings-schema.json)
- [JSONSchema - Theme](json-schema/wordpress-theme-schema.json)
- [JSONSchema - Plugin](json-schema/wordpress-plugin-schema.json)
- [JSONSchema - Block](json-schema/wordpress-block-schema.json)
- [JSONSchema - BlockType](json-schema/wordpress-block-type-schema.json)
- [JSONSchema - PostType](json-schema/wordpress-post-type-schema.json)
- [JSONSchema - SearchResult](json-schema/wordpress-search-result-schema.json)

### WP-CLI
WP-CLI is the command-line interface for WordPress. It provides commands for managing WordPress installations, plugins, themes, users, content, and more without using a web browser.

**Human URL:** [https://wp-cli.org/](https://wp-cli.org/)

#### Tags:

 - CLI, Command Line, DevOps, WordPress

#### Properties

- [Documentation](https://wp-cli.org/)
- [APIReference](https://developer.wordpress.org/cli/commands/)
- [GitHubRepository](https://github.com/wp-cli/wp-cli)
- [CLI](https://wp-cli.org/)

### WordPress Block Editor API
The Block Editor API (Gutenberg) enables developers to create custom blocks, block patterns, block templates, and editor plugins for the WordPress Block Editor.

**Human URL:** [https://developer.wordpress.org/block-editor/](https://developer.wordpress.org/block-editor/)

#### Tags:

 - Block Editor, Gutenberg, JavaScript, WordPress

#### Properties

- [Documentation](https://developer.wordpress.org/block-editor/)
- [APIReference](https://developer.wordpress.org/block-editor/reference-guides/)
- [GitHubRepository](https://github.com/WordPress/gutenberg)
- [GettingStarted](https://developer.wordpress.org/block-editor/getting-started/)

### WordPress AI API
WordPress AI API provides a provider-agnostic interface for integrating generative AI capabilities into WordPress plugins and themes.

**Human URL:** [https://github.com/WordPress/wp-ai-client](https://github.com/WordPress/wp-ai-client)

#### Tags:

 - AI, Generative AI, MCP, WordPress

#### Properties

- [Documentation](https://github.com/WordPress/wp-ai-client)
- [GitHubRepository](https://github.com/WordPress/wp-ai-client)
- [Tools - MCP Adapter](https://github.com/WordPress/mcp-adapter)

## Common Properties

- [Portal](https://developer.wordpress.org/)
- [GitHubOrganization](https://github.com/WordPress)
- [GitHubRepository](https://github.com/WordPress/wordpress-develop)
- [Documentation](https://developer.wordpress.org/)
- [GettingStarted](https://developer.wordpress.org/rest-api/using-the-rest-api/)
- [Blog](https://developer.wordpress.org/news/)
- [ChangeLog](https://wordpress.org/documentation/article/wordpress-versions/)
- [Support](https://wordpress.org/support/)
- [StatusPage](https://www.incsub.com/status/)
- [TermsOfService](https://wordpress.org/about/license/)
- [PrivacyPolicy](https://automattic.com/privacy/)
- [Security](https://wordpress.org/about/security/)
- [Training](https://learn.wordpress.org/)
- [StackOverflow](https://stackoverflow.com/questions/tagged/wordpress)
- [SDK - PHP Toolkit](https://github.com/WordPress/php-toolkit)

## Features

| Name | Description |
|------|-------------|
| REST API | JSON-based REST API for interacting with WordPress content including posts, pages, media, users, and custom post types |
| Block Editor | Gutenberg block editor with JavaScript and PHP APIs for creating custom blocks and extending the editing experience |
| Application Passwords | Built-in authentication mechanism for third-party applications using per-application passwords with granular scoping |
| WP-CLI | Command-line interface for managing WordPress installations, automating tasks, and running deployments |
| Plugin API | Hooks and filters system for extending WordPress functionality through plugins without modifying core code |
| Multisite | WordPress Multisite enables running a network of sites from a single WordPress installation with shared users and plugins |
| WordPress Playground | Run WordPress in the browser via WebAssembly PHP for development, testing, and demonstrations |
| AI Integration | Provider-agnostic PHP AI client SDK and MCP adapter for integrating generative AI capabilities into WordPress |

## Use Cases

| Name | Description |
|------|-------------|
| Headless CMS | Use WordPress as a headless CMS with the REST API to deliver content to any frontend framework like Next.js, Nuxt, or React |
| Mobile Applications | Build iOS and Android apps that read and write WordPress content using the REST API |
| Content Automation | Automate content creation, publishing, and management using WP-CLI in CI/CD pipelines |
| Custom Block Development | Create custom Gutenberg blocks for unique editorial experiences and complex page layouts |
| Third-Party Integrations | Connect WordPress to external services like CRMs, analytics platforms, and e-commerce systems via the REST API |
| AI-Powered Content | Enhance WordPress with AI content generation, writing assistance, and intelligent recommendations |

## Integrations

| Name | Description |
|------|-------------|
| WooCommerce | E-commerce plugin with its own REST API that extends WordPress for online stores |
| Jetpack | WordPress.com connectivity plugin providing security, performance, and marketing tools |
| Advanced Custom Fields | Custom field framework for extending WordPress content models with structured data |
| Elementor | Visual page builder with REST API extensions for custom integrations |
| OpenAI | AI provider integration via WordPress AI API for content generation and assistance |
| Anthropic | AI provider integration via WordPress AI API using Claude models |
| Google AI | AI provider integration via WordPress AI API for Gemini models |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [WordPress REST API](openapi/wordpress-rest-api-openapi.yml)

### JSON Schema

- [Block](json-schema/wordpress-block-schema.json)
- [Block Type](json-schema/wordpress-block-type-schema.json)
- [Comment](json-schema/wordpress-comment-schema.json)
- [Comment Input](json-schema/wordpress-comment-input-schema.json)
- [Media Item](json-schema/wordpress-media-item-schema.json)
- [Page](json-schema/wordpress-page-schema.json)
- [Page Input](json-schema/wordpress-page-input-schema.json)
- [Plugin](json-schema/wordpress-plugin-schema.json)
- [Post](json-schema/wordpress-post-schema.json)
- [Post Input](json-schema/wordpress-post-input-schema.json)
- [Post Type](json-schema/wordpress-post-type-schema.json)
- [Rendered Content](json-schema/wordpress-rendered-content-schema.json)
- [Search Result](json-schema/wordpress-search-result-schema.json)
- [Settings](json-schema/wordpress-settings-schema.json)
- [Term](json-schema/wordpress-term-schema.json)
- [Term Input](json-schema/wordpress-term-input-schema.json)
- [Theme](json-schema/wordpress-theme-schema.json)
- [User](json-schema/wordpress-user-schema.json)

### JSON Structure

- [Block Structure](json-structure/wordpress-block-structure.json)
- [Block Type Structure](json-structure/wordpress-block-type-structure.json)
- [Comment Structure](json-structure/wordpress-comment-structure.json)
- [Media Item Structure](json-structure/wordpress-media-item-structure.json)
- [Page Structure](json-structure/wordpress-page-structure.json)
- [Plugin Structure](json-structure/wordpress-plugin-structure.json)
- [Post Structure](json-structure/wordpress-post-structure.json)
- [Post Type Structure](json-structure/wordpress-post-type-structure.json)
- [Search Result Structure](json-structure/wordpress-search-result-structure.json)
- [Settings Structure](json-structure/wordpress-settings-structure.json)
- [Term Structure](json-structure/wordpress-term-structure.json)
- [Theme Structure](json-structure/wordpress-theme-structure.json)
- [User Structure](json-structure/wordpress-user-structure.json)

### JSON-LD

- [WordPress Context](json-ld/wordpress-context.jsonld)

### Examples

- [Block Example](examples/wordpress-block-example.json)
- [Comment Example](examples/wordpress-comment-example.json)
- [Media Item Example](examples/wordpress-media-item-example.json)
- [Page Example](examples/wordpress-page-example.json)
- [Plugin Example](examples/wordpress-plugin-example.json)
- [Post Example](examples/wordpress-post-example.json)
- [Post Type Example](examples/wordpress-post-type-example.json)
- [Search Result Example](examples/wordpress-search-result-example.json)
- [Settings Example](examples/wordpress-settings-example.json)
- [Term Example](examples/wordpress-term-example.json)
- [Theme Example](examples/wordpress-theme-example.json)
- [User Example](examples/wordpress-user-example.json)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [WordPress REST API](capabilities/shared/rest-api.yaml) — 19 operations for posts, pages, media, comments, users, categories, tags, search, settings, themes, plugins, and blocks

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Content Management](capabilities/content-management.yaml) | WordPress REST API | 14 | Content Editor, Publisher |

## Vocabulary

- [WordPress Vocabulary](vocabulary/wordpress-vocabulary.yml) — Unified taxonomy mapping 13 resources, 6 actions, 1 workflow, and 4 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [WordPress Spectral Rules](rules/wordpress-spectral-rules.yml) — 35 rules across 13 categories enforcing WordPress REST API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
