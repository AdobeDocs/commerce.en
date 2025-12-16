---
title: Documentation RAG service
description: Learn how to use the AI-powered documentation search service for Adobe Commerce development.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
hide: yes
hidefromtoc: yes
---
# Documentation RAG service (Beta)

>[!NOTE]
>
>The documentation RAG service is currently in Beta and the experience is subject to change.

The documentation RAG (Retrieval-Augmented Generation) service provides AI-powered semantic search capabilities across relevant Adobe Commerce and App Builder documentation.

This RAG provides an IDE interface for asking questions about Adobe Commerce and can advise you on best practices for developing applications and other migration tasks.

The RAG service is part of the [Commerce extensibility tools](./coding-tools.md) MCP (Model Context Protocol) server, which integrates with Cursor and other MCP-compatible AI assistants.

## Available documentation

The following table describes what documentation is currently indexed by the RAG service, and the keywords you can use to trigger searching the associated index. The documentation included will continue to expand as we develop the RAG service.

| Category | Index | Content included | Keywords |
|-------|---------|---------|------------------------|
| [Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) | commerce-storefront-docs | Edge Delivery Services, drop-ins, storefront components | storefront, drop-in, EDS, product listing, checkout |
| [Extensibility](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhooks, events, extensions, integrations | webhook, event, extension, API mesh, GraphQL |
| [Commerce](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview) | commerce-core-docs | Core Commerce (catalog, customers, orders) | catalog, product, customer, order, inventory |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, runtime actions, UI extensions | app builder, runtime action, React Spectrum |

For more information on index selection, refer to [Automatic index selection](#automatic-index-selection-recommended) and [Explicit index selection](#explicit-index-selection).

## Security and privacy

* **IMS authentication** - All API calls use Adobe IMS OAuth2 tokens.
* **No data storage** - The MCP server does not store any credentials or data.
* **Local execution** - All tools run locally on your machine.
* **Secure communication** - Documentation search uses HTTPS with token validation.

The production endpoint is protected by [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview), which includes the following protections:

* Web Application Firewall (WAF) with Microsoft Default RuleSet 2.1 and Bot Manager RuleSet 1.0
* Geo-blocking for US embargoed regions (Cuba, Iran, North Korea, Syria, Crimea, Luhansk, Donetsk)
* DDoS protection at the edge
* API management backend locked down to only accept traffic from Front Door

For different security requirements, you can use a custom endpoint. See [Custom Front Door endpoint](#custom-front-door-endpoint) for more information.

## Prerequisites

Before installing, make sure you have:

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ (LTS recommended)
* [Cursor IDE](https://cursor.com/download){target="_blank"} (recommended) or another MCP-compatible IDE

   >[!NOTE]
   >
   >While other MCP-compatible IDEs are supported, Cursor is the recommended IDE for the best experience. If you are using another IDE, you will need to modify the prompts and other steps in the documentation to work with your selected IDE.

## Installation

1. Install the [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) globally:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Authenticate with Adobe IMS:

   ```bash
   aio auth login
   ```

1. Clone the Commerce extensibility tools repository and navigate to the directory:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. Install dependencies:

   ```bash
   npm install
   ```

1. Create or update `.cursor/mcp.json` in your Commerce project directory (not globally) to include the `commerce-extensibility-tools` MCP server:

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   Ensure that you replace `<your-project-directory>` with the actual path where you cloned the repository.

   >[!NOTE]
   >
   >On Windows, if you encounter issues with providing the path to your project directory, refer to [Path issues troubleshooting](#path-issues-windows).

1. Restart Cursor IDE to load the MCP server.

1. Verify the installation by asking the AI assistant:

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## Usage

Once installed, you can call the indexes [automatically](#automatic-index-selection-recommended) or [explicitly](#explicit-index-selection). You can also use the [`/search-commerce-docs` command](#command-based-search).

>[!NOTE]
>
>The RAG service returns the top 5 most relevant results.

### Automatic index selection (recommended)

By asking natural language questions about your Commerce project, the tool will automatically search the appropriate documentation index and provide relevant information:

>[!BEGINSHADEBOX]

The following prompt automatically selects the `commerce-storefront-docs` index:

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

The following prompt automatically selects the `commerce-extensibility-docs` index:

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

The following prompt automatically selects the `commerce-core-docs` index:

```shell-session
"How to configure product catalog settings?"
```

The following prompt automatically selects the `app-builder-docs` index:

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### Explicit index selection

Alternatively, you can specify the index you want to use in your prompt.

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### Command-based search

If you want to ensure the RAG service is used, you can manually invoke the `/search-commerce-docs` Cursor command to search documentation with your prompt:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Custom Front Door endpoint

By default, the documentation search uses the production [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) endpoint with WAF protection. For testing or development purposes, you can override this with the `FRONT_DOOR_URL` environment variable.

To use a custom endpoint, add it to your Cursor MCP configuration:

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>Most developers should use the default production endpoint and do not need to set the `FRONT_DOOR_URL` variable.

## Troubleshooting

The following sections provide troubleshooting tips for common issues you could encounter when using the documentation RAG service.

### Authentication errors

The documentation search tool requires Adobe IMS authentication. If you encounter authentication errors, use the following steps to troubleshoot and resolve the issue.

1. Verify you are logged in:

   ```bash
   aio where
   ```

1. Verify that you can see your IMS token:

   ```bash
   aio auth login --bare
   ```

1. If authentication errors persist, try logging out and back in:

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP server not loading

If the MCP server is not connecting, or your agent says it cannot connect to the RAG, use the following steps to troubleshoot and resolve the issue.

1. Open Cursor Settings using **Cmd ,** (macOS) or **Ctrl ,** (Windows and Linux).

1. Search for "MCP" and verify that `commerce-extensibility-tools` is listed and enabled.

1. Check for error messages in the MCP settings panel.

1. Verify the `mcp.json` file exists in your project:

   ```bash
   cat .cursor/mcp.json
   ```

1. Verify the path is correct and absolute:

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### Tool not found

1. Quit Cursor and reopen it.

1. Check the MCP server logs in Cursor's developer console by using **Cmd+Shift+P** (macOS) or **Ctrl+Shift+P** (Windows/Linux) and searching for "Developer: Open Logs Folder".

1. Verify the installation:

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   The server should start without errors.

### Path issues (Windows)

On Windows, use forward slashes `/` or escaped backslashes `\\`:

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## Additional resources

* [Adobe Commerce developer documentation](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [App Builder documentation](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [Model Context Protocol](https://modelcontextprotocol.io/){target="_blank"}
* [Cursor IDE](https://cursor.sh/docs){target="_blank"}
