---
title: Catalog Sync
description: Learn how to export product data from the [!DNL Commerce] server to [!DNL Commerce Services].
feature: Catalog Management, Data Import/Export, Catalog Service
exl-id: 99f96b93-b036-490c-8c57-40463a0de365
TQID: https://experienceleague.adobe.com/-X5W4TJNW6pduPsWH-SLuAXrfP7iReCpaVg5qeu2odA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Catalog Sync

>[!NOTE]
>
> The Catalog Sync Dashboard is now the Data Management Dashboard. This revamped dashboard now supports [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+, [[!DNL Live Search]](../live-search/overview.md) v4.1.0+, and [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+. Customers can get the Data Management Dashboard by updating to the latest version of one of those services. Read more about it in the [Data Management Dashboard](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) documentation. This current topic remains for those users who have yet to upgrade and still have the Catalog Sync dashboard.

Adobe Commerce uses indexers to compile catalog data into tables. The process is automatically triggered by [events](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing) such as a change to a product price or inventory level.

The Catalog Sync service moves product data from an [!DNL Adobe Commerce] instance to the [!DNL Commerce Services] platform on an ongoing basis to keep the data up to date. For example, [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) requires current catalog information to accurately return recommendations with correct names, pricing, and availability. Use the _Catalog Sync_ dashboard to observe and manage the synchronization process or the command-line interface to trigger a catalog sync and to reindex product data for consumption by [!DNL Commerce Services]. See [Command-line Interface Reference](../data-export/data-export-cli-commands.md) in the _SaaS Data Export_ Guide.

## Access the Catalog Sync dashboard

To access the Catalog Sync dashboard, select **System** > _Data Transfer_ > **Catalog Sync**.

With the **Catalog Sync** dashboard you can:

- View the sync status (**In Progress**, **Success**, **Failed**)
- View the total number of products synced
- Search synced products to view their current state
- Search store catalog by name, SKU, etc.
- View synced product details in JSON to help diagnose a sync discrepancy
- Reinitiate the sync process

### Last sync

Reports a sync status of:

- **Success** - Displays the date and time that the sync was successful and the number of products updated
- **Failed** - Displays the date and time that the sync was attempted
- **In Progress** - Displays the date and time of the last successful sync

The catalog sync process automatically runs every hour. If you do not see expected products on the storefront, or if the products do not reflect recent changes you made, you can resolve [catalog sync issues](#resolvesync).

### Products synced

Displays the total number of products synced from your [!DNL Commerce] catalog. After the initial sync, only changed products should be synced.

## Resync {#resync}

If you must initiate a resync of your catalog before the hourly scheduled sync occurs, you can force a resync.

>[!NOTE]
>
> Forcing a resync triggers a resync of your entire product catalog, which can increase load on hardware resources.

1. From the _Catalog Sync_ dashboard, select **Settings**.

   The _Catalog Sync Settings_ page appears.

1. In the _Resync Data_ section, click [!UICONTROL Resync].

   [!DNL Commerce] syncs your catalog during the next scheduled sync window. Depending on the size of your catalog, this operation can take a long time.

## Synced catalog products

The **Synced catalog products** table displays the following information.

|Field|Description|
|---|---|
|ID | Unique identifier of the product|
|Name | Storefront name of the product|
|Type | Identifies the product type, such as simple, configurable, or downloadable|
|Last Exported | Date the product was last successfully exported from your catalog|
|Last Modified | Date the product was last modified in your catalog|
|SKU | Displays the stock-keeping unit for the product|
|Price | Price of the product|
|Visibility | A product's visibility setting as defined in the [!DNL Commerce] catalog|

## Resolve catalog sync issues {#resolvesync}

See [Troubleshooting](../data-export/troubleshooting/logging.md#troubleshooting) in the _SaaS Data Export Guide_.
