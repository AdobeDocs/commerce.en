---
title: View and Manage the Synchronization Process
description: Learn how to view and manage the [!DNL SaaS Data Export] synchronization process using the Data Management dashboard and Data Feed Sync Status page.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
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
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# View and manage the synchronization process

Most synchronization activities are processed automatically using full sync, partial sync, or retry failed items sync. See [Synchronization types](sync-overview.md#synchronization-types) for details on when each type runs. [!DNL SaaS Data Export] also provides tools to monitor, manage, and troubleshoot the process. You can view the synchronization status and manage the data sync process using the dashboards for your deployment.

>[!BEGINTABS]

>[!TAB Adobe Commerce]

For Adobe Commerce on cloud, on-premises, or Adobe Commerce as a Cloud Service deployments, view and manage the synchronization process from these Commerce Admin resources:

- **[Data Feed Sync Status page](../optimizer/setup/data-sync.md)**—Check the feed export status for deployments connected with [!DNL Live Search], [!DNL Product Recommendations], or [!DNL Catalog Service]. This dashboard shows the feed export status for each feed including any errors encountered. A detail view displays feed export status for individual feed items.

- **[Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**—Admin users can view and track data successfully exported and synchronized to connected Commerce Services. This dashboard shows the product data synced to Commerce Services.

>[!NOTE]
>
>The Data Management dashboard and Data Feed Sync Status page are available only if you have [!DNL Live Search], [!DNL Product Recommendations], or [!DNL Catalog Service] installed.

>[!TAB Adobe Commerce with Commerce Optimizer]

For Commerce on cloud or on-premises deployments integrated with [!DNL Commerce Optimizer], view and manage the synchronization process using the following resources:

- **[Data Feed Sync Status page](../optimizer/setup/data-sync.md)**—For Commerce projects that use [!DNL Commerce Optimizer], check catalog data availability for your storefront from the Data Feed Sync Status page in [!DNL Commerce Optimizer]. This dashboard shows the synchronization status of the data export feeds.

- **[Data Sync page](../optimizer/setup/data-sync.md)**—The Data Sync page gives an overview of synchronization status for product data coming from your upstream catalog source into [!DNL Commerce Optimizer].

For details on how to use these dashboards to verify that data sync is working and to manually resync data, see [Manage synchronization](../aco-connector/data-sync-manage.md) in the _Adobe Commerce Optimizer Connector Guide_.

>[!ENDTABS]

## Verify that the data sync is working {#verify-that-the-data-sync-is-working}

To verify that the data sync is working, confirm that data exported successfully from [!DNL Adobe Commerce] and that the data was successfully delivered to the connected Commerce service. Use the dashboards for your deployment to check both steps.

Start with export, then confirm delivery.

1. Check the sync status in the Commerce Admin.

   Go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Data Feed Sync Status page with feed item status reporting](./assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   When the sync is running, the feed data shows successfully sent records. Select a feed to view details or troubleshoot sync issues.

1. Confirm the data was delivered to connected Commerce Services.

   From the Commerce Admin, go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Data Management dashboard showing synced catalog data in connected Commerce Services](./assets/data-management-dashboard.png){width="700" zoomable="yes"}

   Verify that the expected products, prices, and attributes appear.

>[!TIP]
>
>If you have any issues with the data sync, see [Review logs and troubleshoot](troubleshooting/logging.md).

## Manually resync data

When partial sync and automatic retry do not resolve synchronization issues, you can manually resync data from the Commerce Admin or by using Commerce CLI commands. Available options depend on your deployment.

### Available manual resync options {#manual-resync-options-commerce}

Use the following options to manually resync feed data.

| Task | Option | Notes |
| --- | --- | --- |
| Resync selected failed or problematic feed items | **[!UICONTROL Data Feed Sync Status] page** | Monitor and resync selected feed items from the Commerce Admin. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working). |
| Full resync of all feeds | **[!UICONTROL Data Management Dashboard]** | Perform a full resync of all feeds from the Commerce Admin; Adobe recommends this primarily when you first connect to a Commerce service. Items whose content hash has not changed since the last export are skipped. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working). |
| Targeted feed resync with operational control | **Commerce CLI** | Use the `saas:resync` command for targeted feed resyncs. See [Sync feeds using the Commerce CLI](data-export-cli-commands.md). |

>[!MORELIKETHIS]
>
> - [How synchronization works](sync-overview.md) — Learn about synchronization modes, full sync, partial sync, and retry failed items.
> - [Sync feeds using the Commerce CLI](data-export-cli-commands.md) — Use the `saas:resync` command for targeted feed resyncs.
> - [Review logs and troubleshoot](troubleshooting/logging.md) — Diagnose data export and SaaS export errors.
> - [Manage synchronization to [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md) — Verify catalog data sync and manually resync connector feeds.


