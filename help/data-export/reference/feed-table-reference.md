---
title: Feed Table Schema Reference
description: Learn about the feed table schema used by [!DNL SaaS Data Export] to track feed item state, export status, and error details.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
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
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---

# Feed table schema reference

Every feed has a dedicated MySQL table in the [!DNL Adobe Commerce] database. All feed tables share the same column structure. The table below lists each feed with its CLI feed name, indexer ID, and feed table name.

## Supported feeds

Actual list of feeds depends on the installed [!DNL SaaS Data Export] package.


| Feed (`--feed`) | Purpose | Indexer ID | Feed Table | Export Mode |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | Product catalog (attributes, categories, images, etc.) | `catalog_data_exporter_products` | `cde_products_feed` | Immediate |
| `productAttributes` | Attribute definitions and metadata. Used to define search schema. | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | Immediate |
| `categories` | Categories data | `catalog_data_exporter_categories` | `cde_categories_feed` | Immediate |
| `prices` | Product prices with customer group prices and tier prices | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | Immediate |
| `variants` | Configurable product variants | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | Immediate |
| `scopesWebsite` | Website with store view codes | `scopes_website_data_exporter` | `scopes_website_data_exporter` | Legacy |
| `scopesCustomerGroup` | Customer group definitions | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | Legacy |
| `productOverrides` | Calculated product permissions | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | Immediate |
| `categoryPermissions` *(EE)* | Raw category permissions data | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | Immediate |
| `orders` | Sales orders status | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | Legacy |

The **Export Mode** column indicates how each feed collects and submits data:

- **Immediate-mode feeds** — Collect data, skip unchanged items using content hashes (hash deduplication), and submit updates in the same indexer run.
- **Legacy-mode feeds** (`scopesWebsite`, `scopesCustomerGroup`, `orders`) — Store assembled data in the feed table first and submit it via a separate cron job.

See [Synchronization modes](../sync-overview.md#synchronization-modes).

## Schema

| Column | Type | Description |
| --- | --- | ---------------- |
| `id` | INT (PK) | Auto-increment primary key |
| `source_entity_id` | INT | Entity ID from the Commerce source table (for example, `catalog_product_entity.entity_id`) |
| `feed_id` | VARCHAR | Unique identifier for a feed item. Computed as a hash of the item's identity fields (for example, `sku + storeViewCode`), not an auto-increment value. |
| `feed_data` | JSON | Feed payload for this item. Only minimal information as entity identifier and scope is populated. When `PERSIST_EXPORTED_FEED=1` is set, full payload is stored. |
| `feed_hash` | VARCHAR | Content hash used for change detection. Computed from the payload, excluding timestamps (`modifiedAt`, `updatedAt`). If the hash matches the previous export, the item is not re-submitted. |
| `is_deleted` | TINYINT | Soft-delete marker. Set to `1` when the entity is deleted in Commerce. |
| `modified_at` | TIMESTAMP | Last time this feed item was modified |
| `status` | INT | Submission status code from the last export attempt. See [Feed submission and HTTP error handling](../sync-overview.md#feed-submission-and-http-error-handling). |
| `errors` | TEXT | JSON-encoded error details returned by the SaaS service for this item |
| `metadata` | JSON | Internal sync flags and lock metadata info used by the export framework |

## Common diagnostic queries

Use the following SQL queries to inspect feed table state directly. Replace `cde_products_feed` with the table for the feed you are investigating. See [Supported feeds](#supported-feeds) for the full list of table names.

**Find all items that have not been successfully exported:**

```sql
SELECT source_entity_id, status, errors, modified_at
FROM cde_products_feed
WHERE status != 200
ORDER BY modified_at DESC
LIMIT 50;
```

**Check export status for a specific SKU across all scopes:**

```sql
SELECT p.sku, f.status, f.modified_at, f.is_deleted, f.feed_data, f.errors
FROM catalog_product_entity p
LEFT JOIN cde_products_feed f ON f.source_entity_id = p.entity_id
WHERE p.sku = 'ADB295';
```


>[!MORELIKETHIS]
>
>- [Synchronize data with SaaS Data Export](../sync-overview.md)
>- [View and manage synchronization](../data-sync-manage.md)
>- [Sync feeds using the Commerce CLI](../data-export-cli-commands.md)
