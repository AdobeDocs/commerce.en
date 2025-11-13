---
title: Set up your storefront
description: Learn how to set up your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
---
# Set up your storefront

This guide walks you through setting up a storefront for your [!DNL Adobe Commerce Optimizer] instance using Adobe Edge Delivery Services. Your storefront includes boilerplate code, sample content, and support for product detail pages and product discovery (search and filtering).

**Estimated time to complete:** 30-45 minutes

## Prerequisites

* **GitHub account** that can create repositories and is configured for local development (github.com)
* **[!DNL Adobe Commerce Optimizer] instance** with sample data and configured catalog views and policies
  * See [Add sample data](get-started.md#add-sample-data) for setup instructions.

### Required instance data

Before you begin, gather the following information from your [!DNL Adobe Commerce Optimizer] instance:

* **Tenant ID** (also called the instance ID)
  * Available from the [instance details page](get-started.md#manage-instances)
* **GraphQL endpoint** for your instance
  * Available from the [instance details page](get-started.md#manage-instances)
* **Catalog view ID** for the global catalog view
  * Available from the [catalog details page](./setup/catalog-view.md#manage-catalog-view)
* **Source locale** for your catalog view
  * Default for sample data is `en_US`

>[!NOTE]
>
>Trial access customers can find the GraphQL endpoint in the welcome email received when your instance was created. Trial instances come pre-configured with sample data, catalog views, and policies.

## Set up steps

1. **[Create your storefront project](#create-your-storefront-project)**–Use the [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) to create a new storefront project with boilerplate code, sample content, and a configuration file.

1. **[Customize the storefront configuration](#customize-the-storefront-configuration)**–Update the `config.json` file in your repository to connect to your [!DNL Adobe Commerce Optimizer] instance.

1. **[Verify your setup](#verify-your-setup)** (10 mins)
   * Preview your storefront site
   * Test product detail pages and search functionality

## Create your storefront project

The Site Creator tool creates a complete storefront project with the following components:

* **Site**: Storefront landing page with boilerplate content
* **Code**: Repository with boilerplate source files
* **Content**: Document Author environment with site content files
* **Commerce Config**: `config.json` file for instance-specific configuration

### Step 1: Generate your project

1. Open the [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Select **Create New Site (Code & Content)**.

1. Complete the site configuration:

   * **GitHub Organization/Username**: Enter your GitHub username or organization name
   * **Site Name**: Choose a descriptive name for your storefront
   * **Commerce GraphQL Endpoint (optional)**: Enter the GraphQL endpoint for your [!DNL Adobe Commerce Optimizer] instance

1. Click **Create Site** to create the GitHub repository with the storefront boilerplate code.

   When the repository is created, the Site Creator updates and prompts you to install the Code Sync app.

### Step 2: Install Code Sync app

1. Click **[!UICONTROL Install AEM Code Sync App]** to open the Code Sync installer in a new tab.

1. Configure the Code Sync app:
   * Select your GitHub organization, then click **[!UICONTROL Configure]**.
   * In the Code Sync interface, click **[!UICONTROL Only select repositories]**.
   * Click the **[!UICONTROL Select repositories]** menu, then choose the storefront code repository you created.
   * Click **[!UICONTROL Save]** to register your repository.

1. Return to the browser window where the Site Creator is open, and click **Create Site**.

   The Site Creator copies the storefront boilerplate content to the Document Author environment. This process takes 1-2 minutes.

### Step 3: Save your project links

1. In the Site Details section, review the links for your storefront project:

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   Use these links to manage your storefront code, content, and configuration.

1. Copy and save these links for future reference: Click **[!UICONTROL Copy].

## Configure your storefront

Update your storefront configuration to connect to your [!DNL Adobe Commerce Optimizer] instance.

1. Open the `config.json` file in your boilerplate code repository.

1. Locate the `cs` (Catalog Service) section in the configuration.

1. Replace the placeholder values with the values for your instance. See [Prerequisites](#prerequisites).

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Environment-ID": "{tenantId}",
      "AC-Source-Locale": "en_US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```
   
   To find the price book ID, check the [catalog view configuration details](../setup/catalog-view.md) in Adobe Commerce Optimizer to
   see the assigned price books. If no price books are assigned, you can remove this header from the configuration file, and add it back when a
   price book has been assigned to the catalog view. 

1. Save the configuration file.

>[!NOTE]
>
>The configuration changes may take a few minutes to propagate. If you don't see data immediately, wait 2-3 minutes before troubleshooting.

## Verify your setup

Test your storefront to ensure it's properly connected to your [!DNL Adobe Commerce Optimizer] instance.

### Step 1: View your storefront homepage

1. Navigate to your live preview URL:

   `https://main--{SITE}--{ORG}.aem.live`

   Replace `{ORG}` and `{SITE}` with your GitHub organization and site name.

1. **Success criteria**: You should see the storefront homepage with boilerplate content.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### Step 2: Test product detail pages

View the default product detail page to verify product data is loading correctly.

1. Navigate to a sample product page:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   Use any SKU from your sample data, for example:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   For the default storefront, you can use the `placeholder` value in the route to view the product. When you begin customizing your storefront, you can customize the storefront code to set the path to the product detail page based on product routes defined in your catalog.

   >[!TIP]
   >
   >View available SKUs from the [Data Sync](./setup/data-sync.md) page in your [!DNL Adobe Commerce Optimizer] instance.

1. **Success criteria**: The page should display:
   * Product name, description, and pricing
   * Product images
   * Add to cart functionality
   * Data retrieved from your [!DNL Adobe Commerce Optimizer] instance

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### Step 3: Test the default search functionality

Test the default product features, including search and filtering.

1. On the storefront homepage, click the magnifying glass icon in the header.

1. Type the search string `tires` and press **Enter**.

1. **Success criteria**: You should see:
   * Search results page with tire products
   * Filtering options in the sidebar
   * Product listings with images and pricing

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. Click on any tire product to view its detail page.

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## Troubleshooting

If you encounter issues during setup, use the web page inspector console to check for errors. Also, try clearing your browser cache or using a different browser.

Use the following guidance to check common issues:

### Common issues

| Issue | Symptoms | Solution |
|-------|----------|----------|
| **Code Sync installation fails** | Unable to complete Code Sync setup | <ul><li>Ensure you have admin access to your GitHub organization.</li><li>Try using a personal repository instead of an organization.</li><li>Check GitHub permissions and try again.</li></ul> |
| **Site not loading** | 404 or connection errors | <ul><li>Verify your site URL format: `https://main--{SITE}--{ORG}.aem.live`</li><li>Check that the Code Sync app is properly installed.</li><li>Ensure that the repository is public or properly configured.</li></ul> |
| **No product data displayed** | Product pages show placeholders or errors | <ul><li>Verify your configuration values in `config.json`</li><li>In the [!DNL Adobe Commerce Optimizer] instance, check the Data Sync page to verify that sample products are loaded. If no products are available, reload the sample data or add a product using the [Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request). Wait a few minutes for configuration changes to propagate.</li><li>Try to retrieve the product details using the Merchandising Service [products query](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details) using the same headers configured in the `config.json` file. If you can retrieve the data, then it is likely an issue with the catalog view configuration or an index error.</li></ul>|
| **Search returns no results** | Empty search results page |<ul><li>Verify that you can retrieve the product search results using the Merchandising Services [productSearch query](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search) using the same headers configured in the `config.json` file. If you can retrieve the data, then it is likely an issue with the catalog view configuration or an index error.</li><li>Confirm that the catalog view ID in the `config.json` file matches the catalog view ID in [!DNL Adobe Commerce Optimizer].</li><li>In Adobe Commerce Optimizer, verify the configuration of the policies, locale, and price books that you used in the storefront header configuration.</li><li>Verify the [attribute metadata settings](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) are set correctly for search.</li></ul>|

### Validation checklist

Before proceeding to the next steps, ensure that your storefront is functioning correctly by verifying the following:

![Checklist](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Configuration values match your instance settings<br>
![Checklist](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Storefront homepage loads without errors<br>
![Checklist](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) At least one product detail page displays complete information<br>
![Checklist](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Search functionality returns relevant results<br>
![Checklist](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Product images are loading correctly<br>
![Checklist](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Configuration values match your instance settings<br>

### Get help

If issues persist:

* Review the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/)
* Check the [Adobe Commerce Optimizer developer guide](https://developer.adobe.com/commerce/services/optimizer/)
* Visit the [Adobe Commerce Support resources](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)

## Next steps

After you setup and verify your storefront, you can:

1. **[Install Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#install-and-configure-sidekick)** - Browser extension for editing, previewing, and publishing content directly from your website

2. **[Set up a local development environment](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)** - Create a local environment to customize your storefront code and content

### Learn and explore

* **[Complete the end-to-end use case](./use-case/admin-use-case.md)** - Learn more about storefront setup and catalog management using [!DNL Adobe Commerce Optimizer]

* **[Explore storefront customization](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)** - Learn advanced setup and configuration options

* **[Use Commerce drop-ins to customize the storefront experience](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)**–Add pre-built components to enhance your storefront experience

>[!MORELIKETHIS]
>
> See the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/) to learn more about updating site content and integrating with Commerce frontend components and backend data.
