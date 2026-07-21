---
title: "[!DNL SaaS Data Export Guide]"
description: Learn about using the [!DNL data export] extension for Adobe Commerce SaaS services that synchronizes data between Adobe Commerce and connected Commerce services.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
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

[!DNL SaaS data export] synchronizes data between an Adobe Commerce instance and connected Commerce Services. When you add Live Search, Product Recommendations, the Catalog Service, or the [!DNL Adobe Commerce Optimizer Connector] to an Adobe Commerce installation, the [!DNL Data Export] extension is installed automatically.

>[!NOTE]
>
>If you install the [!DNL Adobe Commerce Optimizer Connector], the same [!DNL Data Export] extension collects catalog and pricing feeds from [!DNL Adobe Commerce]. The connector then maps and submits those feeds to [!DNL Adobe Commerce Optimizer] using the Composable Catalog Data Model (CCDM). See the [[!DNL Adobe Commerce Optimizer Connector] overview](../aco-connector/overview.md) for setup and architecture, and [Connector sync pipeline](../aco-connector/connector-sync-pipeline.md) for synchronization behavior after export.

SaaS data export collects and exports various types of data, referred to as _feeds_, which aggregate specific types of information. Depending on which Commerce services are installed, the SaaS data export feeds include:

- **Catalog entity feeds** aggregate product data. Data includes products, product attributes, product prices, product variations, categories, category permissions, and product permissions.
- The **Scopes feed** aggregates data for customer groups, websites, stores, and store views.
- The **Sales Order feed** aggregates orders data including their related entities such as invoices, shipments, credit memos, and so on.
- The **Multi-Source Inventory feed** aggregates data about inventory stock status items.

SaaS data export is delivered as a PHP extension that supports both automated and manual synchronization:

- **Automated synchronization**—After the initial full sync when you connect a Commerce service, cron jobs keep connected services current using partial sync and automatic retry of failed items, with no action required from the Admin user or system integrator.

- **Manual synchronization**—Run a full resync or resync selected feeds from the Commerce Admin or the [Commerce CLI](data-export-cli-commands.md).

- **Monitoring**—Track feed health, status, and delivery from the [!UICONTROL Data Feed Sync Status] page and Data Management dashboard in the Commerce Admin. See [Manage synchronization](data-sync-manage.md) for verification and resync steps.

For synchronization behavior, modes, and the export flow diagram, see [How synchronization works](sync-overview.md).

SaaS data export also provides tools to plan and troubleshoot the synchronization process:

- **Scheduling and performance**—Estimate sync time to schedule processing and avoid site disruption, and customize export processing to improve performance. See [Estimate data volume and transmission time](estimate-data-volume-sync-time.md) and [Improve data export performance](customize-export-processing.md).

- **Tracking and troubleshooting**—Review sync status and feed payloads using data-export and saas-export logs. See [Review logs and troubleshoot](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Extend and customize SaaS data export feeds](extensibility-and-customizations.md) — Add or modify feed data.
> - [Troubleshooting scenarios](troubleshooting/troubleshooting-scenarios.md) — Diagnose misconfiguration and unexpected sync results.
> - [Release notes](release-notes.md) — Extension updates and known issues.
