---
title: Adobe Commerce Optimizer Connector
description: Learn how to connect your data from your Commerce cloud or on-premises project to Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
hidefromtoc: yes
hide: yes

---

# Adobe Commerce Optimizer Connector for Commerce

The Adobe Commerce Connector is the integration bridge that synchronizes catalog and pricing data between an existing Adobe Commerce Cloud on cloud or on-premises deployment and Adobe Commerce Optimizer composable catalog data model. This enables features such as dynamic AI search, recommendations, fast-loading headless storefronts, including Adobe Commerce storefronts on Edge Delivery Services, and real-time performance analytics.

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

## Architecture and experience

The Adobe Commerce Connector operates by mapping Commerce's `website/store/storeview` catalog hierarchy to Adobe Commerce Optimizer `channel/policy/source` data model.

Instead of configuring and managing Commerce Services (Live Search and Product Recommendations) from the Commerce Admin, you use [Adobe Commerce Optimizer Merchandising tools](../optimizer/merchandising/overview.md) to manage product discovery (Live Search) and recommendations (Product Recommendations) rule configuration.  The Adobe Commerce instance becomes the data-origin for catalog and price data. When the data is updated in Commerce, the updates are synced to the Adobe Commerce Optimizer instance.

## Workflows

The Connector enables several key workflows:

* **Export Commerce catalog data to Adobe Commerce Optimizer**—price and price book data is exported at the `website` level. Product and product attribute data is exported at the `store view` level. By default, catalog data sync is enabled for all Commerce scopes (websites and store views).

  To enable this workflow, use Composer to install the `adobe-commerce/commerce-data-export-aco-adapter` PHP extension, and then provide the IMS credentials to authenticate the connection between the Commerce project.

* **Map the Commerce `website/store/storeview` data to export to Adobe Commerce Optimizer**

  You have the option to customize the Adobe Commerce Optimizer exporter settings to export data only for specific scopes by updating the exporter configuration from the Store grid in Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* **Merchandising rule configuration and management**

  When the Connector is enabled, merchandising rules for product discovery and recommendations are defined and managed from Adobe Commerce Optimizer UI, not from the [!UICONTROL Live Search] and [!UICONTROL Product Recommendations] pages in the Commerce Admin.

* **Deploy your Commerce Storefront on Edge Delivery Services**

  After setting up the integraation with Adobe Commerce Optimizer, you can set up and deploy a Commerce Storefront on Edge Delivery services to deliver ultra-fast performance, scalability, seamless content authoring, integrated personalization, and reduced operational costs using the composable, API-driven architecture and modular components available with Adobe Commerce Optimizer.  

## Requirements to use the integration

* Adobe Commerce 2.4.7+

  * PHP 8.2, 8.3, or 8.4
  * Composer 2.x

* Adobe Commerce Optimizer license with a provisioned sandbox instance.

* Access to [repo.magento.com](https://repo.magento.com) to download the Commerce Connector metapackage using Composer.

* Admin access to an [Adobe Commerce Optimizer sandbox instance](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

The Adobe Commerce user configuring the integration must have:

* Administrator access to the Adobe Commerce Admin.

* [Command line access to the Adobe Commerce application server](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Developer access to the [IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) where the Adobe Commerce Optimizer project is provisioned.

## Get Started

1. **Set up the Integration**

   1. [Install the Commerce Connector package](#install-the-commerce-connector-package).

   1. [Get the required values for configuring the Commerce Optimizer connection](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Enable the Adobe Commerce Optimizer integration](#enable-the-adobe-commerce-optimizer-integration).

   1. [Verify that the data sync is working](#verify-that-the-data-sync-is-working).

   1. [Customize the data export configuration](#customize-commerce-data-export-configuration) (optional).

1. **[Configure Adobe Commerce Optimizer stores](#configure-adobe-commerce-optimizer-stores)**

1. **[Set up a Commerce Storefront on Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Install the Commerce Connector package

The Adobe Commerce Connector Composer metapackage is available to all Commerce merchants with an active license for Adobe Commerce Optimizer.

### Installation steps

1. Add the `adobe-commerce/commerce-data-export-aco-adapter` module using Composer:

  ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
  ```

1. Deploy the changes to your Adobe Commerce staging environment.

  After your changes are deployed, the Commerce Optimizer Optimizer option is available in the Commerce Admin menu.

>[!NOTE]
>
>For detailed extension installation instructions, see the following guides:
>
>[Install extension on Adobe Commerce on Cloud Infrastructure](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Install extension Adobe Commerce on-premises](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Get required values for configuring the Commerce Optimizer connection

### Get API credentials

>[!NOTE]
>
>If you already have a developer project configured with the Data Ingestion API in the IMS organization where your Commerce Optimizer instance is deployed, you can get the required API credentials and organization ID from the OAUTH-server-to-server credentials in that project.

Create a new developer project in Adobe Developer console to get Adobe Commerce Optimizer Ingestion API credentials to configure the integration between Commerce and Commerce Optimizer instances. For instructions, see [Obtain IMS Credentials](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) in the *Merchandising Developer Guide*.

After you create the project with the , save the following values from the OAUTH Server-to-Server credentials page:

* **Organization ID** (`org_id`)

* **IMS `client_id` and `client_secret`**

### Get Adobe Commerce Optimizer instance details

Save the following values from your Adobe Commerce Optimizer instance details.

* **Instance ID—**The unique identifier for your Adobe Commerce Optimizer instance. Also known as the tenant ID.

  Get the instance ID from the URL to access your Adobe Commerce Optimizer instance. For example, in the URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, the instance ID is `1234567890abcdef`.

* **Region—**The region where your Adobe Commerce Optimizer sandbox instance is hosted.

  Get the region from the Adobe Commerce Optimizer URL. For example, in the URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, the region is `na1`.

## Enable the Adobe Commerce Optimizer integration

>[!IMPORTANT]
>
>Data sync processing starts as as you run the configuration command. By default, catalog data sync is enabled for all Commerce scopes (websites and store views). Depending on the size of your catalog, the data sync process can take many hours.

Using the API credentials and instance details you gathered in the previous steps, you can now configure the integration between your Commerce and Adobe Commerce Optimizer instances.

1. From the Commerce Admin, select **[!UICONTROL Adobe Commerce Optimizer]** to display the configuration page with instructions.

   ![Adobe Commerce Optimizer configuration page](../assets/aco-connector-config-page.png)

1. From the command line, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) to connect to the Commerce staging environment.

1. Run the following Commerce CLI command to configure the integration, replacing the placeholder values with the values for your Commerce Optimizer project:

  ```terminal
  bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
  ```

1. Verify the connection by returning to the Commerce Admin and selecting the [!UICONTROL Adobe Commerce Optimizer] option.

   When you click the option, it opens the Adobe Commerce Optimizer UI in a new tab.

## Verify that the data sync is working

You can check the data sync from both the Commerce Admin and Commerce Optimizer.

* The **[Data Feed Sync Status page](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)** shows the progress of the catalog data synchronization from Commerce to Adobe Commerce Optimizer.

* The **[[!UICONTROL Data Sync] page](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)** in Adobe Commerce Optimizer shows the catalog data transferred from your Commerce instance.

1. Verify that catalog data is flowing from Commerce to Commerce Optimizer:

   From the Commerce Admin, open the [!UICONTROL Data Feed Sync Status] page by selecting [!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.

    ![Data Feed Sync Status page with feed item status reporting](./assets/data-feed-sync-status.png)

    If the data sync has started, the feed data shows successfully sent records. You can also view and troubleshoot sync issues by viewing the details for each feed.

1. Verify that Adobe Commerce Optimizer is receiving the catalog data:

   From the Commerce Optimizer menu, select **[!UICONTROL Data Sync]** to open the Data Sync page.

   ![Data Sync](./assets/data-sync.png)

### Troubleshooting

If the data sync has not started, ensure that the catalog indexes are valid. If the indexes are invalid, run the following command from the Commerce CLI to reindex the catalog data:

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Customize Commerce data export configuration

You have the option to customize the Adobe Commerce Optimizer exporter settings to export data only for specific scopes by updating the exporter configuration from the Store grid in Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* At the `website` level, disabling the exporter setting stops the export of prices and price book data to Adobe Commerce Optimizer.

* At the `storeview` level, disabling the exporter setting stops the export of products and product attributes to Adobe Commerce Optimizer.

When the configuration is changed, the corresponding indexes are invalidated to trigger re-export of the affected entities.

## Configure Adobe Commerce Optimizer stores

Configure Adobe Commerce Optimizer stores by creating catalog views and policies.​ See [Creating Catalog Views](../optimizer/setup/catalog-view.md) in the Adobe Commerce Optimizer Guide.

Note that price books are created automatically from Adobe Commerce customer groups.

## Set up a Commerce Storefront on Edge Delivery Services

This section provides a high-level overview of the steps required to set up your Commerce storefront. Detailed information is available in the [Adobe Commerce Storefront] (https://experienceleague.adobe.com/developer/commerce/storefront/) documentation site.

1. Clone and deploy Adobe Commerce Storefront boilerplate to EDS using the [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. [Set up a local development environment](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment).

1. [Install GraphQL Storefront Compatibility package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).​

1. [Configure CORS headers for Commerce instance in cloud environment](#configure-cors-headers-for-commerce-instance).

1. [Connect the storefront to Commerce data sources](#connect-the-storefront-to-commerce-data-sources).

### Configure CORS headers for Commerce instance

To allow GraphQL requests to come from an Edge Delivery Services (EDS) storefront to Adobe Commerce on cloud or on-premises environment, add specific Cross-Origin Resource Sharing (CORS) headers to the Adobe Commerce GraphQL endpoints.​ For instructions, see [CORS setup](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/) in the *Adobe Commerce Storefront* documentation.

### Connect the storefront to Commerce data sources

In the GitHub repository for the Storefront boilerplate code, update the storefront configuration file, `config.json` with the following parameters:

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`, for example `https://{{your store}}/graphql`.

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"`, for example `https://na1-sandbox.api.commerce.adobe.com/{{instanceId}}/v1/catalog​`.

* `"AC-Environment-Id": "Customer organization ID"` - Get this value from the [Commerce cloud project](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/overview#project-overview).

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` - Get this value from the [catalog view details](../optimizer/setup/catalog-view.md#view-details) in Adobe Commerce Optimizer.

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` — Get this value from the list of assigned price books in the [catalog view details](../optimizer/setup/catalog-view.md#view-details) in Adobe Commerce Optimizer.

* `"AC-Source-Locale": "catalogSource"`— Specify the source associated with the Commerce storeview to connect to the storefront. You can see available sources from the [Data Sync](../optimizer/setup/data-sync.md) page in Adobe Commerce Optimizer.

For more information, see [Storefront configuration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/) in the *Adobe Commerce Storefront* documentation.


