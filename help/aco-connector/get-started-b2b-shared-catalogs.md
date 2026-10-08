---
title: Set up the connector for B2B Commerce
description: Learn how to install the B2B connector, select Commerce scopes, synchronize shared catalog data, verify catalog views, and monitor projection health.
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
last-update: 2026-10-01T00:00:00.000Z
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

# Set up the connector for B2B Commerce

Merchants using [!DNL Adobe Commerce] B2B shared catalogs can use the [!DNL Adobe Commerce Optimizer Connector for B2B] to synchronize custom shared catalog data and configuration to [!DNL Adobe Commerce Optimizer].

{{aco-integration-environment-alignment}}

## Requirements to use the integration {#requirements-to-use-the-integration}

* Adobe Commerce 2.4.8+ with [Commerce B2B version 1.5.3+](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/install) installed and enabled.

* [!DNL Commerce Optimizer] license with provisioned sandbox instance.

* [Authentication keys](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) to download the connector meta package using Composer.

* Admin access to an [[!DNL Commerce Optimizer] sandbox instance](../optimizer/get-started.md).

The [!DNL Adobe Commerce] user configuring the integration must have:

* Administrator access to the Commerce Admin.

* [Command line access to the [!DNL Adobe Commerce] application server](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Developer access to the [IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) where the [!DNL Commerce Optimizer] project is provisioned.

### Application requirements

* Commerce cron and indexers operating normally.
* The required websites and store views identified for export.
* Shared catalogs, company assignments, assortment, and B2B pricing configured or ready to configure in Adobe Commerce.

>[!BEGINSHADEBOX]

## Remove conflicting extensions {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## Configuration steps {#configuration-steps}

To enable the [!DNL Adobe Commerce Optimizer Connector for B2B] and begin synchronizing custom shared catalog configuration from [!DNL Adobe Commerce] to your [!DNL Commerce Optimizer] instance, follow these steps.

1. **[Install the [!DNL Adobe Commerce Optimizer Connector for B2B] package](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)** using Composer to connect your [!DNL Adobe Commerce] instance to [!DNL Commerce Optimizer].

1. **[Customize the Commerce scopes export configuration](#data-export-and-scope-mapping)** from the Admin.

1. **[Enable the [!DNL Commerce Optimizer] integration](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verify that the data sync is working](#verify-that-the-data-sync-is-working)**.

## Install the [!DNL Adobe Commerce Optimizer Connector for B2B] package {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

The [!DNL Adobe Commerce Optimizer Connector for B2B] is delivered as a Composer meta package available to all Commerce merchants with an active license for [!DNL Commerce Optimizer].

### Installation steps

1. Add the `adobe-commerce/commerce-data-export-aco-adapter-b2b` module using Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. Deploy the changes to your [!DNL Adobe Commerce] staging environment.

   After deployment completes, the [!DNL Commerce Optimizer] option is available from the Commerce Admin menu. Select **[!UICONTROL Commerce Optimizer]** to open your [!DNL Commerce Optimizer] instance directly from the Commerce Admin.

{{install-extension-links}}

### Data export and scope mapping

Select the websites and store views to synchronize, then verify the initial feeds. For B2B, the connector uses the enabled scopes when it projects shared catalog data to [!DNL Commerce Optimizer].

* **Store view** → catalog source with localized product content
* **Website and customer group** → price book for website and customer-group pricing
* **Shared catalog** → protected private catalog view and enforced policy

The shared catalog defines the product assortment, and each enabled store view supplies the localized catalog source. The website and customer group determine the applicable price book. The connector projects each custom shared catalog for each enabled store view, so you do not need a separate scope setting for the B2B projection.

A custom shared catalog can generate multiple protected private catalog views, one for each enabled store view. The default public shared catalog is not projected as a B2B private catalog view. For the detailed object mapping and runtime authorization flow, see [B2B shared catalog projection](b2b-shared-catalog-projection.md).

>[!IMPORTANT]
>
>Changing the export settings triggers a full re-indexation, which can take significant time depending on your catalog size. Configure the Commerce scopes before enabling the integration and starting the initial data sync.

### To change scope export settings

1. In the Commerce Admin, go to **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Select the website or store view you want to configure.

1. In the **[!DNL Commerce Optimizer] exporter settings**, use the checkbox to enable or disable the data sync as needed.

   ![Update data sync configuration](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. Save your changes.

### Enable and disable behavior

| Action | Result |
| -------- | -------- |
| Disable a store view | **Disabling sync removes catalog data from your B2B storefront.** The catalog source remains in [!DNL Adobe Commerce Optimizer], but all synced data is removed on the next cron run. |
| Disable then re-enable a store view | The same catalog source is repopulated with a full data resynchronization. |

### Monitor B2B shared catalog changes

The connector watches for changes to shared catalogs and company assignments. When you remove a shared catalog in the Commerce Admin, the connector removes access to its private catalog view after a configurable grace period.

>[!NOTE]
>
>The deletion grace period defaults to seven days. You can change it by updating the catalog view sync settings configuration. See [catalog view sync status configuration](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings).

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

1. **Monitor the B2B catalog view projection**

  After the initial feed sync, use [Catalog View Sync Status](catalog-view-sync-status.md) to verify projected private catalog views, policies, price book references, and restricted access key configuration. For the projection model and runtime authorization flow, see [B2B shared catalog projection](b2b-shared-catalog-projection.md).

1. **Set up a Commerce Storefront on [!DNL Edge Delivery Services]**

   To connect your storefront to the [!DNL Commerce Optimizer] instance and start delivering personalized commerce experiences, follow the [Storefront setup documentation](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}.
