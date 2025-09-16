---
title: Set up your storefront
description: Learn how to set up your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
---
# Set up your storefront

Fast track the storefront set up process by using the Site Creator tool to set up your storefront code repository and Document Author environment for managing storefront content.

If you want a more customizable and detailed walkthrough, see the [Create your storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) in the *Adobe Commerce Storefront documentation*.

## Prerequisites

* Ensure that you have a GitHub account (github.com) that can create repositories and is configured for local development.

* Review the concepts and workflow for storefront development in the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/get-started).

* An Adobe Commerce Optimizer instance with sample data and configured catalog views and policies.  See [Add sample data](get-started#add-sample-data)


## Create your storefront project





### Workflow overview


4. **[Preview demo site](#step-7-preview-demo-site)**–Connect to your storefront site to view the sample content and data from the [!DNL Adobe Commerce Optimizer] demo instance.
5. **[Develop in your local environment](#step-8-develop-in-your-local-environment)**–Install the required dependencies. Start the local development server, and update the storefront configuration to connect to the [!DNL Adobe Commerce Optimizer] instance that Adobe provisioned for you.
6. **[Next steps](#next-steps)**–Learn more about managing and displaying content and data in the storefront.

## Set up your storefront

Use the site creator tool to create storefront project with the following resources:

* **Site** links to the storefront landing page with the boilerplate content.
* **Code** links to the repository with the storefront boilerplate code source files
* **Content** links to the Document Author environment where you can manage site content
* **Commerce Config** links to the `config.json` file where you can customize configuration settings that determine what content displays in the storefront.

Before you begin, make sure you have the following information:

* Name of the GitHub organization to host the repository for the storefront boilerplate code
* The [Catalog Service endpoint](get-started.md#manage-an-instance) for your Adobe Commerce Optimizer instance

## Step 1: Create your storefront project

1. Open the [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Open the [site creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Select **Create New Site (Code & Content)**.

1. Enter the **Github Organization/Username** where you want to create the storefront code repository.

1. Enter a **Site Name**.

1. In the **Commerce GraphQL Endpoint (optional)** field, enter your Adobe Commerce Optimizer GraphQL endpoint, which you can access in the Commerce Cloud Manager after [creating an instance](getting-started.md#step-1-create-an-instance).

   Alternatively, if you are using [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), enter your API Mesh GraphQL endpoint into the **Commerce GraphQL Endpoint (optional)** field. See [create a mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) for more information.

1. Click **Create Site**. Follow the onscreen instructions to authorize access to your GitHub repository and copy the boilerplate code to the repository.

1. In the Site Details section, copy the links for your storefront project, so you can use them later.

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   You can use these links to customize your storefront using the following methods:

  * Customize your code: `https://github.com/<username or org>/<repo name>`
  * Edit your content: `https://da.live/#/<username or org>/<repo name>`
  * Manage your project configuration: `https://da.live/sheet#/<username or org>/<repo name>/config.json`
  * Preview your storefront: `https://main--<repo name>--<username or org>.aem.page/`

1. Customize the storefront configuration to pull data from your Commerce Optimizer instance.

     * In the **[!DNL Site Details]** section, click the **[!DNL Commerce Config]** link to open the `config.json` source file in your repository.

     * Updated the catalog service configuration to add the values for the required headers, `AC-View-ID` and `AC-Environment-ID`.

       ```json
       "cs": {
          "AC-View-ID": "{catalogViewId}",   # Replace with the catalog view ID for the global catalog view created when you added sample data.
          "AC-Environment-ID": "{tenantId}",} # Replace with the instance ID from your Commerce Optimizer instance.

       }
       ```


Step 3: Preview the demo site and explore

Verify that both the demo site and sample data display correctly.

* **Sample content** is served from the content folder in the Document Author environment. It includes the page layouts, banners, and labels for your site.
* **Sample data** is served from the [!DNL Adobe Commerce Optimizer] demo instance. Data includes product data with product attributes, images, product descriptions, and prices populated based on the header values specified in the storefront configuration file, `config.json`.

### Connect to your site to view sample content and data

1. View your site by navigating to `https://main--{SITE}--{ORG}.aem.live`.

   Replace `{ORG}` and `{SITE}` with the organization and name for your boilerplate repository.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   If the page returns a 404, verify the following in the config.json

   * The GitHub storefront code repository is registered with the [Code Sync app](https://github.com/apps/aem-code-sync/installations/select_target).
   * [Content has been published to Document Author environment using the demo content clone tool](#step-6%3A-add-content-documents-for-your-storefront).


1. View the sample catalog data coming from the Commerce Optimizer default instance.

   1. In the storefront header, click the magnifying glass to search for `tires`.

      ![[!DNL View product list page]](./assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

   1. Press **Enter** to view the search results page.

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

      The search results page components are defined by the `search` content document. The search results data is populated based on the storefront configuration in `config.json`.

   1. View the product details page by selecting any tire product on the page.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

      The product details page components are defined by the `default` content document in the `product` folder.

### Step 5: Develop in your local environment

In this section, you update the storefront configuration from your local development environment.

* Update the storefront configuration to connect to the GraphQL endpoint for the [!DNL Adobe Commerce Optimizer] instance that Adobe provisioned for you.
* Update the header values to retrieve data from your instance.

#### Start local development

1. In your IDE, checkout your main branch, and reset it to the last commit on the remote branch.

   ```shell
   git checkout main
   git reset --hard origin/main
   ```

1. Install the required dependencies.

   ```shell
   npm install
   ```

1. Install the [AEM Command Line Interface (CLI)](https://www.aem.live/developer/cli-reference).

   ```shell
   npm install -g @adobe/aem-cli
   ```

1. Clone your boilerplate repo.

   ```shell
   git clone https://github.com/{{ORG}}/{{SITE}}
   ```

1. Start the local development server.

   ```bash
   aem up
   ```

   The first page of your boilerplate storefront should be visible in your browser at `http://localhost:3000`.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Update the storefront configuration

Update the storefront configuration file and preview the changes in your local development environment.

1. In your IDE, update the storefront configuration to connect to the [!DNL Adobe Commerce Optimizer] instance that Adobe has provisioned for you.

   1. Open the `config.json` file.

   1. Update the following values using the endpoint for your [!DNL Adobe Commerce Optimizer] instance:

      * **`commerce-endpoint`**–Replace the existing value with your endpoint URL.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{instance ID}/graphql"
        ```

      * **`ac-environment-id`**—Replace the existing value with the instance ID from your endpoint URL.

        ```json
        "ac-environment-id": "{instanceId}"
        ```

   1. Save the file.

      If your local preview is working correctly, the updates are applied to your local storefront.

1. Check the site to see the results of the configuration change.

   1. In the browser, navigate to `http://localhost:3000` and refresh the page.

   1. In the storefront header, click the magnifying glass to search for `tires`.

      ![Search for tires](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

   1. Press **Enter** to display the Search Results page.

      ![Empty search results with invalid header values](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      The search doesn't return any results because the header values in your storefront configuration file are based on the default instance. Now that the configuration points to the [!DNL Adobe Commerce Optimizer] instance provisioned for you, those values are invalid.

### Next steps

See the [Storefront and Catalog Administrator end-to-end use case](./use-case/admin-use-case.md) to learn more about managing and displaying content and data in the storefront.

>[!MORELIKETHIS]
>
> See the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/) to learn more about updating site content and integrating with Commerce frontend components and backend data.
