---
title: 'Get Started with the [!DNL Adobe Commerce Optimizer Connector]'
description: "Learn how to install the [!DNL Adobe Commerce Optimizer Connector], configure scope export settings, enable IMS authentication, and verify catalog synchronization."
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T16:55:50.934Z'
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization

---

# Get started

Install and configure the [!DNL Adobe Commerce Optimizer Connector] to sync your [!DNL Adobe Commerce] catalog data with [!DNL Adobe Commerce Optimizer], then monitor the data sync status to ensure your storefront is up to date.

{{aco-integration-environment-alignment}}

## Requirements to use the integration {#requirements-to-use-the-integration}

* [!DNL Adobe Commerce] 2.4.7+

  * PHP 8.2, 8.3, or 8.4
  * Composer 2.x

* [!DNL Commerce Optimizer] license with a provisioned sandbox instance.

* [Authentication keys](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) to download the connector metapackage using Composer.

* Admin access to an [[!DNL Commerce Optimizer] sandbox instance](../optimizer/get-started.md).

The [!DNL Adobe Commerce] user configuring the integration must have:

* Administrator access to the Commerce Admin.

* [Command line access to the [!DNL Adobe Commerce] application server](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Developer access to the [IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) where the [!DNL Commerce Optimizer] project is provisioned.

>[!BEGINSHADEBOX]

## Remove conflicting extensions {#remove-conflicting-extensions}

If you have any of the following extensions installed, uninstall them before installing the [!DNL Adobe Commerce Optimizer Connector]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

Data associated with these extensions is still available in the Commerce database. However, it is not exported to [!DNL Commerce Optimizer] when the connector is enabled. To implement the search and merchandising capabilities provided by these extensions after enabling the connector, configure them from the [[!DNL Commerce Optimizer] Admin UI](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>If these extensions are not removed before enabling the connector, you may see broken configuration screens, duplicate data in [!DNL Commerce Optimizer] because the same data is exported from both the connector and the existing extensions, and 401 or 403 errors in the logs due to conflicts in the way the extensions and the connector authenticate with the connected services.

>[!ENDSHADEBOX]

## Configuration steps

Follow these steps to enable the [!DNL Adobe Commerce Optimizer Connector] and begin synchronizing data from [!DNL Adobe Commerce] to your [!DNL Commerce Optimizer] instance.

1. **[Install the [!DNL Adobe Commerce Optimizer Connector] package](#install-the-adobe-commerce-optimizer-connector-package)** using Composer to connect your [!DNL Adobe Commerce] instance to [!DNL Commerce Optimizer].

1. **[Customize the Commerce scopes export configuration](#customize-the-commerce-scopes-export-configuration)** from the Admin.

1. **[Enable the [!DNL Commerce Optimizer] integration](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verify that the data sync is working](#verify-that-the-data-sync-is-working)**.

## Install the [!DNL Adobe Commerce Optimizer Connector] package {#install-the-adobe-commerce-optimizer-connector-package}

The [!DNL Adobe Commerce Optimizer Connector] is delivered as a Composer metapackage available to all Commerce merchants with an active license for [!DNL Commerce Optimizer].

### Installation steps

1. Add the `adobe-commerce/commerce-data-export-aco-adapter` module using Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Deploy the changes to your [!DNL Adobe Commerce] staging environment.

   After deployment completes, the [!DNL Commerce Optimizer] option is available from the Commerce Admin menu. Select **[!UICONTROL Commerce Optimizer]** to open your [!DNL Commerce Optimizer] instance directly from the Commerce Admin.

>[!NOTE]
>
>For detailed extension installation instructions, see the following guides:
>
>[Install extension on [!DNL Adobe Commerce] on Cloud Infrastructure](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Install extension on [!DNL Adobe Commerce] on-premises](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Customize the Commerce scopes export configuration {#customize-the-commerce-scopes-export-configuration}

By default, catalog data sync is enabled for all Commerce scopes (websites, customer groups, and store views). You can customize the export settings to sync data only for specific scopes based on your business needs. For example, if you have multiple store views that share the same language, you can choose to export data for only one of the store views and use it as the [catalog source](../optimizer/setup/catalog-sources.md) for multiple catalog views in [!DNL Commerce Optimizer].

>[!IMPORTANT]
>
>Changing export settings triggers a full re-indexation, which can take significant time depending on your catalog size. Adobe recommends configuring the Commerce scopes to sync to [!DNL Commerce Optimizer] before enabling the integration and starting the initial data sync.

The following table describes what data is exported at each scope level:

| Scope | Data exported | Notes |
| ----- | ------------- | ----- |
| Website and customer group | Prices and price books | Each set of prices is exported as a [price book](../optimizer/setup/pricebooks.md) using the naming convention `&lt;website&gt;::&lt;SHA1 of customer group ID&gt;`. All customer groups for the website are included. |
| Store view | Products and product attributes | Each store view creates a separate [catalog source](../optimizer/setup/catalog-sources.md) in [!DNL Commerce Optimizer]. |

![Store Grid with Commerce Optimizer sync settings](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

### To change scope export settings

1. In the Commerce Admin, go to **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Select the website or store view you want to configure.

1. In the **[!DNL Commerce Optimizer] exporter settings**, use the checkbox to enable or disable the data sync as needed.

   ![Update data sync configuration](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. Save your changes.

### Enable and disable behavior

| Action | Result |
| -------- | -------- |
| Disable a store view | The catalog source remains in [!DNL Commerce Optimizer], but all data is removed. |
| Disable then re-enable a store view | The same catalog source is repopulated with a full data resynchronization. |

## Enable the [!DNL Commerce Optimizer] integration

You enable the integration and initiate the data sync by running the `aco:config:init` CLI command. This command completes the following steps:

1. Obtains an IMS access token using credentials supplied as command line arguments.
1. Calls the Commerce Cloud Manager (CCM) service at `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` to validate the tenant and extract the ingestion URL and [!DNL Commerce Optimizer] Studio URL.
1. Saves all configuration (client secret encrypted) to `core_config_data`.
1. Schedules the initial full sync by invalidating all [!DNL Commerce Optimizer] feed indexers.

>[!IMPORTANT]
>
>Data sync processing starts in background as soon as you complete configuration. Depending on the size of your catalog, the data sync process can take from a few minutes to several hours.

### Get required connection details

From the [Adobe Developer Console](https://developer.adobe.com/console), create a new project enabled for the [!DNL Commerce Optimizer] Ingestion service and generate OAuth Server-to-Server credentials. For detailed instructions, see [Obtain IMS Credentials](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) in the *Merchandising Developer Guide*.

Save the following values from the credentials page:

* **Organization ID** (`org_id`)
* **Client ID** (`client_id`)
* **Client Secret** (`client_secret`)

![Obtain credential details from the Adobe Developer Console project page](./assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### Get [!DNL Commerce Optimizer] instance details

Get the _tenant ID_ from the _[!DNL Instance Id]_ field on the [!DNL Commerce Optimizer] instance [[!DNL Instance details] page](../optimizer/get-started.md#manage-instances), or from the URL used to access the instance. For example, in `https://experience.adobe.com/#/@&lt;your organization&gt;/in:&lt;tenant ID&gt;/commerce-optimizer-studio/home`.

1. From the Commerce Admin, select **[!UICONTROL Adobe Commerce Optimizer]** to display the configuration page with instructions.

   ![[!DNL Commerce Optimizer] configuration page](./assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. From the command line, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) to connect to the [!DNL Adobe Commerce] staging environment.

1. Run the following [!DNL Adobe Commerce] CLI command to configure the integration, replacing the placeholder values with the values for your [!DNL Commerce Optimizer] project:

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Verify the connection by returning to the Commerce Admin and selecting the [!UICONTROL Adobe Commerce Optimizer] option.

   When you select the option, it opens the [!DNL Commerce Optimizer] UI in a new tab.

## Verify that the data sync is working {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Next steps

1. **Configure [!DNL Commerce Optimizer] catalog views and policies**

   Create catalog views and policies in the [!DNL Commerce Optimizer] UI. Note that price books are created automatically from [!DNL Adobe Commerce] customer groups. For instructions, see the [Catalog views](../optimizer/setup/catalog-view.md) and [Policies](../optimizer/setup/policies.md) documentation in the *[!DNL Commerce Optimizer] User Guide*.

1. **Set up a Commerce Storefront on [!DNL Edge Delivery Services]**

   Follow the [Storefront setup documentation](https://experienceleague.adobe.com/developer/commerce/storefront/setup/){target="_blank"} to connect your storefront to the [!DNL Commerce Optimizer] instance and start delivering personalized commerce experiences.
