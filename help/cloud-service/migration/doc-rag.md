---
title: Documentation RAG service
description: Learn how to use the AI-powered documentation search service for Adobe Commerce development.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
hide: yes
hidefromtoc: yes
---
# Documentation RAG service

The documentation RAG (Retrieval-Augmented Generation) service provides AI-powered semantic search across Adobe Commerce and App Builder documentation.

The RAG service is part of the [Commerce extensibility tools](https://github.com/adobe-commerce/commerce-extensibility-tools){target="_blank"} MCP (Model Context Protocol) server, which integrates with Cursor IDE and other MCP-compatible AI assistants.

## How it works

The documentation search uses the `search-commerce-docs` tool, which provides intelligent documentation search powered by Azure RAG with automatic index selection:

1. **Automatic authentication**: Uses your `aio` CLI token (from `aio auth login`).
1. **Intelligent index selection**: Automatically selects the best documentation index based on your query keywords.
1. **IMS authentication**: Secure authentication via Adobe IMS.
1. **AI-powered search**: Semantic search across comprehensive documentation.
1. **Instant results**: Returns top 5 most relevant results in approximately 2 seconds.

## Available documentation indexes

| Index | Content | Auto-selected keywords |
|-------|---------|------------------------|
| **commerce-storefront-docs** | Edge Delivery Services, drop-ins, storefront components | storefront, drop-in, EDS, product listing, checkout |
| **commerce-extensibility-docs** | Webhooks, events, extensions, integrations | webhook, event, extension, API mesh, GraphQL |
| **commerce-core-docs** | Core Commerce (catalog, customers, orders) | catalog, product, customer, order, inventory |
| **app-builder-docs** | App Builder, runtime actions, UI extensions | app builder, runtime action, React Spectrum |

## Prerequisites

Before installing, make sure you have:

* [Cursor IDE](https://cursor.com/download){target="_blank"} (recommended) or another MCP-compatible IDE
* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ (LTS recommended)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli){target="_blank"} installed globally
* Adobe IMS authentication configured

## Installation

1. Install the Adobe I/O CLI globally:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Authenticate with Adobe IMS:

   ```bash
   aio auth login
   ```

1. Clone the Commerce extensibility tools repository:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. Install dependencies:

   ```bash
   npm install
   ```

1. Create or update `.cursor/mcp.json` in your Commerce project directory (not globally):

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/ABSOLUTE/PATH/TO/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   Replace `/ABSOLUTE/PATH/TO/` with the actual path where you cloned the repository.

1. Restart Cursor IDE to load the MCP server.

1. Verify the installation by asking the AI assistant:

   ```text
   Can you show me the available Adobe Commerce tools?
   ```

## Usage

Once installed, you can use the tools in two ways:

### Automatic index selection (recommended)

Ask natural language questions and the tool automatically searches the appropriate documentation:

```text
"How do I use Edge Delivery Services drop-ins for product listing?"
```

Automatically selects: `commerce-storefront-docs`

```text
"How do I create a webhook in Adobe Commerce?"
```

Automatically selects: `commerce-extensibility-docs`

```text
"How to configure product catalog settings?"
```

Automatically selects: `commerce-core-docs`

```text
"What are App Builder runtime action best practices?"
```

Automatically selects: `app-builder-docs`

### Explicit index selection

You can also specify which index to search:

```text
Search commerce-storefront-docs for authentication drop-in
```

```text
Using app-builder-docs, how do I deploy runtime actions?
```

### Direct command

Use the `/search-commerce-docs` command to search documentation directly in conversations with your agent:

```text
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Troubleshooting

### Authentication errors

The documentation search tool requires Adobe IMS authentication.

1. Verify you are logged in:

   ```bash
   aio where
   ```

1. Test token retrieval:

   ```bash
   aio auth login --bare
   ```

1. If you encounter authentication errors, try logging out and back in:

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP server not loading

1. Open Cursor Settings using **Cmd+,** (macOS) or **Ctrl+,** (Windows and Linux).

1. Search for "MCP" and verify `commerce-extensibility-tools` server is listed.

1. Check for error messages in the MCP settings panel.

1. Verify the `mcp.json` file exists in your project:

   ```bash
   cat .cursor/mcp.json
   ```

1. Verify the path is correct and absolute:

   ```bash
   ls -la /path/to/commerce-extensibility-tools/index.js
   ```

### Tool not found

1. Restart Cursor completely (quit and reopen).

1. Check MCP server logs in Cursor's developer console.

1. Verify the installation:

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   The server should start without errors.

### Path issues (Windows)

On Windows, use forward slashes or escaped backslashes:

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

Or:

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## Custom APIM endpoint

By default, the documentation search uses the production Azure API Management endpoint. For testing or development purposes, you can override this with the `APIM_URL` environment variable.

To use a custom endpoint, add it to your Cursor MCP configuration:

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/path/to/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "APIM_URL": "https://your-custom-apim-endpoint.azure-api.net"
      }
    }
  }
}
```

>[!NOTE]
>
>Most users should use the default production endpoint and do not need to set this variable.

## Security and privacy

* **IMS authentication**: All API calls use Adobe IMS OAuth2 tokens.
* **No data storage**: The MCP server does not store any credentials or data.
* **Local execution**: All tools run locally on your machine.
* **Secure communication**: Documentation search uses HTTPS with token validation.

## Additional resources

* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [Adobe Commerce Developer](https://developer.adobe.com/commerce/){target="_blank"}
* [Model Context Protocol](https://modelcontextprotocol.io/){target="_blank"}
* [Cursor IDE](https://cursor.sh/docs){target="_blank"}

