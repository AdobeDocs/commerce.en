---
title: ACO Connector Technical Architecture
description: Learn about the ACO Connector modules, sync mechanisms, supported feeds, configuration paths, scope control, and error handling for system integrators.
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# ACO Connector technical architecture

The **ACO Connector** is built on top of the [SaaS Data Export](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview) extension. It maps data collected by SaaS Data Export extension to the ACO Catalog Data Ingestion API format and handles authentication, batched submission, and scope-based sync control.

For a high-level business overview and key benefits, see the [ACO Connector Overview](../overview.md).

## Sync architecture

The following diagram shows the data sync flow within the Adobe Commerce instance and out to Adobe Commerce Optimizer through the Adobe I/O Gateway:

![ACO Connector high-level sync diagram](../assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

Two cron jobs drive the sync:

| Cron job | Schedule | Responsibility |
|----------|----------|---------------|
| `indexer_reindex_all_invalid` | Every 1 minute | Listens for entity updates, assembles feed items, persists feed status |
| `*_resend_failed_items` | Every 5 minutes | Checks for failed feed items and resubmits them to ACO |

The **SaaS Data Export** extension handles feed collection and status tracking. The **ACO Connector** layer maps entities to the ACO API format and submits them via `POST /v1/catalog/<feed name>`.

## Module architecture

The connector is composed of seven Magento modules:

| Module | Package | Role |
|--------|---------|------|
| `DataExporterAdapter` | `adobe-commerce/module-data-exporter-adapter` | Maps Commerce feeds to ACO API format; overrides feed pool and schema config |
| `SaasExportAdapter` | `adobe-commerce/module-saas-export-adapter` | Routes ACO feeds to the ingestion API; blocks unsupported feeds from submission |
| `CommerceAcoExporter` | `adobe-commerce/module-commerce-aco-exporter` | Manages ACO credentials; provides CLI setup commands |
| `CommerceAdapter` | `adobe-commerce/module-commerce-adapter` | ACO API compatibility layer (GraphQL, bundle add-to-cart, config UI) |
| `PriceBookDataExporter` | `adobe-commerce/module-price-book-data-exporter` | Price book feed indexed by website and customer group |
| `SaasPriceBook` | `adobe-commerce/module-saas-price-book` | SaaS infrastructure for price book submission |
| `CommerceOptimizerScopeMapper` | `adobe-commerce/module-commerce-optimizer-scope-mapper` | Per-website and per-store-view sync enablement |

## Supported feeds

The connector submits only ACO-specific feeds to the ingestion API:

| Feed | ACO API Endpoint | Batch Limit | AC Index Name | Feed Table |
|------|-----------------|-------------|---------------|------------|
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

The `products`, `productAttributes`, `categories`, and `prices` feeds use data collected by SaaS Data Export indexers. The `priceBooks` feed is generated entirely by the connector from website and customer group configuration - it has no corresponding SaaS Data Export feed.

For field-level mapping details for each feed, see [Field Mappings](field-mappings.md).

## Configuration paths

The `aco:config:init` CLI command stores all connector configuration in `core_config_data`. Use `aco:config:show` to review current values (the client secret is not shown).

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```

When `aco:config:init` runs, it:

1. Obtains an IMS access token using the provided credentials
2. Calls the CCM service at `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` to validate the tenant and extract the ingestion URL and Commerce Optimizer Studio URL
3. Saves all configuration (client secret encrypted) to `core_config_data`
4. Schedules an initial full sync by invalidating all ACO feed indexers

Use `--no-feed-cleanup` to skip truncating existing feed data before the initial sync.

For setup instructions, see [Enable the integration](../get-started.md#enable-the-adobe-commerce-optimizer-integration).

## Scope-based sync control

The `CommerceOptimizerScopeMapper` module allows selective sync per website and store view. Configure via **Stores > Configuration > ACO Sync** at the website or store view level.

| Scope | Data controlled |
|-------|----------------|
| Website | Price and price book export for that website |
| Store view | Product and attribute export for that store view |

When a scope is disabled, the configuration change invalidates the affected indexers and previously synced entities are deleted from ACO.

For the Admin UI procedure, see [Customize the Commerce scopes export configuration](../get-started.md#customize-the-commerce-scopes-export-configuration).

## Feed submission and error handling

`FeedSubmitter` handles the ACO ingestion API calls:

1. Separates update items from delete items (different API endpoints)
2. Calls update and delete endpoints independently
3. Merges per-item status results back into a single response

**Status merging logic:**

| Updates result | Deletes result | Final result |
|---------------|---------------|-------------|
| 200 | 200 or none | 200 success |
| 200 | 400 | 200 with delete errors |
| 400 | 400 | 400 merged errors |
| other | other | RETRYABLE |

400-level item errors are not retried. 5xx errors are retried by the standard cron retry mechanism (`*_resend_failed_items`).

For guidance on diagnosing sync failures, see [Troubleshooting](troubleshooting.md).
