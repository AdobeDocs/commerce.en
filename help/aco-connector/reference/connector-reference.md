---
title: Adobe Commerce Optimizer Connector Modules and Feed Endpoints
description: Learn about Adobe Commerce Optimizer Connector modules, catalog feed API endpoints, batch limits, and core_config_data configuration paths for Adobe Commerce.
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Connector modules and feed endpoints

This reference lists the Commerce Optimizer Connector module packages, supported feed API endpoints, and configuration key paths stored in `core_config_data`. To learn how these components work together during synchronization, see [Data synchronization](../data-synchronization.md).

## Modules

The connector includes multiple Magento modules that collect catalog data, map feed data to the format supported by the Commerce Optimizer API, and manage submission and scope control. The following table summarizes each module and its role.

| Module | Role |
| ------ | ---- |
| `DataExporterAdapter` | Maps Commerce feeds to the format required by the Commerce Optimizer API. Overrides feed pool and schema config. |
| `SaasExportAdapter` | Routes Commerce Optimizer feeds to the ingestion API and blocks unsupported feeds from submission. |
| `CommerceAcoExporter` | Manages Commerce Optimizer credentials and provides CLI setup commands |
| `CommerceAdapter` | Adobe Commerce Optimizer API compatibility layer (GraphQL, bundle add-to-cart, config UI) |
| `PriceBookDataExporter` | Price book feed indexed by website and customer group |
| `SaasPriceBook` | SaaS infrastructure for price book submission |
| `CommerceOptimizerScopeMapper` | Per-website and per-store-view sync enablement |

## Supported feeds

The connector submits multiple feed types to the [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. The table below lists each feed with its endpoint, batch limit, indexer name, and feed table in Adobe Commerce.

| Feed | Commerce Optimizer API Endpoint | Batch Limit | AC Index Name | Feed Table |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

The `products`, `productAttributes`, `categories`, and `prices` feeds reuse data collected by SaaS Data Export indexers. The connector generates the `priceBooks` feed from website and customer group configuration and does not rely on a SaaS Data Export indexer.

For field-level mapping details for each feed, see [Field mapping for Adobe Commerce Optimizer Connector feeds](field-mapping.md).

## Configuration paths

Adobe Commerce Optimizer Connector credentials and service URLs are stored in `core_config_data` under the `aco_exporter/general/` path prefix. Run `bin/magento aco:config:show` to review current values. The command does not display the client secret.

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
