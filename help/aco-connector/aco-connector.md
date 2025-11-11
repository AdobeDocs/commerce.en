---
title: Adobe Commerce Optimizer Connector for Commerce
description: Learn how to connect your data from your Commerce cloud or on-premises project to Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
hidefromtoc: yes
hide: yes
---

# Overview

The Adobe Commerce Connector is the integration bridge that synchronizes catalog and pricing data between an existing Adobe Commerce Cloud on cloud or on-premises deployment and Adobe Commerce Optimizer composable catalog data model. This enables features such as dynamic AI search, recommendations, fast-loading headless storefronts, including Adobe Commerce storefronts on Edge Delivery Services, and real-time performance analytics.

## Architecture and experience

The Adobe Commerce Connector operates by mapping Commerce's `website/store/storeview` catalog hierarchy to Adobe Commerce Optimizer `channel/policy/source` data model.

Instead of configuring and managing Commerce Services (Live Search and Product Recommendations) from the Commerce Admin, you use [Adobe Commerce Optimizer Merchandising tools](../optimizer/merchandising/overview.md) to manage product discovery (Live Search) and recommendations (Product Recommendations) rule configuration.  The Adobe Commerce instance becomes the data-origin for catalog and price data. When the data is updated in Commerce, the updates are synced to the Adobe Commerce Optimizer instance.

## Workflows

The Connector enables several key workflows:

* Export Commerce catalog data to Adobe Commerce Optimizer—price and price book data is exported at the `website` level. Product and product attribute data is exported at the `store view` level. By default, catalog data sync is enabled for all Commerce scopes (websites and store views).

  To enable this workflow, use Composer to install the `adobe-commerce/commerce-data-export-aco-adapter` PHP extension, and then provide the IMS credentials to authenticate the connection between the Commerce project.

* Map the Commerce `website/store/storeview` data to export to Adobe Commerce Optimizer

  You have the option to customize the Adobe Commerce Optimizer exporter settings to export data only for specific scopes by updating the exporter configuration from the Store grid in Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

  * At the `website` level, disabling the exporter setting stops the export of prices and price book data to Adobe Commerce Optimizer.

  * At the `storeview` level, disabling the exporter setting stops the export of products and product attributes to Adobe Commerce Optimizer.

  When the configuration is changed, the corresponding indexes are invalidated to trigger re-export of the affected entities.

* Merchandising rule configuration and management

  When the Connector is enabled, merchandising rules for product discovery and recommendations are defined and managed from Adobe Commerce Optimizer UI, not from the [!UICONTROL Live Search] and [!UICONTROL Product Recommendations] pages in the Commerce Admin.

## Get started

## Install Commerce Connector packages

The Adobe Commerce Connector PHP extension is available to all Commerce merchants with an active license for Adobe Commerce Optimizer.

**Requirements**

* PHP 8.1, 8.2, 8.3, or 8.4
* Adobe Commerce 2.4.4+
* Access to [repo.magento.com](https://repo.magento.com) to download the extension via Composer.
* Admin access to an [Adobe Commerce Optimizer sandbox instance](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).
* [Developer access to the organization where the Adobe Commerce Optimizer is provisioned](../optimizer/user-management.md#add-users-developers-and-product-profile-admins)
* [Command line to the Adobe Commerce application server](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

**Prerequisites**

Gather the following information before you begin the installation:

* Adobe Commerce Optimizer instance ID

  You can find the instance ID in the URL of your Adobe Commerce Optimizer instance. For example, in the URL `https://optimizer.adobe.com/instances/1234567890abcdef`, the instance ID is `1234567890abcdef`.

* Adobe Commerce Optimizer IMS credentials (`client_id` and `client_secret`) associated with your Adobe Commerce Optimizer Developer project.

  Log in to the [Adobe Developer Console](https://developer.adobe.com/console) and navigate to your Adobe Commerce Optimizer project to find the IMS credentials. If you do not have an Adobe Commerce Optimizer project, create one and [generate the IMS credentials](../optimizer/get-started/get-ims-credentials.md).

### Installation steps

1. Add the `adobe-commerce/commerce-data-export-aco-adapter` module using Composer:

  ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
  ```

1. Deploy the changes to your Adobe Commerce staging environment.

  After your changes are deployed, the Commerce Optimizer Optimizer option is available in the Commerce Admin menu.

For detailed extension installation instructions, see the following guides:

* [Install extension on Adobe Commerce on Cloud Infrastructure](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)

* [Install extension Adobe Commerce on-premises](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Configure the Adobe Commerce Optimizer integration

Configure the Adobe Commerce Optimizer integration to connect the Commerce project environment to your Adobe Commerce Optimizer instance.

>[!IMPORTANT]
>
>After you run the command to configure the integration, the data sync for Commerce product and price data starts automatically. Depending on the size of your catalog, the initial sync can take several hours to complete.

1. Gather the values required to configure the connection to Adobe Commerce Optimizer project.

   * Organization ID (`org_id`)
   * Adobe Commerce Optimizer Instance ID (tenant_id)
   * Region (`region`)
   * Adobe Commerce Optimizer IMS `client_id` and `client_secret`

1. From the Commerce Admin, select **[!UICONTROL Adobe Commerce Optimizer]** to display the configuration page with instructions.

   ![Adobe Commerce Optimizer configuration page](./assets/aco-connector-config-page.png)

1. From the command line, use SSH to connect to the Commerce staging environment for your project.

1. Run the following Commerce CLI command to configure the integration, replacing the placeholder values with the values for your Commerce Optimizer project:

  ```bin/magento aco:config:init --org_id=your_org_id --tenant_id=your_tenant_id --client_id=your_client_id --client_secret=your_client_secret --region=na1 --type=sandbox```

1. Verify the connection by returning to the Commerce Admin and selecting the [!UICONTROL Adobe Commerce Optimizer] option.

   When you click the option, it opens the Adobe Commerce Optimizer UI in a new tab.

1. From the Adobe Commerce Optimizer UI, you can see the data synced to Commerce Optimizer by selecting the **[!UICONTROL Data Sync]** option from the left navigation menu.

   When the initial sync is complete, the status displays as **Healthy**.

