---
title: Synchronize Data with SaaS Data Export
description: Learn how the [!DNL SaaS Data Export] collects and synchronizes data between Adobe Commerce instances and connected Commerce services.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
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
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Synchronize data with SaaS Data Export

When you install an [!DNL Adobe Commerce] service that requires data export such as Catalog Service, Live Search, or Product Recommendations, a collection of SaaS data export modules is installed to manage the data collection and synchronization process.

SaaS data export moves product data from an Adobe Commerce instance to the Commerce Services platform on an ongoing basis to keep the data up to date. For example, Product Recommendations requires current catalog information to accurately return recommendations with correct names, pricing, and availability. For details on monitoring the synchronization process, see [View and manage the synchronization process](data-sync-manage.md).

The following diagram shows the SaaS data export flow.

![SaaS data export collection and synchronization flow for Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

When catalog data changes in [!DNL Adobe Commerce], synchronization moves through these stages.

1. **Entity change detection** - Magento's Mview system detects row changes in subscribed database tables (for example, `catalog_product_entity`) and writes entries to a changelog table.
1. **Feed indexing** - The feed indexer reads the changelog, loads entity data from the source tables, and assembles feed items.
1. **Data collection and transformation** - Providers registered in the feed schema [`et_schema.xml`](extensibility-and-customizations.md#feed-schema-overview) collect field data.
1. **Hash deduplication** - A content hash is computed for each feed item. Items whose hash has not changed since the last export are skipped, so only modified data is transmitted.
1. **HTTP submission** - Feed items are sent as authenticated HTTP POST batches to the Adobe SaaS Feed Ingestion Service.
1. **Status persist** - The API response status is written back to the [feed table](reference/feed-table-reference.md) for each item.
1. **Failure retry** - Items that failed to export are automatically retried by a scheduled cron job.

>[!NOTE]
>
>For [!DNL Adobe Commerce Optimizer Connector] deployments, [!DNL SaaS Data Export] handles entity change detection and feed assembly. The connector then maps feeds to the [!DNL Catalog Data Ingestion API] format and submits them to [!DNL Adobe Commerce Optimizer]. See [Connector sync pipeline](../aco-connector/connector-sync-pipeline.md) for scope control, submission, and error handling.

>[!NOTE]
>
>To ensure smooth scheduling and avoid disruptions in site operations, Adobe recommends estimating data volume and sync time before starting any data feed synchronization. This estimation is important when planning for initial syncs or large scale catalog updates, such as mass price changes. For details, see [Estimate data volume and transmission time for data sync](estimate-data-volume-sync-time.md)

## Synchronization modes

SaaS data export has two modes to process entity feeds:

- **Immediate export mode**—In this mode, data is collected and sent immediately to the Commerce Service in a single iteration. This mode speeds up delivery of entity updates to the Commerce Service and reduces the storage size of the feed tables.

- **Legacy export mode**—In this mode, data is collected in a single process. Then, a cron job sends the collected data to the connected commerce services. In data export log entries, feeds that use the legacy mode are labeled `(legacy)`.

## Synchronization types

SaaS data export supports three synchronization types–full sync, partial sync, and retry failed items sync.

### Full sync

After connecting an Adobe Commerce instance to Commerce Service, perform a full sync to send entity feed data from Adobe Commerce to the connected service.

>[!NOTE]
>
>Full sync is mainly for the onboarding phase. Avoid regular use to prevent database overload. After the initial synchronization, ongoing changes are synched automatically using partial sync.

### Partial sync {#partial-sync}

With partial sync, SaaS data export automatically sends updates from the Commerce application, such as product name changes or price updates, to connected commerce services.
For partial sync to work, the Commerce application requires the following configuration:

- [Task scheduling is enabled via cron jobs](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)
- All SaaS data export indexers are configured in `Update by Schedule` mode.



### Retry failed items sync {#retry-failed-items-sync}

The Retry failed items sync uses a separate process to resend items that failed to sync due to errors during the synchronization process, for example an application error, network disruption, or SaaS service error. The `*_resend_failed_items` cron jobs in the `resync_failed_feeds_data_exporter` group handle this automatically every 5 minutes.

## Scheduled cron jobs

The following cron groups automate the pipeline on a fixed schedule.

| Cron group | Cron job | Purpose | Schedule |
|---|---|---|---|
| `index` | `indexer_update_all_views` | Processes Mview changelogs and triggers partial feed updates | Every 1 minute |
| `index` | `indexer_reindex_all_invalid` | Performs a full resync for feed indexes marked as "Reindex required" | Every 1 minute |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | Detects failed feed items and resubmits them | Every 5 minutes |
| `commerce_data_export` | `saas_data_exporter` | Submits data for legacy-mode feeds (orders, scopes) | Every 5 minutes |
| `commerce_data_export`              | `cleanup_deleted_feed_items`  | Cleans up synced deleted feed items past the retention period (7 days) | Every day at 2:00 AM|

## Feed submission and HTTP error handling {#feed-submission-and-http-error-handling}

Feed items are submitted as authenticated gzip-compressed JSON batches over HTTP POST. The following table shows how HTTP response codes map to export status and retry behavior.

| Status code | Retry? | Meaning                                                                                                             |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------|
| 200         | No     | Accepted successfully                                                                                               |
| 400         | No     | Bad data or validation failure - requires manual investigation. Check `var/log/saas-export-errors.log` for details. |
| 429         | Yes    | Rate limit hit - reduce `thread_count` in [export processing settings](customize-export-processing.md)              |
| 5xx         | Yes    | SaaS-side error - automatic retry                                                                                   |
| 2           | Yes    | Item is scheduled for retry                                                                                         |

In addition to HTTP-level failures, application-level errors such as local processing failures or network disruptions are also scheduled for automatic retry by the `*_resend_failed_items` cron jobs.

Monitor per-feed status from the [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) page in the Commerce Admin.

>[!MORELIKETHIS]
>
> - [Manage synchronization](data-sync-manage.md) — Verify sync status and manually resync feeds.
> - [Feed table schema](reference/feed-table-reference.md) — Inspect item-level status and error details.
> - [Improve data export performance](customize-export-processing.md) — Tune batch size and thread count.
