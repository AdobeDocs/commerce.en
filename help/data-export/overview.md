---
title: "[!DNL SaaS Data Export Guide]"
description: Learn about using the [!DNL data export] extension for Adobe Commerce SaaS services that synchronizes data between Adobe Commerce and connected Commerce services.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# [!DNL SaaS Data Export] Guide

[!DNL SaaS data export] synchronizes data between an Adobe Commerce instance and connected Commerce Services. When you add Live Search, Product Recommendations, the Catalog Service, or the [!DNL Adobe Commerce Optimizer Connector] to an Adobe Commerce installation, the [!DNL Data export] extension is installed automatically.

>[!NOTE]
>
>If you install the [!DNL Adobe Commerce Optimizer Connector], the same [!DNL Data Export] extension collects catalog and pricing feeds from [!DNL Adobe Commerce]. The connector then maps and submits those feeds to [!DNL Adobe Commerce Optimizer] using the Composable Catalog Data Model (CCDM). See the [[!DNL Adobe Commerce Optimizer Connector] overview](../aco-connector/overview.md) for setup and architecture, and [Connector sync pipeline](../aco-connector/connector-sync-pipeline.md) for synchronization behavior after export.

SaaS data export collects and exports various types of data, referred to as _feeds_, which aggregate specific types of information. Depending on which Commerce services are installed, the SaaS data export feeds include:

- **Catalog entity feeds** aggregate product data. Data includes products, product attributes, product prices, product variations, categories, category permissions, and product permissions.
- The **Scopes feed** aggregates data for customer groups, websites, stores, and store views.
- The **Sales Order feed** aggregates orders data including their related entities such as invoices, shipments, credit memos, and so on.
- The **Multi-Source Inventory feed** aggregates data about inventory stock status items.

SaaS data export is delivered as a PHP extension. It supports several methods to initiate and manage the data synchronization process.

- **Manual synchronization from the Admin or the command line**

  - The [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard){target="_blank"} in the Commerce Admin provides a graphical view of the synchronization status that shows product data successfully synced to commerce services. You can use the dashboard to perform a full resynchronization (_full sync_) of all feeds. However, Adobe recommends only performing a full sync the first time you connect Adobe Commerce to a Commerce service. See [Synchronization process](sync-overview.md).

    {{aco-data-sync-verification}}

  - The [Data Feed Sync Status](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"} page provides real-time insights into the health and performance of data export feeds that transfer product and category data from Commerce to external services such as Product Recommendations, Live Search, and Catalog Service, or Adobe Commerce Optimizer.

  - The [Adobe Commerce command-line tool](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli){target="_blank"} (CLI) provides commands to synchronize specific feeds and includes additional options to customize feed processing.

- **Automated synchronization with cron jobs**

  - [Partial data synchronization](sync-overview.md#partial-sync)—Cron jobs trigger a partial data sync when a Commerce Admin user updates an entity. The data export process sends only these updates to connected Commerce services. The partial synchronization process is based on the MView mechanism and requires no actions from the Admin user or system integrator.

  - [Automatic retry for synchronization errors](sync-overview.md#retry-failed-items-sync)—Cron jobs trigger automatic retry of the synchronization process when errors occur during the data synchronization process.

- **Export scheduling and performance**

  - Developers and system integrators can estimate the time required for SaaS data export to synchronize data between Adobe Commerce and connected services. This estimation can help schedule data export processing to prevent site disruption. See [Estimate data volume and transmission time](estimate-data-volume-sync-time.md).

  - In cases where the sync needs to happen more quickly, SaaS data export provides customization options to improve export processing performance. See [Improve data export performance](customize-export-processing.md).

- **Track and troubleshoot data export activities**—Use data-export and saas-export logs to review sync status and feed payloads during the synchronization and indexation process. See [Logging and troubleshooting](troubleshooting/logging.md).
