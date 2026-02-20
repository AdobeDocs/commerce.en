---
title: Adobe Commerce Optimizer Connector
description: Learn how to connect your data from your Commerce cloud or on-premises project to Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
hidefromtoc: yes
hide: yes
---

# Adobe Commerce Optimizer Connector

The Adobe Commerce Optimizer Connector is the integration bridge that synchronizes catalog and pricing data between an Adobe Commerce on cloud infrastructure or on-premises deployment and [!DNL Adobe Commerce Optimizer] composable catalog data model. This enables features such as dynamic AI search, recommendations, fast-loading headless storefronts, including Adobe Commerce storefronts on Edge Delivery Services, and real-time performance analytics.

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

## Architecture and experience

The Adobe Commerce Optimizer Connector operates by mapping Commerce websites and store views to a Commerce Optimizer project:

* Commerce store views are mapped to catalog sources
* Websites are mapped to price books

The associated catalog and price data is exported and later used to create catalog views and optionally define a policy to filter the catalog and price data for specific business use cases.

Instead of configuring and managing Commerce Services (Live Search and Product Recommendations) from the Commerce Admin, you use [[!DNL Adobe Commerce Optimizer] Merchandising tools](../optimizer/merchandising/overview.md) to manage product discovery (Live Search) and recommendations (Product Recommendations) rule configuration. The Adobe Commerce instance becomes the data source for catalog and price data. When the data is updated in Commerce, the updates are synced to the [!DNL Adobe Commerce Optimizer] instance.

## Workflows

The Connector enables several key workflows:

* **Export Commerce catalog data to [!DNL Adobe Commerce Optimizer]**—price and price book data is exported at the `website` and `customer group` level. Product and product attribute data is exported at the `store view` level. By default, catalog data sync is enabled for all Commerce scopes (websites and store views).

  To enable this workflow, use Composer to install the `adobe-commerce/commerce-data-export-aco-adapter` PHP extension, and then provide the IMS credentials to establish the connection between the Commerce and [!DNL Adobe Commerce Optimizer] environments.

* **Map the Commerce `website/store/storeview` data to export to [!DNL Adobe Commerce Optimizer]**

  Optionally, customize the export settings to sync data only for specific websites or store views. See [Customize Commerce data export configuration](#customize-commerce-data-export-configuration).

* **Merchandising rule configuration and management**

  When the Connector is enabled, merchandising rules for product discovery and recommendations are defined and managed from the [!DNL Adobe Commerce Optimizer] UI, not from the [!UICONTROL Live Search] and [!UICONTROL Product Recommendations] pages in the Commerce Admin.

* **Deploy your Commerce Storefront on Edge Delivery Services**

  After setting up the integration with [!DNL Adobe Commerce Optimizer], you can set up and deploy a Commerce Storefront on Edge Delivery Services to deliver ultra-fast performance, scalability, seamless content authoring, integrated personalization, and reduced operational costs using the composable, API-driven architecture and modular components available with [!DNL Adobe Commerce Optimizer].

## Requirements to use the integration

* Adobe Commerce 2.4.7+

  * PHP 8.2, 8.3, or 8.4
  * Composer 2.x

* [!DNL Adobe Commerce Optimizer] license with a provisioned sandbox instance.

* Access to [repo.magento.com](https://repo.magento.com) to download the Commerce Connector metapackage using Composer.

* Admin access to an [Adobe Commerce Optimizer sandbox instance](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

The Adobe Commerce user configuring the integration must have:

* Administrator access to the Adobe Commerce Admin.

* [Command line access to the Adobe Commerce application server](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Developer access to the [IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) where the [!DNL Adobe Commerce Optimizer] project is provisioned.

## Get Started

1. **Set up the Integration**

   1. [Install the Commerce Optimizer Connector package](#install-the-commerce-connector-package).

   1. [Customize the data export configuration](#customize-commerce-data-export-configuration) (optional).

   1. [Get the required values for configuring the Commerce Optimizer connection](#get-required-values-for-configuring-the-commerce-optimizer-connection).

   1. [Enable the [!DNL Adobe Commerce Optimizer] integration](#enable-the-adobe-commerce-optimizer-integration).

   1. [Verify that the data sync is working](#verify-that-the-data-sync-is-working).

1. **[Configure [!DNL Adobe Commerce Optimizer] catalog views and policies](#configure-adobe-commerce-optimizer-stores)**

1. **[Set up a Commerce Storefront on Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Install the Commerce Optimizer Connector package

The Adobe Commerce Optimizer Connector is delivered as a Composer metapackage that is available to all Commerce merchants with an active license for [!DNL Adobe Commerce Optimizer].

For detailed instructions, see [Uninstall modules](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions/uninstalling-modules/).

### Installation steps

1. Add the `adobe-commerce/commerce-data-export-aco-adapter` module using Composer:

  ```shell
  composer require adobe-commerce/commerce-data-export-aco-adapter
  ```

1. Deploy the changes to your Adobe Commerce staging environment.

  After your changes are deployed, the Commerce Optimizer option is available in the Commerce Admin menu.

>[!NOTE]
>
>For detailed extension installation instructions, see the following guides:
>
>[Install extension on Adobe Commerce on Cloud Infrastructure](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Install extension on Adobe Commerce on-premises](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Get required values for configuring the Commerce Optimizer connection

### Get API credentials

>[!NOTE]
>
>If you already have a developer project configured with the Data Ingestion API in the IMS organization where your Commerce Optimizer instance is deployed, you can get the required API credentials and organization ID from the OAUTH-server-to-server credentials in that project.

Create a new developer project in Adobe Developer console to get [!DNL Adobe Commerce Optimizer] Ingestion API credentials to configure the integration between Commerce and Commerce Optimizer instances. For instructions, see [Obtain IMS Credentials](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) in the *Merchandising Developer Guide*.

After you create the project, save the following values from the OAUTH Server-to-Server credentials page:

* **Organization ID** (`org_id`)

* **IMS `client_id` and `client_secret`**

### Get [!DNL Adobe Commerce Optimizer] instance details

Save the following values from your [!DNL Adobe Commerce Optimizer] instance details.

* **Instance ID—**The unique identifier for your [!DNL Adobe Commerce Optimizer] instance. Also known as the tenant ID.

  Get the instance ID from the URL to access your [!DNL Adobe Commerce Optimizer] instance. For example, in the URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, the instance ID is `1234567890abcdef`.

## Customize the Commerce data export configuration

By default, catalog data sync is enabled for all Commerce scopes (websites and store views). You can customize the export settings to sync data only for specific scopes based on your business needs. For example, if you have multiple store views but only want to export data for one of them, you can disable the exporter for the other store views.

>[!IMPORTANT]
>
>Changing export settings triggers a full re-indexation, which can take significant time depending on your catalog size. Plan these changes during low-traffic periods to minimize performance impact.

### Data export by scope

The following table describes what data is exported at each scope level:

| Scope | Data exported | Notes |
| ------- | --------------- | ------- |
| Website | Prices and price books | Each set of prices is exported as a [price book](../optimizer/setup/pricebooks.md) using the naming convention `website::customergroupcode`. All customer groups for the website are included. |
| Store view | Products and product attributes | Each store view creates a separate catalog source in [!DNL Adobe Commerce Optimizer]. |

### Enable and disable behavior

| Action | Result |
| -------- | -------- |
| Disable a store view | The catalog source remains in [!DNL Adobe Commerce Optimizer], but all data is removed. |
| Disable then re-enable a store view | The same catalog source is repopulated with a full data resynchronization. |

### Update the export configuration

After you install the Connector package, the Store grid in the Admin now shows the export configuration settings for Commerce Optimizer.

![Store Grid with Commerce Optimizer sync settings](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**To change the settings for a website or store view:**

1. In the Commerce Admin, navigate to **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**.

1. Select the website or store view you want to configure.

1. In the **[!DNL Adobe Commerce Optimizer] exporter settings**, use the checkbox to enable or disable the data sync as needed.

  ![Update data sync configuration](./assets/aco-connector-store-website-export-settings.png){width="600" zoomable="yes"}

1. Save your changes.

## Enable the [!DNL Adobe Commerce Optimizer] integration

>[!IMPORTANT]
>
>Data sync processing starts as soon as you run the configuration command. By default, catalog data sync is enabled for all Commerce scopes (websites and store views). Depending on the size of your catalog, the data sync process can take from a few minutes to several hours.

Using the API credentials and instance details you gathered in the previous steps, you can now configure the integration between your Commerce and [!DNL Adobe Commerce Optimizer] instances.

1. From the Commerce Admin, select **[!UICONTROL Adobe Commerce Optimizer]** to display the configuration page with instructions.

   ![[!DNL Adobe Commerce Optimizer] configuration page](../assets/aco-connector-config-page.png)

1. From the command line, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) to connect to the Commerce staging environment.

1. Run the following Commerce CLI command to configure the integration, replacing the placeholder values with the values for your Commerce Optimizer project:

  ```terminal
  bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
  ```

1. Verify the connection by returning to the Commerce Admin and selecting the [!UICONTROL Adobe Commerce Optimizer] option.

   When you click the option, it opens the [!DNL Adobe Commerce Optimizer] UI in a new tab.

## Verify that the data sync is working

Check the data sync from both the Commerce Admin and Commerce Optimizer.

1. Verify that catalog data is flowing from Commerce to Commerce Optimizer:

   From the Commerce Admin, open the [!UICONTROL Data Feed Sync Status] page by selecting **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]****.

    ![Data Feed Sync Status page with feed item status reporting](./assets/data-feed-sync-status.png){width="600" zoomable="yes"}

    If the data sync has started, the feed data shows successfully sent records. You can also view and troubleshoot sync issues by viewing the details for each feed.

1. Verify that Adobe Commerce Optimizer is receiving the catalog data:

   From the Commerce Optimizer menu, select **[!UICONTROL Data Sync]** to open the Data Sync page.

   ![Data Sync](./assets/data-sync.png){width="600" zoomable="yes"}


>[!TIP]
>
>If you have any issues with the data sync, see the [Troubleshooting](/help/data-export/troubleshooting-logging.md) section in the *SaaS Data Export* documentation.

## Configure [!DNL Adobe Commerce Optimizer] stores

Configure [!DNL Adobe Commerce Optimizer] stores by creating catalog views and policies.​ See [Creating Catalog Views](../optimizer/setup/catalog-view.md) in the [!DNL Adobe Commerce Optimizer] Guide.

Note that price books are created automatically from Adobe Commerce customer groups.

## Set up a Commerce Storefront on Edge Delivery Services

This section provides a high-level overview of the steps required to set up your Commerce storefront. Detailed information is available in the [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) documentation site.

1. **Clone and deploy Adobe Commerce Storefront boilerplate** using the [Site Creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. **[Set up a local development environment](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)** to run and test the storefront locally before deploying to Edge Delivery Services.

1. **[Install GraphQL Storefront Compatibility package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)** on your Commerce instance to ensure that the necessary GraphQL endpoints are available for the storefront to connect to.

1. **[Configure CORS headers for Commerce instance in cloud environment](#configure-cors-headers-for-commerce-instance)** to enable GraphQL requests from an Edge Delivery storefront to your Commerce Optimizer instance.

1. **[Connect the storefront to Commerce data sources](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)**.



