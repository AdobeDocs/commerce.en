---
title: Set up your storefront
description: Learn how to run the scaffolding tool to setup your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
---
# Set up your storefront

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

The following steps demonstrate how to quickly set up your Adobe Commerce Storefront powered by Edge Delivery using the `aio commerce init` command. This process sets up the following:

* [Commerce Storefront powered by Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) - A performant, scalable, and secure storefront that is powered by Adobe's Edge Delivery Services.
* [API Mesh for Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/mesh/) - an API platform that allows developers to combine multiple data sources into a single GraphQL endpoint. API Mesh orchestrates third-party API with Adobe API through a single gateway. One query to the single GraphQL endpoint can return results from multiple sources.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - A collection of developer tools with access to APIs, events, runtime functions, and plugins, which you can use to build projects for Adobe applications.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - A serverless engine for deploying custom code that responds to events and executes functions in the cloud.

## Prerequisites

Before running the `aio commerce init` command, you must complete the following prerequisites:

1. Install Node Version Manager (NVM).

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
    ```

1. Install Node.js and NPM. For more information, see [Node.js](https://nodejs.org/en/).

    ```bash
    nvm install 22
    ```

    ```bash
    npm install -g npm
    ```

1. Install the [Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).

    ```bash
    npm install -g @adobe/aio-cli
    ```

1. Install the Adobe Developer API Mesh plugin.

    ```bash
    aio plugins:install @adobe/aio-cli-plugin-api-mesh
    ```

1. Install the Adobe Developer Commerce plugin.

    ```bash
    aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
    ```

1. Update any existing plugins.

    ```bash
    aio plugins:update
    ```

1. Log in to your Adobe Experience Cloud account.

    ```bash
    aio login
    ```

1. Select the IMS org, project, and workspace. Use the arrow keys and press **Enter** to make your selection. For more information on `aio` commands, refer to the [Adobe Developer CLI documentation](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands).

    ```bash
    aio console org select
    ```

    ```bash
    aio console project select
    ```

    ```bash
    aio console workspace select
    ```

1. If you have not already, accept the Developer Terms of Use in the Adobe Developer console by navigating to https://developer.adobe.com/console/home and clicking **Accept and continue**.

## Run the `aio commerce init` command

Running the following command creates a scaffolding for your Commerce storefront. This scaffolding provides a great starting place for building and understanding your storefront. For more information about working with the storefront, see the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).


1. Run the `init` command:

    ```bash
    aio commerce init
    ```

1. If you are already logged into GitHub, enter `Y` to create the repo under your username.

1. Enter the name of the repository that you want to create.

1. Select one of the following options:

    * **Use the demo Adobe Commerce tenant** - Use a demo tenant. 
      * If you select this option, you are prompted to install the AEM Code Sync bot in a browser window. Specify the repository that you created and authorize the bot. Return to the CLI and enter `y` to confirm the AEM Code Sync bot installation.
    * **Pick an available Adobe Commerce tenant** - Select an existing Commerce tenant in the selected organization.
      * If you select this option, you must select the project and workspace to create a mesh in.

    >[!NOTE]
    >
    >If you select the `Pick an available API (Mesh -> SaaS)` option, you must have an existing Project and Workspace in the Adobe Developer Console. [Creating a templated project](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) and selecting App Builder will automatically create the necessary workspaces.

1. Once the process completes, you can customize your storefront using the following methods:

   * Customize your code: `https://github.com/<username or org>/<repo name>`
   * Edit your content: `https://da.live/#/<username or org>/<repo name>`
   * Manage your config: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * Preview your storefront: `https://main--<repo name>--<username or org>.aem.page/`
   * Run locally: `aio commerce:dev`

To customize your storefront, refer to the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).

## Drop-ins

For Adobe Commerce Optimizer, your storefront uses drop-ins to support the popover and PLP functionality available in [product discovery](./product-discovery.md).

[Learn](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/) how to configure the popover and PLP drop-ins.
