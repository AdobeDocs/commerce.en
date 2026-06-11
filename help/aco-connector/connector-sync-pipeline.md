---
title: Catalog Sync Pipeline
description: "Learn how the [!DNL Adobe Commerce Optimizer Connector] sync pipeline works, including feed transformation, cron schedules, scope control, and error handling."
feature: Integration, Configuration
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
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
    internal-label: Data pipelines
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connector sync pipeline

Built on [[!DNL SaaS Data Export]](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview), the **[!DNL Adobe Commerce Optimizer Connector]** maps data collected by [!DNL SaaS Data Export] indexers to the format required by the [!DNL Adobe Commerce Optimizer] [!DNL Catalog Data Ingestion API] and handles authentication, batched submission, and scope-based sync control. The sections below describe how that synchronization works.

Related context:

- Learn about the integration's business value, key features, and architecture in the [[!DNL Commerce Optimizer Connector] overview](overview.md) topic.

- For module package names, feed API endpoints, and configuration key paths, see the [Connector reference](reference/connector-reference.md)

## How the sync works

The following diagram shows data synchronization from [!DNL Adobe Commerce] to [!DNL Commerce Optimizer] through the [!DNL Adobe I/O Gateway].

![Commerce Optimizer Connector high-level sync diagram](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

When catalog data changes in [!DNL Adobe Commerce], synchronization moves through these stages.

1. **Entity Change Detection** — (every 1 min) A cron job (`indexer_reindex_all_invalid`) detects [!DNL Adobe Commerce] entity changes and triggers the [!DNL SaaS Data Export], which assembles feed items and tracks their status.
1. **Transformation** — The [!DNL Commerce Optimizer Connector] picks up the assembled feeds, maps [!DNL Adobe Commerce] entities and scopes to formats required by the [!DNL Commerce Optimizer] API, and prepares the payload for transmission.
1. **Transmission** — The transformed data is sent via HTTP POST (`/v1/catalog/<feed name>`) through the [!DNL Adobe I/O Gateway] to [!DNL Commerce Optimizer], which validates and persists the incoming feeds.
1. **Failure Retry** (every 5 min) — A separate cron job (`*_resend_failed_items`) detects any failed feed items and re-submits them through the same pipeline.

### Scheduled cron jobs

Two cron groups automate the pipeline on a fixed schedule.

| Cron group | Purpose | Schedule |
| ---------- | ------- | -------- |
| `indexer_reindex_all_invalid`  | Listens for entity updates, assembles feed items, persists feed status | Every 1 minute |
| `*_resend_failed_items`| Checks for failed feed items and resubmits them to [!DNL Commerce Optimizer] | Every 5 minutes |

The **[!DNL SaaS Data Export]** extension handles feed collection and status tracking. The connector layer maps entities and scopes to the format required by the [!DNL Commerce Optimizer] API and submits them via `POST /v1/catalog/<feed name>`.

#### Requirements

- [Commerce cron must be running](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}.
- Feed indexers must use **[!UICONTROL Update by Schedule]** mode. See [Verify Commerce application configuration](../data-export/data-synchronization.md#verify-commerce-application-configuration){target="_blank"}.

## Scope-based sync control

The `CommerceOptimizerScopeMapper` module reads per-website and per-store-view export settings and enforces them during feed collection and submission.

- **Enabled scopes** export data on the normal delta schedule.
- **Disabled scopes** are excluded from the pipeline.
  Previously synced entities are removed from [!DNL Commerce Optimizer] on the next cron run.

If sync issues affect only one catalog source or price book, see [Data not syncing](troubleshooting.md#data-not-syncing).

For details on customizing the synchronization scope, see [Customize the Commerce scopes export configuration](get-started.md#customize-the-commerce-scopes-export-configuration).

## Timing and monitoring

| Scenario | Typical timing |
| -------- | -------------- |
| Routine catalog updates | 1–2 delta-sync cycles (~1–2 minutes for indexing, plus submission) |
| Transient failures | Retried every 5 minutes |
| Full sync or large catalogs | Minutes to hours |

Monitor per-feed status from the [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) page in the Commerce Admin. See [Verify that the data sync is working](./get-started.md#verify-that-the-data-sync-is-working).

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
> - [Connector overview](overview.md) — Learn business context and scope mapping
> - [Connector reference](reference/connector-reference.md) — Review modules, API endpoints, and configuration keys
> - [Customize the Commerce scopes export configuration](./get-started.md#customize-the-commerce-scopes-export-configuration) — Configure feeds per scope level, enable and disable behavior, and Admin steps
> - [Troubleshooting](troubleshooting.md) — Diagnose sync failures
