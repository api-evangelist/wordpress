# WordPress GraphQL API

## Overview

WordPress supports a full-featured GraphQL API through the [WPGraphQL plugin](https://www.wpgraphql.com/), an open-source WordPress plugin that provides an extendable GraphQL schema and API for any WordPress site. WPGraphQL is widely adopted for headless WordPress setups, enabling developers to query and mutate WordPress data using standard GraphQL operations.

- **Plugin**: WPGraphQL
- **Homepage**: https://www.wpgraphql.com/
- **Documentation**: https://www.wpgraphql.com/docs/
- **GitHub**: https://github.com/wp-graphql/wp-graphql
- **Default Endpoint**: `https://{site}/graphql`
- **License**: GPL-3.0

## Authentication

WPGraphQL supports multiple authentication strategies:

- **Cookie Authentication** — uses WordPress nonces; suitable for browser-based clients on the same domain.
- **HTTP Basic Auth** — via [WPGraphQL JWT Authentication](https://github.com/wp-graphql/wp-graphql-jwt-authentication) or Application Passwords.
- **Application Passwords** — built into WordPress core since 5.6; pair with HTTP Basic for REST or GraphQL requests.
- **JWT Tokens** — the `wp-graphql-jwt-authentication` extension adds `login` and `refreshJwtAuthToken` mutations.

Public (non-authenticated) queries return only publicly visible content. Authenticated queries can access drafts, private posts, user details, and mutations.

## Endpoint

```
POST https://{site}/graphql
```

All operations use a single POST endpoint with a JSON body:

```json
{
  "query": "{ posts { nodes { id title } } }",
  "variables": {},
  "operationName": null
}
```

A GET endpoint is also available for simple queries using the `query` parameter.

## Core Schema Concepts

### Content Nodes

WPGraphQL models WordPress content using a layered interface system:

- `ContentNode` — base interface for all post-type objects (posts, pages, custom post types).
- `TermNode` — base interface for taxonomy terms (categories, tags, custom taxonomies).
- `NodeWithTitle`, `NodeWithContent`, `NodeWithExcerpt`, `NodeWithAuthor`, `NodeWithFeaturedImage`, `NodeWithComments` — composable interfaces applied to content types.

### Connections (Relay Pagination)

WPGraphQL uses the [Relay Connection spec](https://relay.dev/graphql/connections.htm) for paginated lists:

- Every list field returns a `*Connection` type (e.g., `PostConnection`).
- Connections have `edges` (list of `*Edge`) and `nodes` (shortcut list of the type).
- Each edge has a `cursor` and a `node`.
- `PageInfo` carries `hasNextPage`, `hasPreviousPage`, `startCursor`, `endCursor`.

Pagination arguments: `first`, `last`, `before`, `after`.

### Global Node IDs

All objects implement the `Node` interface with a globally unique `id` field (base64-encoded). Use the `node(id: ID!)` root field to fetch any object by its global ID.

## Example Queries

### Fetch Recent Posts

```graphql
query GetRecentPosts {
  posts(first: 10, where: { status: PUBLISH }) {
    nodes {
      id
      databaseId
      title
      slug
      date
      excerpt
      author {
        node {
          name
          avatar {
            url
          }
        }
      }
      categories {
        nodes {
          name
          slug
        }
      }
      featuredImage {
        node {
          sourceUrl
          altText
          mediaDetails {
            width
            height
          }
        }
      }
    }
  }
}
```

### Fetch Single Post by Slug

```graphql
query GetPostBySlug($slug: ID!) {
  post(id: $slug, idType: SLUG) {
    id
    databaseId
    title
    content
    date
    modified
    status
    author {
      node {
        name
        email
      }
    }
    tags {
      nodes {
        name
        slug
      }
    }
  }
}
```

### Fetch Pages Hierarchically

```graphql
query GetPages {
  pages(where: { parent: 0 }) {
    nodes {
      id
      title
      slug
      uri
      children {
        nodes {
          id
          title
          slug
        }
      }
    }
  }
}
```

### Fetch Menu by Location

```graphql
query GetMenu($location: MenuLocationEnum!) {
  menus(where: { location: $location }) {
    nodes {
      id
      name
      menuItems {
        nodes {
          id
          label
          url
          target
          parentId
          childItems {
            nodes {
              id
              label
              url
            }
          }
        }
      }
    }
  }
}
```

### Fetch User with Roles

```graphql
query GetUsers {
  users(first: 20) {
    nodes {
      id
      databaseId
      name
      email
      roles {
        nodes {
          name
          displayName
        }
      }
      avatar {
        url
        width
        height
      }
    }
  }
}
```

## Example Mutations

### Create a Post (Authenticated)

```graphql
mutation CreatePost($input: CreatePostInput!) {
  createPost(input: $input) {
    post {
      id
      databaseId
      title
      status
      slug
      date
    }
  }
}
```

Variables:

```json
{
  "input": {
    "title": "My New Post",
    "content": "<p>Hello world</p>",
    "status": "PUBLISH",
    "authorId": "dXNlcjox"
  }
}
```

### Update a Post (Authenticated)

```graphql
mutation UpdatePost($input: UpdatePostInput!) {
  updatePost(input: $input) {
    post {
      id
      title
      modified
    }
  }
}
```

### Delete a Post (Authenticated)

```graphql
mutation DeletePost($id: ID!) {
  deletePost(input: { id: $id }) {
    deletedId
    post {
      id
      title
    }
  }
}
```

### Create a Comment (Authenticated)

```graphql
mutation CreateComment($input: CreateCommentInput!) {
  createComment(input: $input) {
    comment {
      id
      content
      date
      author {
        node {
          name
        }
      }
    }
  }
}
```

## Filtering and Ordering

WPGraphQL exposes `where` arguments on connection fields using `*ConnectionWhereArgs` input types:

```graphql
query FilteredPosts {
  posts(
    first: 5
    where: {
      categoryName: "news"
      tag: "featured"
      dateQuery: { after: { year: 2024, month: 1, day: 1 } }
      orderby: { field: DATE, order: DESC }
      search: "wordpress"
      status: PUBLISH
    }
  ) {
    nodes {
      title
      date
    }
  }
}
```

## Introspection

WPGraphQL supports standard GraphQL introspection by default. Disable it in production via the WPGraphQL settings if desired:

```graphql
{
  __schema {
    types {
      name
      kind
    }
  }
}
```

## Extensions

The WPGraphQL ecosystem includes official and community extensions:

| Extension | Purpose |
|---|---|
| WPGraphQL JWT Authentication | JWT-based auth tokens |
| WPGraphQL for WooCommerce | WooCommerce product/order schema |
| WPGraphQL for ACF | Advanced Custom Fields schema |
| WPGraphQL Smart Cache | Persisted queries and edge caching |
| WPGraphQL for Gravity Forms | Gravity Forms schema |
| WPGraphQL Polylang | Multi-language via Polylang |

## Resources

- Documentation: https://www.wpgraphql.com/docs/
- GitHub: https://github.com/wp-graphql/wp-graphql
- Extensions: https://www.wpgraphql.com/extensions
- Discord: https://wpgraphql.com/discord
- Changelog: https://github.com/wp-graphql/wp-graphql/releases
