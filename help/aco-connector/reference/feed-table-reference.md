---
title: Feed Table Schema Reference
description: Learn about the feed table schema used by the [!DNL Adobe Commerce Optimizer Connector] to track feed item state, export status, and error details.
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---

# Feed table schema reference

Every feed has a dedicated MySQL table in the [!DNL Adobe Commerce] database. All feed tables share the same column structure.

## Supported feeds

For the full list of supported feeds with API endpoints, batch limits, indexer names, and feed table names, see [Connector modules and feed endpoints](connector-reference.md#supported-feeds).

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
| `status` | INT | Submission status code from the last export attempt. See [Feed submission and error handling](../connector-sync-pipeline.md#feed-submission-and-error-handling). |
| `errors` | TEXT | JSON-encoded error details returned by the [!DNL Commerce Optimizer] API for this item |
| `metadata` | JSON | Internal sync flags and lock metadata info used by the export framework |

## Common diagnostic queries

Use the following SQL queries to inspect feed table state directly. The `feed_data` column stores data in [!DNL Adobe Commerce Optimizer] API format. Replace placeholder values such as `<SKU>`, `<ATTRIBUTE_CODE>`, `<SLUG>`, and `<PRICE_BOOK_ID>` with actual values from your environment.

**Products feed - by SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Product attributes feed - by attribute code:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**Categories feed - by URL path:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**Prices feed - by SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Price books feed - by price book ID:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [Connector modules and feed endpoints](connector-reference.md)
>- [Connector sync pipeline](../connector-sync-pipeline.md)
>- [Manage synchronization](../data-sync-manage.md)
>- [Field mapping for connector feeds](field-mapping.md)
