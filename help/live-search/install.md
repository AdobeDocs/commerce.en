---
title: Get Started with [!DNL Live Search]
description: Learn the system requirements and installation steps for [!DNL Live Search] from Adobe Commerce.
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Set up for success with [!DNL Live Search]

Adobe Commerce [!DNL Live Search] and [[!DNL Catalog Service]](../catalog-service/guide-overview.md) work together to provide a performant, relevant, and intuitive search solution to allow your customers to find exactly what they need, fast. Specifically, [!DNL Catalog Service] surfaces your catalog data for SaaS services, such as [!DNL Live Search] to use.

This article provides step-by-step instructions for implementing [!DNL Live Search] with the [!DNL Catalog Service].

## Audience

This article is intended for the developer or systems integrator on your team who is responsible for installing and configuring your Adobe Commerce instance.

## Requirements

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1, 8.2, or 8.3
- [!DNL Composer]
- Running cron jobs and indexers

>[!IMPORTANT]
>
>Before implementing [!DNL Live Search], see the [Boundaries and Limits](boundaries-limits.md) section to ensure that [!DNL Live Search] fits your business needs.

## Important updates

- As of [!DNL Live Search] 3.0.2, the [!DNL Catalog Service] extension is bundled with the installation.

- Due to the Elasticsearch 7 end-of-support announcement for August 2023, Adobe recommends that all Adobe Commerce customers migrate to the OpenSearch 2.x search engine. For information about migrating your search engine during a product upgrade, see [Migrating to OpenSearch](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) in the _Upgrade Guide_.

## Supported platforms

- Adobe Commerce on Cloud (ECE) : 2.4.4+
- Adobe Commerce on-prem (EE) : 2.4.4+

## Workflow overview

At a high level, onboarding [!DNL Live Search] requires that you:

1. [Install](#1-install-the-live-search-extension) the [!DNL Live Search] extension
1. [Configure](#2-configure-api-keys) the API keys
1. [Sync](#3-sync-your-catalog-data) your catalog data
1. [Verify](#4-verify-that-the-data-was-exported) that the catalog data was exported
1. [Configure](#5-configure-the-data) the data
1. [Test](#6-test-the-connection) the connection
1. [Verify](#7-validate-events-are-capturing-data) that events are capturing data
1. [Customize](#8-customize-for-your-storefront) your storefront

## 1. Install the [!DNL Live Search] extension

[!DNL Live Search] is installed as an extension from [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) through [Composer](https://getcomposer.org/). After you install and configure [!DNL Live Search], Adobe [!DNL Commerce] begins sharing search and catalog data with SaaS services. At this point, *Admin* users can set up, customize, and manage search facets, synonyms, and merchandising rules.

>[!BEGINTABS]

>[!TAB New Commerce instance]

Follow these instructions if you are installing [!DNL Live Search] on a new Commerce instance.

1. Confirm that [cron jobs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) and [indexers](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) are running.

1. Use Composer to add the Live Search module to your project:

   ```bash
   composer require magento/live-search --no-update
   ```

1. Update dependencies and install the extension:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Disable [!DNL OpenSearch] and related modules temporarily, and install [!DNL Live Search].

   ```bash
   bin/magento module:disable Magento_ Magento_Elasticsearch8 Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Elasticsearch] continues to manage search requests from the storefront while the [!DNL Live Search] service synchronizes catalog data and indexes products in the background.

1. Install the updates.

   ```bash
   bin/magento setup:upgrade
   ```

1. Verify that the following [indexers](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) are set to "Update by Schedule":

   - Product Feed
   - Product Variant Feed
   - Catalog Attributes Feed
   - Product Prices Feed
   - Scopes Website Data Feed
   - Scopes Customer Groups Data Feed
   - Categories Feed
   - Category Permissions Feed

After verifying the indexers, the next step is to [configure the API keys](#2-configure-api-keys).

>[!TAB Existing Commerce instance]

Follow these instructions if you are installing [!DNL Live Search] on an existing Commerce instance.

1. Confirm that [cron jobs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) and [indexers](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) are running.

1. Use Composer to add the Live Search module to your project:

   ```bash
   composer require magento/live-search --no-update
   ```

1. Update dependencies and install the extension:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Disable the [!DNL Live Search] modules that serve storefront search results.

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing
   ```

   [!DNL Elasticsearch] continues to manage search requests from the storefront while the [!DNL Live Search] service synchronizes catalog data and indexes products in the background.

1. Install the updates.

   ```bash
   bin/magento setup:upgrade
   ```

1. Verify that the following [indexers](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) are set to "Update by Schedule":

   - Product Feed
   - Product Variant Feed
   - Catalog Attributes Feed
   - Product Prices Feed
   - Scopes Website Data Feed
   - Scopes Customer Groups Data Feed
   - Categories Feed
   - Category Permissions Feed

1. Enable the [!DNL Live Search] extension, and disable [!DNL OpenSearch] (Magento Elasticsearch and OpenSearch modules).

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing
   ```

   ```
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_Elasticsearch8 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   >[!NOTE]
   >
   >The disable command includes the list of Commerce modules that support OpenSearch. If your Commerce instance does not have a module installed, you will see a `module does not exist` error.

1. Install the updates.

   ```bash
   bin/magento setup:upgrade
   ```

After verifying the indexers, the next step is to [configure the API keys](#2-configure-api-keys).

>[!ENDTABS]

### Install the [!DNL Live Search] beta

>[!IMPORTANT]
>
>The following feature is in beta. To participate in the beta, send an email request to [commerce-storefront-services](mailto:commerce-storefront-services@adobe.com).

This beta supports three new capabilities in the [`productSearch` query](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/):

- **Layered search** - Search within another search context - With this capability, you can undertake up to two layers of search for your search queries. For example:

  - **Layer 1 search** - Search for "motor" on "product_attribute_1
  - **Layer 2 search** - Search for "part number 123" on "product_attribute_2". This example searches for "part number 123" within the results for "motor".

  Layered search is available for both `startsWith` search indexation and `contains` search indexation as described below:

- **startsWith search indexation** - Search using `startsWith` indexation. This new capability allows:

  - Searching for products where the attribute value starts with a particular string.
  - Configuring an "ends with" search so shoppers can search for products where the attribute value ends with a particular string. To enable an "ends with" search, the product attribute needs to be ingested in reverse, and the API call should also be a reversed string.

- **contains search indexation** -Search an attribute using contains indexation. This new capability allows:

    - Searching for a query within a larger string. For example, if a shopper searches for the product number "PE-123" in the string "HAPE-123".

      >[!NOTE]
      >
      >This search type is different from the existing [phrase search](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase), which performs an autocomplete search. For example, if your product attribute value is "outdoor pants", a phrase search returns a response for "out pan", but does not return a response for "oor ants". A contains search, however, does return a response for "oor ants".

These new conditions enhance the search query filtering mechanism to refine search results. These new conditions do not affect the main search query.

You can implement these new conditions on your search results page. For example, you can add a new section on the page where the shopper can further refine their search results. You can allow shoppers to select specific product attributes, such as "Manufacturer", "Part Number", and "Description". From there, they search within those attributes using the `contains` or `startsWith` conditions. See the Admin guide for a list of searchable [attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types).

1. To install the beta, add the following dependency to your project:

    ```bash
    composer require magento/module-live-search-search-types:"^1.0.0-beta1"
    ```

1. Commit and push the changes to your `composer.json` and `composer.lock` files to your cloud project. [Learn more](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension).

   This beta adds **[!UICONTROL Search types]** checkboxes for **[!UICONTROL Autocomplete]**, **[!UICONTROL Contains]**, and **[!UICONTROL Starts with]** in the Admin. It also updates the [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) GraphQL API to include these new search capabilities.

1. In the Admin, [set a product attribute](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) to be searchable and specify the search capability for that attribute, such as **Contains** (default) or **Starts with**. You can specify a maximum of six attributes to be enabled for **Contains** and six attributes to be enabled for **Starts with**. For beta, be aware that the Admin does not enforce this restriction but it is enforced in API searches.

    ![Specify search capability](./assets/search-filters-admin.png)

1. See the [developer documentation](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) to learn how to update your [!DNL Live Search] API calls using the new `contains` and `startsWith` search capabilities.

### Field descriptions

| Field | Description |
|--- |--- |
|`Autocomplete`| Enabled by default and cannot be modified. With `Autocomplete`, you can use `contains` in the [search filter](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering). Here, the search query in `contains` returns an autocomplete type search response. Adobe recommends you use this type of search for description fields, which typically have more than 50 characters.|
|`Contains`| Enables a true "text contained in a string" search instead of an autocomplete search. Use `contains` in the [search filter](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability). Refer to the [Limitations](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations) for more information.|
|`Starts with`| Query strings which start with a particular value. Use `startsWith` in the [search filter](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability).|

## 2. Configure API keys

The Adobe Commerce API key and its associated private key are required to connect [!DNL Live Search] to an installation of Adobe Commerce. The API key is generated and maintained in the account of the [!DNL Commerce] license holder, who can share it with the developer or systems integrator. The developer can then create and manage the SaaS Data Spaces on behalf of the license holder. If you already have a set of API keys, you do not need to regenerate them.

Learn how to configure your API keys in the [Commerce Services Connector](../landing/saas.md) article.

## 3. Sync your catalog data

[!DNL Live Search] moves catalog data to Adobe's SaaS infrastructure. The data is indexed and search results are delivered from this index directly to the storefront. Depending on the size and complexity, indexing can take from 30 minutes to a couple of hours.

To begin the initial sync of your catalog data to SaaS services, run the following commands in this order:

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

When you run these commands, the initial sync of your catalog data to SaaS services begins.

>[!WARNING]
>
>Search and category browse operations are unavailable during sync. The process can take 1+ hours depending on catalog size.

### Monitor sync progress

Use the [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) to monitor sync progress. This dashboard provides valuable insights into the availability of product data on your storefront, ensuring that it can be promptly displayed to customers.

![Data Management Dashboard](assets/data-management-dashboard.png)

You can also run sync commands and troubleshoot the synchronization process using the [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) and the data export extension logs.

#### Future product updates

After the initial synchronization, it can take up to 15 minutes for incremental product updates to become available to storefront search. To learn more, see [Streaming Product Updates](indexing.md) in the Indexing documentation.

## 4. Verify that the data was exported

To check if your catalog data has been exported from Adobe Commerce and synced with [!DNL Live Search], you have a few options:

- Look for entries in the following tables:

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >If you get a `table does not exist` error, look for entries in the `catalog_data_exporter_products` and `catalog_data_exporter_product_attributes` tables. These table names are used in [!DNL Live Search] versions earlier than 4.2.1.

- Use the [GraphQL playground](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/graphql) with the default query (see [GraphQL reference](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) for more details) to verify the following:

   - The returned product count is close to what you expect for the store view.
   - Facets are returned.

For additional help, see [[!DNL Live Search] catalog not synchronized](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) in the Support Knowledge Base.

## 5. Configure the data

Getting your product data configured correctly ensures good search results for your customers. In this section, you enable the product listing widgets and assign categories.

### Enable product listing widgets

When you install [!DNL Live Search] 4.0.0+, product listing widgets are enabled by default. When widgets are enabled, a different UI component is used for the search results, and category browse product listing pages. This UI component makes direct calls to the [Catalog Service API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/), which results in faster response times.

If you have a [!DNL Live Search] version older than 4.0.0+, you must manually enable the Product Listing Widget.

1. From the *Admin*, go to **[!UICONTROL Stores]** > _[!UICONTROL Settings]_ > **[!UICONTROL Configuration]**.
1. Under **[!UICONTROL Live Search]**, select **[!UICONTROL Storefront Features]**.
1. Set **[!UICONTROL Enable Product Listing Widgets]** to `Yes`.

   ![Enable Product Listing Widgets](assets/ls-admin-enable-widget.png)

When you change this configuration, the message `Page cache is invalidated` appears. You need to flush the Magento Cache to save your change.

1. Access the [Cache Management](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) page by doing one of the following:

   - Click the **[!UICONTROL Cache Management]** link in the message above the workspace.
   - On the _Admin_ sidebar, go to **[!UICONTROL System]** > _[!UICONTROL Tools]_ > **[!UICONTROL Cache Management]**.

1. Select the **Configuration** [!UICONTROL Cache Type] and click **[!UICONTROL Flush Magento Cache]**.

   Changes to the storefront are immediate after you flush the cache.

### Assign categories

Products returned in [!DNL Live Search] must be assigned to a [category](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories). In Luma, for example, products are put into categories such as "Men", "Women", and "Gear". Subcategories are also set up for "Tops", "Bottoms", and "Watches". These category assignments improve granularity when filtering.

## 6. Test the connection

With your catalog data now in SaaS, test to make sure product data is returned in the following scenarios:

- The [!UICONTROL Search] box returns results correctly
- Category browse returns results correctly
- Facets are available as filters on search results pages

If everything works correctly, [!DNL Live Search] is installed, connected, and ready to use.

If you encounter problems in the storefront, check the `var/log/system.log` file for API communication failures or errors on the services side.

To allow [!DNL Live Search] through a firewall, add `commerce.adobe.io` to the allowlist.

## 7. Verify that events are capturing data

Ensure that the storefront events deployed to your site are working. This check is especially important for headless implementations.

- Review the [events](events.md) that are required for [!DNL Live Search].
- Ensure that the [[!DNL Live Search] dashboard](performance.md) is displaying data from your non-production environments.
- [Verify event collection](../product-recommendations/verify.md). While this page is in the [!DNL Product Recommendations] guide, the verification steps apply to [!DNL Live Search] as well.

## 8. Customize for your storefront

You have installed the [!DNL Live Search] extension, synced, validated, and configured your data. The next step is to ensure that the [!DNL Live Search] widgets conform to your store's look and feel.

You can style the popover and PLP widgets by defining custom CSS rules as needed. See [Styling Popover Elements](storefront-popover.md#styling-popover-example) and [product listing page widget](plp-styling.md#styling-example).

If you wish to extend the functionality of the widgets, the source code for each is available in a public repo.
In this scenario, you can customize the JavaScript for your own needs and then host your custom code on your CDN. This custom script communicates with the [!DNL Live Search] service and returns the results like normal, allowing you to control the functionality of the widget.

- [PLP widget repo](https://github.com/adobe/storefront-product-listing-page)
- [Search bar repo](https://github.com/adobe/storefront-search-as-you-type)

## Updating [!DNL Live Search]

Before updating [!DNL Live Search], check the version of [!DNL Live Search] that is installed using Composer.

```bash
composer show magento/module-live-search | grep version
```

To update [!DNL Live Search], run the following from the command line:

```bash
composer update magento/live-search --with-dependencies
```

To update to a major version such as from 3.1.1 to 4.0.0, edit the project's root [!DNL Composer] `.json` file as follows:

1. If your currently installed `magento/live-search` version is `3.1.1` or below, and you are upgrading to version `4.0.0` or higher, run the following command before the upgrade:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   For information about the currently installed `magento/live-search` version, run the following command:

   ```bash
   composer show magento/live-search
   ```

1. Open the root `composer.json` file and search for `magento/live-search`.

1. In the `require` section, update the version number as follows:

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. Save `composer.json`. Then, run the following from the command line:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Uninstalling [!DNL Live Search]

To uninstall [!DNL Live Search], refer to [Uninstall modules](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] packages

The [!DNL Live Search] extension consists of the following packages:

| Package | Description |
|--- |--- |
| `module-live-search` | Allows merchants to configure their search settings for faceting, synonyms, query rules, and so on, and provides access to a read-only GraphQL playground to test queries from the *Admin*. |
| `module-live-search-adapter` | Routes search requests from the storefront to the [!DNL Live Search] service and renders the results in the storefront. <br />- Category browse - Routes requests from the storefront [top navigation](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top) to the search service.<br />- Global search - Routes requests from the [quick search](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) field to the [!DNL Live Search] service. The quick search field is located in the upper-right corner of the storefront page.|
| `module-live-search-storefront-popover` | A "search as you type" popover replaces the standard quick search and returns data and thumbnails of top search results. |

## [!DNL Live Search] dependencies

The [!DNL Composer] metapackage to install the [!DNL Live Search] extension includes the following module dependencies.

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## Advanced concepts

The following sections provide more advanced topics when using [!DNL Live Search] and [!DNL Catalog Service].

### Endpoint

[!DNL Live Search] communicates through the endpoint at `https://catalog-service.adobe.io/graphql`.

As [!DNL Live Search] does not have access to the complete product database, the [!DNL Live Search] GraphQL and Commerce core GraphQL APIs do not have complete parity.

Adobe recommends calling the SaaS APIs directly — specifically the Catalog Service endpoint.

- Gain performance and reduce processor load by bypassing the Commerce database/Graphql process
- Take advantage of the [!DNL Catalog Service] federation to call [!DNL Live Search], [!DNL Catalog Service], and [!DNL Product Recommendations] from a single endpoint.

For some use cases, it maybe better to call [!DNL Catalog Service] for product details and similar cases. See [refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) for more information.

If you have a custom headless implementation, check out the [!DNL Live Search] reference implementations:

- [PLP widget](https://github.com/adobe/storefront-product-listing-page)
- [[!DNL Live Search] field](https://github.com/adobe/storefront-search-as-you-type)

Automatic collection of user interaction data does not work by default if you do not use the standard components like the Search Adapter, Luma widgets, or AEM CIF Widgets. Adobe Sensei uses this collected data for intelligent merchandising and performance tracking. To resolve this issue, you need to develop a custom solution to implement this data collection in a headless manner.

The latest version of [!DNL Live Search] already uses [!DNL Catalog Service].

### Language support

[!DNL Live Search] widgets support the following languages:

|||||
|--- |--- |--- |--- |
|Language|Region| Language Code |Magento Locale|
|Bulgarian|Bulgaria|bg_BG|bg_BG|
|Catalan|Spain|ca_ES|ca_ES|
|Czech|Czech Republic|cs_CZ|cs_CZ|
|Danish|Denmark|da_DK|da_DK|
|German|Germany|de_DE|de_DE|
|Greek|Greece|el_GR|el_GR|
|English|United Kingdom|en_GB|en_GB|
|English|United States|en_US|en_US|
|Spanish|Spain|es_ES|es_ES|
|Estonian|Estonia|et_EE|et_EE|
|Basque|Spain|eu_ES|eu_ES|
|Persian|Iran|fa_IR|fa_IR|
|Finnish|Finland|fi_FI|fi_FI|
|French|France|fr_FR|fr_FR|
|Galician|Spain|gl_ES|gl_ES|
|Hindi|India|hi_IN|hi_IN|
|Hungarian|Hungary|hu_HU|hu_HU|
|Indonesian|Indonesia|id_ID|id_ID|
|Italian|Italy|it_IT|it_IT|
|Korean|South Korea|ko_KR|ko_KR|
|Lithuanian|Lithuania|lt_LT|lt_LT|
|Latvian|Latvia|lv_LV|lv_LV|
|Norwegian|Norway Bokmal|nb_NO|nb_NO|
|Dutch|Netherlands|nl_NL|nl_NL|
|Polish|Poland|pl_PL|pl_PL|
|Portuguese|Brazil|pt_BR|pt_BR|
|Portuguese|Portugal|pt_PT|pt_PT|
|Romanian|Romania|ro_RO|ro_RO|
|Russian|Russia|ru_RU|ru_RU|
|Swedish|Sweden|sv_SE|sv_SE|
|Thai|Thailand|th_TH|th_TH|
|Turkish|Turkey|tr_TR|tr_TR|
|Chinese|China|zh_CN|zh_Hans_CN|
|Chinese|Taiwan|zh_TW|zh_Hant_TW|

If the widget detects that the Commerce Admin language setting matches a supported language, it defaults to that language. Otherwise, the widget default to English. In the Admin, the language setting is configured by navigating to _[!UICONTROL Stores]_ > [!UICONTROL Settings] > _[!UICONTROL Configuration]_ > _[!UICONTROL General]_ > [!UICONTROL Country Options]. 

Admins can also set the language of the [search index](settings.md#language), to help ensure better search results.

### Widget code repository

The code for the product listing page widget and the [!DNL Live Search] field widget is available for download from GitHub.

Developers who have access to the code can completely customize how it works and looks. They host the code on their own servers but still use the [!DNL Live Search] service.

- [PLP widget](https://github.com/adobe/storefront-product-listing-page)
- [Search bar](https://github.com/adobe/storefront-search-as-you-type)

### Data Export extension

After [!DNL Live Search] is enabled, the Data Export extension synchronizes Commerce data between the Commerce application and [!DNL Live Search]. This process ensures that the most current Commerce data is available on the storefront. In the Admin, you can check synchronization status using the Data Management dashboard. You can manage and troubleshoot the data export process using the Commerce CLI and logs. For details, see the [Data Export Guide](../data-export/overview.md).

### Inventory management

[!DNL Live Search] supports [Inventory Management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) capabilities in Commerce (formerly knows as Multi-Source Inventory, or MSI). To enable full support, you must [update](install.md#updating-live-search) the dependency module `commerce-data-export` to version 102.2.0+.

[!DNL Live Search] returns a boolean noting whether a product is available within Inventory Management, but does not contain information about which source has the stock.

### Price indexer

[!DNL Live Search] customers can use the [SaaS price indexer](../price-index/price-indexing.md), which provides faster price change updates and synchronization time.

### Price support

[!DNL Live Search] widgets support most but not all price types supported by Adobe Commerce.

Currently, basic prices are supported. Advanced prices that are not supported are:

- Cost
- Minimum Advertised Price

Look at [API Mesh](../catalog-service/mesh.md) for more complex price calculations.

The price format supports the locale configuration setting within the Commerce instance: *Stores* > Settings > *Configuration* > General > *General* > Local Options > Locale.

### Headless storefront support

Optionally, you might need to install the `module-data-services-graphql` module that expands the application's existing GraphQL coverage to include fields required for storefront behavioral data collection.

   ```bash
   composer require magento/module-data-services-graphql
   ```

This module adds additional contexts to GraphQL queries:

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### B2B support

[!DNL Live Search] supports [B2B functionality](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview) with additional [limitations](boundaries-limits.md#b2b-and-category-permissions).

### PWA support

[!DNL Live Search] works with PWA Studio but users might see slight differences compared to other Commerce implementations. Basic functionality such as search and product listing page work in Venia but some permutations of Graphql might not work correctly. There might also be performance differences.

- The current PWA implementation of [!DNL Live Search] requires more processing time to return search results than [!DNL Live Search] with the native Commerce storefront.
- [!DNL Live Search] in PWA does not support [event handling](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). As a result, search reporting and intelligent merchandising do not work on PWA storefronts.
- When using [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/), GraphQL does not support filtering directly on `description`, `name`, `short_description`, but these fields can be returned with a more general filter.

To use [!DNL Live Search] with PWA Studio, integrators must also:

1. Install [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Set the `environmentId` in the `storeDetails` object.

    ```javascript
    const storeDetails: StoreDetailsProps = {
        environmentId: <Storefront_ID>,
        websiteCode: "base",
        storeCode: "main_website_store",
        storeViewCode: "default",
        searchUnitId: searchUnitId,
        config: {
            minQueryLength: 5,
            pageSize: 8,
            currencySymbol: "$",
            },
        };
    ```

### Cookies

[!DNL Live Search] collects user interaction data as part of its base functionality and cookies are used to store this data. When collecting any user information, the user must agree to store cookies. [!DNL Live Search] and [!DNL Product Recommendations] share the data stream and therefore the same cookie mechanism. Read more about it in [Handle Cookie Restrictions](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/setting-cookie).
