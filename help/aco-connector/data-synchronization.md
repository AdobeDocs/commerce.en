---
title: Data Synchronization
description: Learn about Adobe Commerce Optimizer Connector data synchronization, including full and delta sync, cron schedules, scope control, and feed error handling.
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Data synchronization

Built on [SaaS Data Export](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview), the **Adobe Commerce Optimizer Connector** maps feed items to the [!DNL Catalog Data Ingestion API] format and handles authentication, batched submission, and scope-based sync control. The sections below describe how that synchronization works.

## How the sync works

The following diagram shows data synchronization from Adobe Commerce to Adobe Commerce Optimizer through the Adobe I/O Gateway.

![Adobe Commerce Optimizer Connector high-level sync diagram](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

When catalog data changes in Commerce, synchronization moves through these stages.

1. **SaaS Data Export** indexers detect entity updates and assemble feed items for the `products`, `productAttributes`, `categories`, and `prices` feeds.
1. Feed items are written to feed tables in Adobe Commerce, each with a sync status.
1. The connector maps items to the [!DNL Catalog Data Ingestion API] format and generates the `priceBooks` feed from website and customer group configuration.
1. The `FeedSubmitter` process batches pending items and submits them through the Adobe I/O Gateway using `POST /v1/catalog/<feed name>`.
1. Per-item results are saved back to the feed tables.
   - Validation failures and other permanent errors appear in the Admin.
   - Transient failures are queued for retry.

### Scheduled cron jobs

Two cron groups automate the pipeline on a fixed schedule.

| Cron group | Purpose | Schedule |
| ---------- | ------- | -------- |
| `index` | **Delta sync** (partial sync) — reindex invalid feed indexers | Every 1 minute |
| `resync_failed_feeds_data_exporter` | **Retry** — resubmit transient failures | Every 5 minutes |

**Requirements:** [Commerce cron must be running](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"} and feed indexers must use **Update by Schedule** mode. See [Verify Commerce application configuration](../data-export/data-synchronization.md#verify-commerce-application-configuration){target="_blank"}.

#### Delta sync {#delta-sync}

When catalog entities change, the corresponding feed indexers are marked **invalid** (pending changes not yet exported). The `indexer_reindex_all_invalid` job reindexes those indexers, assembles feed items, and triggers submission through the pipeline above.

#### Retry failed items

The `resync_failed_feeds_data_exporter` group includes one retry job per connector feed. Each job resubmits items that failed because of transient errors (for example, network timeouts or 5xx responses).

| Feed | Retry cron job | Schedule |
| ---- | -------------- | -------- |
| `products` | `products_feed_resend_failed_items` | Every 5 minutes |
| `categories` | `categories_feed_resend_failed_items` | Every 5 minutes |
| `productAttributes` | `productAttributes_feed_resend_failed_items` | Every 5 minutes |
| `prices` | `prices_feed_resend_failed_items` | Every 5 minutes |
| `priceBooks` | `priceBooks_feed_resend_failed_items` | Every 5 minutes |

#### Timing and monitoring

| Scenario | Typical timing |
| -------- | -------------- |
| Routine catalog updates | 1–2 delta-sync cycles (~1–2 minutes for indexing, plus submission) |
| Transient failures | Retried every 5 minutes |
| Full sync or large catalogs | Minutes to hours |

Monitor per-feed status from the [Data Feed Sync Status](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) page in the Commerce Admin. See [Verify that the data sync is working](./get-started.md#verify-that-the-data-sync-is-working).

## Full sync and delta sync

The connector follows the [SaaS Data Export synchronization model](../data-export/data-synchronization.md#synchronization-types). Day-to-day catalog updates use **delta sync**. **Full sync** re-exports all items for one or more feeds.

| Sync type | Typical triggers | What is sent |
| --------- | ---------------- | ------------ |
| **Full sync** | Initial connector setup, [scope export configuration](./get-started.md#customize-the-commerce-scopes-export-configuration) changes, re-enabling a sync-disabled store view | All items in the affected feeds (minutes to hours, depending on catalog size) |
| **Delta sync** | Ongoing product, price, category, and attribute changes in Commerce | Only entities with pending changes |

After initial setup, the `indexer_reindex_all_invalid` cron job drives delta sync on the schedule in [Delta sync](#delta-sync).

For targeted recovery, you can manually resync individual connector feeds with the `saas:resync` CLI command. Adobe does not recommend manual resync for routine operations. See [Sync feeds using the Commerce CLI](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"} and [Supported feeds](reference/connector-reference.md#supported-feeds).

### Initialization

When you run the `aco:config:init` CLI command during initial setup, it performs the following steps:

1. Obtains an IMS access token using the provided credentials.
1. Calls the Commerce Cloud Manager (CCM) service at `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` to validate the tenant and extract the ingestion URL and Commerce Optimizer Studio URL.
1. Saves all configuration (client secret encrypted) to `core_config_data`.
1. Schedules the initial full sync by invalidating all Adobe Commerce Optimizer feed indexers.

Add the `--no-feed-cleanup` option to skip truncating existing feed data before the initial sync.

For the step-by-step setup procedure, see [Enable the integration](./get-started.md#enable-the-adobe-commerce-optimizer-integration).

## Scope-based sync control

The `CommerceOptimizerScopeMapper` module reads per-website and per-store-view export settings and enforces them during feed collection and submission.

- **Enabled scopes** export data on the normal delta schedule.
- **Disabled scopes** are excluded from the pipeline.

Changing scope export settings triggers a full re-export for the affected scopes. See [Full sync and delta sync](#full-sync-and-delta-sync). If sync issues affect only one catalog source or price book, see [Data not syncing](troubleshooting.md#data-not-syncing).

## Feed submission and error handling

The `FeedSubmitter` process handles [!DNL Catalog Data Ingestion API] calls.

1. Separates update items from delete items (different API endpoints).
1. Calls update and delete endpoints independently.
1. Merges per-item status results back into a single response.

### HTTP status code merging

When update and delete calls return different status codes, `FeedSubmitter` combines the results as follows.

| Updates result | Deletes result | Final result |
| --------------- | --------------- | ------------- |
| 200 | 200 or none | 200 success |
| 200 | 400 | 200 with delete errors |
| 400 | 400 | 400 merged errors |
| other | other | RETRYABLE |

| Error type | Behavior |
| ---------- | -------- |
| **400** | Items listed in the response `errors` field appear in the Admin and require attention. Other items in the batch are retried. |
| **5xx** | Retried by the feed-specific `*_feed_resend_failed_items` cron jobs in the `resync_failed_feeds_data_exporter` group. |

>[!MORELIKETHIS]
>
> - [Adobe Commerce Optimizer Connector overview](overview.md) — Learn business context and scope mapping
> - [Adobe Commerce Optimizer Connector reference](reference/connector-reference.md) — Review modules, API endpoints, and configuration keys
> - [Customize the Commerce scopes export configuration](./get-started.md#customize-the-commerce-scopes-export-configuration) — Configure feeds per scope level, enable and disable behavior, and Admin steps
> - [Troubleshooting](troubleshooting.md) — Diagnose sync failures
