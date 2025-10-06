---
title: Set up your storefront
description: Learn how to set up your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
---
# Set up your storefront

Your initial storefront site provides boilerplate code for a basic storefront with sample content, and support for product detail pages and product discovery (search and filtering).

## Prerequisites

* Ensure that you have a GitHub account (github.com) that can create repositories and is configured for local development.

* Learn about the concepts and workflow to develop Commerce storefronts on Adobe Edge Delivery Services by reviewing the [Overview](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) in the Adobe Commerce Storefront documentation.

* An [!DNL Adobe Commerce Optimizer] instance with sample data and configured catalog views and policies.  See [Add sample data](get-started.md#add-sample-data). You need the following data from your instance:
   * Tenant ID for your instance (also called the instance ID). You can get this value from the [instance details page](./get-started.md#manage-an-instance) in your [!DNL Commerce Optimizer instance].
   * The [GraphQL endpoint](get-started.md#manage-an-instance) for your [!DNL Adobe Commerce Optimizer] instance
   * The catalog view ID for the global catalog view created when you added sample data. You can get this value from the [catalog details page](./setup/catalog-view#view-details) in your [!DNL Commerce Optimizer instance].
   * The source locale for your catalog view. The default locale for the sample data is `en_US`.

  >[!NOTE]
  >
  > Trial access customers provisioned in the shared IMS organization can find the GraphQL endpoint in the welcome email you received when your instance was created. Additionally, trial instances are pre-configured with sample data, catalog views, and policies.

## Set up steps

Install Node.js and the Sidekick browser extension required to develop and test your [!DNL Adobe Commerce Optimizer] storefront on Edge Delivery Services.

1. **[Create your storefront project](#set-up-your-storefront)**–Use the [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) to create a new storefront project with boilerplate code, sample content, and a configuration file.

1. **[Customize the storefront configuration](#customize-the-storefront-configuration)**–Update the `config.json` file in your repository to connect to your [!DNL Adobe Commerce Optimizer] instance.

1. **[Preview the demo site and verify sample data](#preview-the-demo-site-and-verify-sample-data)**–View your storefront site and verify that product detail pages and product discovery (search and filtering) are working correctly.

### 1. Set up your storefront

Use the site creator tool to create storefront project with the following resources:

* **Site** the storefront site landing page with the boilerplate content.
* **Code** the repository with the storefront boilerplate code source files
* **Content** the Document Author environment with site content files
* **Commerce Config** a `config.json` file to customize storefront configuration settings for your instance

### 2. Create your storefront project

1. Open the [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Select **Create New Site (Code & Content)**.

   When the repository is created, the Site Creator updates and prompts you to install the Code Sync app.

   ![[!DNL Install Code Sync app]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. In the **Commerce GraphQL Endpoint (optional)** field, enter the GraphQL endpoint for your [!DNL Adobe Commerce Optimizer] instance.

1. Install the Code Sync app: Click **[!UICONTROL Install AEM Code Sync App]** to open the Code Sync installer in a new tab.

   * Select your GitHub organization, then click **[!UICONTROL Configure]**
   * In the Code Sync interface, select **[!UICONTROL Only select repositories]**.
   * Click the **[!UICONTROL Select respositories]** menu, choose the storefront code repository you created.
   * Click **[!UICONTROL Save]** to register your repository.

1. In the browser window where the Site Creator is open, click **Continue** to add the boilerplate content to the Document Author environment.

   The Site Creator copies the storefront boilerplate content to the Document Author environment. This step takes a minute or two.

1. In the Site Details section, review the links for your storefront project

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   Use these links to customize your storefront using the following methods:

   * Customize your code: `https://github.com/<username or org>/<repo name>`
   * Edit your content: `https://da.live/#/<username or org>/<repo name>`
   * Manage your storefront project configuration: `https://da.live/sheet#/<username or org>/<repo name>/config.json`
   * Preview your storefront: `https://main--<repo name>--<username or org>.aem.page/`

1. Use the **Copy** feature to copy the links and save them for future reference.

### 2. Customize the storefront configuration

1. Customize the storefront configuration to retrieve data from your [!DNL Commerce Optimizer] instance.

   * Update the catalog service configuration to add the values for the required headers, `AC-View-ID`, `AC-Environment-ID`, and `AC-Source-Locale`. See the [Prerequisites](#prerequisites).

      ```json
      "cs": {
         "AC-View-ID": "{catalogViewId}",
         "AC-Environment-ID": "{tenantId}",
         "AC-Source-Locale": "en_US"
         }
      ```

   * Save the file.

### 3. Preview the demo site and verify sample data

1. View your site by navigating to **Site** URL provided, for example:

   `https://main--{SITE}--{ORG}.aem.live`.

   Replace `{ORG}` and `{SITE}` with the GitHub organization and site name you set for your boilerplate repository.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

1. **View a sample product**:  In the browser, navigate to `https://main-{SITE}.aem.live/products/foo/{sku}`, where {sku} is the SKU of any of the sample products.

   For example, `https://main--{SITE}.aem.live/products/foo/aur-flu-tir-std-2017.`

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

   The product detail page components are defined by the `products` content document in your content folder. The product details are retrieved from your [!DNL Adobe Commerce Optimizer] instance.

   >[!NOTE]
   >
   > View available SKUs from the [[!DNL Data Sync]](./setup/data-sync.md) page in your [!DNL Adobe Commerce Optimizer] instance.

1. **Check search results**: Verify that product discovery (search and filtering) is working correctly.

   * In the storefront header, click the magnifying glass to search for `tires`.

   * Press **Enter** to view the search results page.

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

   * View the product details page by selecting any tire product on the page.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## Next steps

* **[Install Sidekick](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/authoring/install-sidekick.html)**, the browser extension for Adobe Experience Manager to edit, preview, and publish your content directly from your website pages.

* **[Set up a local development environment](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/local-development-setup/)** to customize and preview your storefront code and content

* **Complete the [Storefront and Catalog Administrator end-to-end use case](./use-case/admin-use-case.md**)** to learn how to manage and display content and data in the storefront

* **[Learn more about storefront setup](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)**

* **[Use Commerce dropins to customize the storefront experience](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)**

>[!MORELIKETHIS]
>
> See the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/) to learn more about updating site content and integrating with Commerce frontend components and backend data.
