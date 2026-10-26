---
title: Get Started with the [!DNL Adobe Commerce Optimizer Connector]
description: Learn how to install the [!DNL Adobe Commerce Optimizer Connector], configure scope export settings, enable IMS authentication, and verify catalog synchronization.
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T16:55:50.934Z'
last-update: 2026-10-01
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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

>[!NOTE]
>
>This topic covers the [!DNL Adobe Commerce Optimizer Connector]. If you use [!DNL Adobe Commerce] B2B shared catalogs, follow the [Get started with the [!DNL Adobe Commerce Optimizer Connector for B2B]](get-started-b2b-shared-catalogs.md) instructions. The B2B connector extends the base catalog data sync to support synchronization of custom shared catalogs.

## Requirements to use the integration {#requirements-to-use-the-integration}

* [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.7+. For detailed requirements, see [System requirements](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements).

* [!DNL Commerce Optimizer] license with a provisioned sandbox instance.

* [Authentication keys](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) to download the connector metapackage using Composer.

* Admin access to an [[!DNL Commerce Optimizer] sandbox instance](../optimizer/get-started.md).

The [!DNL Adobe Commerce] user configuring the integration must have:

* Administrator access to the Commerce Admin.

* [Command line access to the [!DNL Adobe Commerce] application server](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Developer access to the [IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) where the [!DNL Commerce Optimizer] project is provisioned.

>[!BEGINSHADEBOX]

## Remove conflicting extensions

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## Configuration steps {#configuration-steps}

To enable the [!DNL Adobe Commerce Optimizer Connector] and begin synchronizing data from [!DNL Adobe Commerce] to your [!DNL Commerce Optimizer] instance, follow these steps.

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

{{install-extension-links}}

## Customize the Commerce scopes export configuration {#customize-the-commerce-scopes-export-configuration}

By default, catalog data sync is enabled for all Commerce scopes (websites, customer groups, and store views). You can customize the export settings to sync data only for specific scopes based on your business needs. For example, if multiple store views share the same language, you can export data for one store view and use it as the [catalog source](../optimizer/setup/catalog-sources.md) for multiple catalog views in [!DNL Commerce Optimizer].

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
| Disable a store view | **Disabling sync removes catalog data from your storefront.** The catalog source remains in [!DNL Commerce Optimizer], but all synced data is removed on the next cron run. |
| Disable then re-enable a store view | The same catalog source is repopulated with a full data resynchronization. |

## Enable the [!DNL Commerce Optimizer] integration {#enable-the-adobe-commerce-optimizer-integration}

You enable the integration and initiate the data sync by running the `aco:config:init` CLI command. This command completes the following steps:

1. Obtains an IMS access token using credentials supplied as command line arguments.
1. Calls the Commerce Cloud Manager (CCM) service at `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` to validate the tenant and extract the ingestion URL and [!DNL Commerce Optimizer] Studio URL.
1. Saves all configuration (client secret encrypted) to `core_config_data`.
1. Schedules the initial full sync by invalidating all [!DNL Commerce Optimizer] feed indexers.


{{aco-data-sync-processing-note}}

## Get required connection details

{{$include /help/_includes/aco-connector/connection-details.md}}

### Get [!DNL Commerce Optimizer] instance details

{{$include /help/_includes/aco-connector/configure-connection.md}}

## Verify that the data sync is working {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Next steps

1. **Configure [!DNL Commerce Optimizer] catalog views and policies**

   Create catalog views and policies in the [!DNL Commerce Optimizer] UI. Note that price books are created automatically from [!DNL Adobe Commerce] customer groups. For instructions, see the [Catalog views](../optimizer/setup/catalog-view.md) and [Policies](../optimizer/setup/policies.md) documentation in the *[!DNL Commerce Optimizer] User Guide*. To restrict access to a catalog view, see [Private catalog views](../optimizer/setup/private-catalog-view.md).

1. **Set up a Commerce Storefront on [!DNL Edge Delivery Services]**

   To connect your storefront to the [!DNL Commerce Optimizer] instance and start delivering personalized commerce experiences, follow the [Storefront setup documentation](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}.
