---
title: '[!DNL Adobe Commerce Optimizer Connector] Modules and Feed Endpoints'
description: "Learn about [!DNL Adobe Commerce Optimizer Connector] modules, catalog feed API endpoints, batch limits, and core_config_data configuration paths for [!DNL Adobe Commerce]."
feature: Integration, Configuration
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Connector modules and feed endpoints

This reference lists the [!DNL Adobe Commerce Optimizer Connector] module packages, supported feed API endpoints, and configuration key paths stored in `core_config_data`. To learn how these components work together during synchronization, see [Connector sync pipeline](../connector-sync-pipeline.md).

## Modules

The connector includes multiple Magento modules that collect catalog data, map feed data to the format supported by the [!DNL Commerce Optimizer] API, and manage submission and scope control. The following table summarizes each module and its role.

| Module | Role |
| ------ | ---- |
| `DataExporterAdapter` | Maps [!DNL Adobe Commerce] feeds to the format required by the [!DNL Adobe Commerce Optimizer] API. Overrides feed pool and schema config. |
| `SaasExportAdapter` | Routes [!DNL Commerce Optimizer] feeds to the ingestion API and blocks unsupported feeds from submission. |
| `CommerceAcoExporter` | Manages [!DNL Commerce Optimizer] credentials and provides CLI setup commands |
| `CommerceAdapter` | [!DNL Commerce Optimizer] API compatibility layer (GraphQL, bundle add-to-cart, config UI) |
| `PriceBookDataExporter` | Price book feed indexed by website and customer group |
| `SaasPriceBook` | SaaS infrastructure for price book submission |
| `CommerceOptimizerScopeMapper` | Per-website and per-store-view sync enablement |

## Supported feeds

The connector submits multiple feed types to the [!DNL Commerce Optimizer] [[!DNL Catalog Data Ingestion API]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}. The table below lists each feed with its endpoint, batch limit, indexer name, and feed table in [!DNL Adobe Commerce].

| Feed | [!DNL Commerce Optimizer] API Endpoint | Batch Limit | AC Index Name | Feed Table |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

The `products`, `productAttributes`, `categories`, and `prices` feeds reuse data collected by [!DNL SaaS Data Export] indexers. The connector generates the `priceBooks` feed from website and customer group configuration and does not rely on a [!DNL SaaS Data Export] indexer.

For field-level mapping details for each feed, see [Field mapping for [!DNL Commerce Optimizer Connector] feeds](field-mapping.md).
To estimate how long a sync will take based on your catalog size, see [Estimate data volume and sync time](estimate-data-volume-sync-time.md).

## Configuration paths

[!DNL Commerce Optimizer Connector] credentials and service URLs are stored in `core_config_data` under the `aco_exporter/general/` path prefix. Run `bin/magento aco:config:show` to review current values. The command does not display the client secret.

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
