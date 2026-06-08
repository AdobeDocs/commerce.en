---
title: ACO Connector Sync Architecture
description: Understand how the ACO Connector syncs Commerce catalog data to Adobe Commerce Optimizer, including cron scheduling, initialization behavior, scope control, and error handling.
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# Sync architecture

The **ACO Connector** is built on top of the [SaaS Data Export](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview) extension. It maps data collected by SaaS Data Export indexers to the ACO Catalog Data Ingestion API format and handles authentication, batched submission, and scope-based sync control.

For a high-level business overview, see the [ACO Connector Overview](overview.md). For module package names, feed API endpoints, and configuration key paths, see the [Connector Reference](reference/connector-reference.md).

## How the sync works

The following diagram shows the data sync flow within the Adobe Commerce instance and out to Adobe Commerce Optimizer through the Adobe I/O Gateway:

![ACO Connector high-level sync diagram](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

Two cron jobs drive the sync:

| Cron job | Schedule | Responsibility |
|----------|----------|---------------|
| `indexer_reindex_all_invalid` | Every 1 minute | Listens for entity updates, assembles feed items, persists feed status |
| `*_resend_failed_items` | Every 5 minutes | Checks for failed feed items and resubmits them to ACO |

The **SaaS Data Export** extension handles feed collection and status tracking. The **ACO Connector** layer maps entities to the ACO API format and submits them via `POST /v1/catalog/<feed name>`.

## Initialization

When you run `aco:config:init`, it performs the following steps:

1. Obtains an IMS access token using the provided credentials
2. Calls the CCM service at `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` to validate the tenant and extract the ingestion URL and Commerce Optimizer Studio URL
3. Saves all configuration (client secret encrypted) to `core_config_data`
4. Schedules an initial full sync by invalidating all ACO feed indexers

Use `--no-feed-cleanup` to skip truncating existing feed data before the initial sync.

For the step-by-step setup procedure, see [Enable the integration](./get-started.md#enable-the-adobe-commerce-optimizer-integration).

## Feed submission and error handling

`FeedSubmitter` handles the ACO ingestion API calls:

1. Separates update items from delete items (different API endpoints)
2. Calls update and delete endpoints independently
3. Merges per-item status results back into a single response

**HTTP status code merging logic:**

| Updates result | Deletes result | Final result |
|---------------|---------------|-------------|
| 200 | 200 or none | 200 success |
| 200 | 400 | 200 with delete errors |
| 400 | 400 | 400 merged errors |
| other | other | RETRYABLE |

If request returned 400 status code, all items in request were not accepted by ACO. Items specified in response `errors` field will require customer attention, oter items - will be retried with `*_resend_failed_items` cron job.

5xx status code errors are retried by the `*_resend_failed_items` cron job.

For guidance on diagnosing sync failures, see [Troubleshooting](troubleshooting.md).
