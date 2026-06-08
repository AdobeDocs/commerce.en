---
title: Adobe Commerce Optimizer Connector Reference
description: Reference tables for Adobe Commerce Optimizer Connector module packages, supported feed API endpoints and batch limits, and configuration key paths stored in core_config_data.
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# Connector reference

Quick-lookup reference for Adobe Commerce Optimizer Connector modules, feed API endpoints, and configuration paths. For an explanation of how these components work together, see [Sync Architecture](../sync-architecture.md).

## Modules

The connector is composed of seven Magento modules:

| Module | Role |
| ------ | ---- |
| `DataExporterAdapter` | Maps Commerce feeds to Adobe Commerce Optimizer API format; overrides feed pool and schema config |
| `SaasExportAdapter` | Routes Adobe Commerce Optimizer feeds to the ingestion API; blocks unsupported feeds from submission |
| `CommerceAcoExporter` | Manages Adobe Commerce Optimizer credentials; provides CLI setup commands |
| `CommerceAdapter` | Adobe Commerce Optimizer API compatibility layer (GraphQL, bundle add-to-cart, config UI) |
| `PriceBookDataExporter` | Price book feed indexed by website and customer group |
| `SaasPriceBook` | SaaS infrastructure for price book submission |
| `CommerceOptimizerScopeMapper` | Per-website and per-store-view sync enablement |

## Supported feeds

The connector submits only Adobe Commerce Optimizer-specific feeds to the ingestion API:

| Feed | Adobe Commerce Optimizer API Endpoint | Batch Limit | AC Index Name | Feed Table |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

The `products`, `productAttributes`, `categories`, and `prices` feeds use data collected by SaaS Data Export indexers. The `priceBooks` feed is generated entirely by the connector from website and customer group configuration and has no corresponding SaaS Data Export feed.

For field-level mapping details for each feed, see [Field Mappings](field-mappings.md).

## Configuration paths

All connector configuration is stored in `core_config_data`. Use `bin/magento aco:config:show` to review current values (the client secret is not shown).

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
