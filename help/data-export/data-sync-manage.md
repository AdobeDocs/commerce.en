---
title: View and Manage the Synchronization Process
description: Learn how to view and manage the [!DNL SaaS Data Export] synchronization process using the Data Management dashboard and Data Sync Feed Sync Status page.
role: Admin, Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
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
hide: true
index: false
---
# View and manage the synchronization process

Most synchronization activities are processed automatically using full sync, partial sync, or retry failed items sync. See [Synchronization types](sync-overview.md#synchronization-types) for details on when each type runs. SaaS data export also provides tools to monitor, manage, and troubleshoot the process. You can view the synchronization status and manage the data sync process using the dashboards for your deployment.

>[!BEGINTABS]

>[!TAB Adobe Commerce]

For Adobe Commerce on cloud, on premises, or Commerce as a Cloud Services deployments, view and manage the synchronization process from these Commerce Admin resources:

- **[Data Sync Feed Sync Status page](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)**—For Commerce projects that use [!DNL Adobe Commerce Optimizer], check catalog data availability for your storefront from the Data Feed Sync Status page in [!DNL Commerce Optimizer]. This dashboard shows the synchronization status of the data export feeds.

- **[Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**—Admin users can view and track data synchronized to Commerce Services and available to storefront services. This dashboard shows the product synced to Commerce Services.

>[!NOTE]
>
>The Data Management dashboard is available only if you have [!DNL Live Search], [!DNL Product Recommendations], or [!DNL Catalog Service] installed.

>[!TAB Adobe Commerce with Commerce Optimizer]

For Commerce on cloud or on premises deployments integrated with [!DNL Commerce Optimizer], view and manage the synchronization process using the following resources:

- **[Data Sync Feed Sync Status page](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)**—For Commerce projects that use [!DNL Commerce Optimizer], check catalog data availability for your storefront from the Data Feed Sync Status page in [!DNL Commerce Optimizer]. This dashboard shows the synchronization status of the data export feeds.

- **[Data Sync page](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)**—The Data Sync page gives an overview of synchronization status for product data coming from your upstream catalog source into [!DNL Commerce Optimizer].

>[!ENDTABS]

## Verify that the data sync is working {#verify-that-the-data-sync-is-working}

Use the dashboards for your deployment to monitor export status and confirm that data was delivered.

>[!BEGINTABS]

>[!TAB Adobe Commerce]

Confirm that catalog data exported from the Commerce Admin was delivered to connected Commerce Services such as [!DNL Live Search], [!DNL Product Recommendations], or [!DNL Catalog Service].

1. **Check sync status in the Commerce Admin:**

   Go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Data Feed Sync Status page with feed item status reporting](../aco-connector/assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   When the sync is running, the feed data shows successfully sent records. Select a feed to view details or troubleshoot sync issues.

1. **Confirm data delivered to connected Commerce Services:**

   From the Commerce Admin, go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Data Management dashboard showing synced catalog data in connected Commerce Services](./assets/data-management-dashboard.png){width="500" zoomable="yes"}

   Verify that the expected products, prices, and attributes appear.

>[!TAB Adobe Commerce with Commerce Optimizer]

Confirm that catalog data exported from the Commerce Admin was delivered to [!DNL Commerce Optimizer].


{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

>[!ENDTABS]

>[!TIP]
>
>If you have any issues with the data sync, see [Review logs and troubleshoot](troubleshooting-logging.md).

## Manually resync data

When partial sync and automatic retry do not resolve synchronization issues, you can manually resync data from the Commerce Admin or by using Commerce CLI commands. Available options depend on your deployment.

>[!BEGINTABS]

>[!TAB Adobe Commerce]

### Available manual resync options

For Adobe Commerce on cloud, on premises, and Adobe Commerce as a Cloud Service deployments with Live Search or Product Recommendations enabled, use the following options to manually resync feed data.

| Task | Option | Notes |
| --- | --- | --- |
| Resync selected failed or problematic feed items | **[!UICONTROL Data Feed Sync Status] page** | Monitor and resync selected feed items from the Commerce Admin. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working). |
| Full resync of all feeds | **[!UICONTROL Data Management Dashboard]** | Perform a full resync of all feeds from the Commerce Admin; Adobe recommends this primarily when you first connect to a Commerce service. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working). |
| Targeted feed resync with operational control | **Commerce CLI** | Use the `saas:resync` command for targeted feed resyncs. See [Sync feeds using the Commerce CLI](data-export-cli-commands.md). |

>[!TAB Adobe Commerce with Commerce Optimizer]

### Available manual resync options

For Adobe Commerce deployments integrated with [!DNL Commerce Optimizer] through the connector, use the following options to manually resync catalog data.

| Task | Option | Notes |
| --- | --- | --- |
| Verify sync status and resync from the upstream system when products are missing | **Upstream-system resync** | Use the [!UICONTROL Data Sync] page in [!DNL Commerce Optimizer] to verify the data delivered to Optimizer; when products are missing, resync from the upstream system. See [Resync catalog data](../optimizer/setup/data-sync.md#resync-catalog-data) in the *[!DNL Commerce Optimizer] User Guide*. |
| Resync selected failed or problematic connector feed items | **[!UICONTROL Data Feed Sync Status] page in the Commerce Admin** | Monitor export status and resync selected connector feed items from the Commerce Admin. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working). |
| Targeted connector feed resync with operational control | **Commerce CLI** | Run `saas:resync` from the Adobe Commerce instance for connector feeds. See [Sync feeds using the Commerce CLI](data-export-cli-commands.md) and [Supported feeds](/help/aco-connector/reference/connector-reference.md#supported-feeds). |
| Force a full repopulation for a catalog source scope | **Disable and re-enable scope** | Clear and reselect the data sync checkbox for a store view in **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]** to trigger a full repopulation. See [Customize the Commerce scopes export configuration](/help/aco-connector/get-started.md#customize-the-commerce-scopes-export-configuration). |

>[!NOTE]
>
>The [!UICONTROL Data Sync] page in [!DNL Commerce Optimizer] does not provide a resync-selected-items control. For connector-backed implementations, use the Commerce Admin [!UICONTROL Data Feed Sync Status] page and/or the Commerce CLI. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working).

>[!ENDTABS]
