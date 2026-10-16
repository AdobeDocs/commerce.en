---
title: Field Mapping for [!DNL Adobe Commerce Optimizer Connector] Feeds
description: Learn about [!DNL Adobe Commerce Optimizer Connector] field mapping from [!DNL Adobe Commerce] catalog data to [!DNL Adobe Commerce Optimizer] ingestion API formats for all feeds.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
---

# Field mapping for connector feeds

This page documents how the [!DNL Adobe Commerce Optimizer Connector] transforms [!DNL Adobe Commerce] catalog fields into the format required by the [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. See the [connector reference](connector-reference.md#supported-feeds) for the list of supported feeds and their API endpoints.

## Products

The `products` feed sends data to the [Products endpoint](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| [!DNL Adobe Commerce] field | [!DNL Commerce Optimizer] API field | Mapping details |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId`| `externalIds[0].id` | Sets `origin` to `"AdobeCommerce"` |
| `status` | `status` |Converts the status to uppercase. Uses `DISABLED` if the status is missing or if a configurable or bundle product has no option values. |
| `description` | `description` | Uses an empty string if the description is missing.|
| `shortDescription` | `shortDescription` | Uses an empty string if the short description is missing.|
| `visibility` | `visibleIn` | Splits the comma-separated value and maps `Catalog` to `CATALOG` and `Search` to `SEARCH`. Drops other values. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Splits newline-separated keywords into an array and trims whitespace. |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Always adds an `aco_ac_attributes` entry as the first attribute. Its JSON value includes `inStock` and `lowStock` as strings. It includes `weight` and `weightType` when those values are available. |
| `attributes[]`                                | `attributes[]` | Maps each entry to its attribute code, string values, and matching variant reference ID when available. Skips `inStock`, `lowStock`, `categories`, `weight`, and `weightType`. The inventory-related values are included in `aco_ac_attributes`. Categories are exported as routes. |
| `images[]`                                    | `images[]` | Skips images without a URL.<br>Exports `url`, `label` (empty if missing), and `sortOrder` (integer, defaults to `0`).<br>Sorts images by `sortOrder` in ascending order.<br>Maps standard roles: `image` to `BASE`, `small_image` to `SMALL`, `thumbnail` to `THUMBNAIL`, and `swatch_image` to `SWATCH`. Exports other roles as `customRoles[]`. |
| `categoryData[].categoryPath`                 | `routes[].path` | Skips entries with an empty category path. |
| `categoryData[].productPosition`              | `routes[].position` | Uses `0` if the product position is missing. |
| `links[].type` + `links[].sku`                | `links[]` | `type` uppercased; entries without `sku` dropped |
| `parents[].productType` + `parents[].sku`     | `links[]` | Maps `configurable` to `VARIANT_OF`, and `bundle` or `bundle_fixed` to `IN_BUNDLE`. Converts other product types to uppercase. Skips parents without a SKU. |
| `configurable options`                        | `configurations[]` | Exports options that have an ID and at least one value.<br>Maps `id` to `attributeCode`. Sets `type` to `SWATCH` when `swatchType` is present, and to `CONFIGURABLE` otherwise.<br>Uses the ID of the default value as `defaultVariantReferenceId`.<br>Maps each value to `variantReferenceId`, `label`, `colorHex`, and `imageUrl`. |
| `bundle options`                              | `bundles[]` | Exports options that contain at least one item.<br>Uses the option label as `group`, or `Bundle group` if the label is empty. Copies `required` to the output.<br>Sets `multiSelect` to `true` for `checkbox` and `multi` render types.<br>Lists default SKUs in `defaultItemSkus`. Each item includes `sku`, `qty` (defaults to `0`), and `userDefinedQty` (from `qtyMutability`, defaults to `false`). |

## Product attributes metadata

The `productAttributes` feed sends data to the [Metadata endpoint](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.

| [!DNL Adobe Commerce] field | [!DNL Commerce Optimizer] API field | Mapping details |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | See conversion table below |
| `dataType` and `frontendInput` | `dataType` | Uses the conversion rules below. |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | When a flag is `true`, adds its corresponding value:<br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Data type conversion

When `dataType` is `int`, the connector checks `frontendInput`. For other data types, `frontendInput` does not affect the conversion.

| Input `dataType` | Input `frontendInput` | Output `dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` or `select` | `TEXT` |
| `int` | Any other value, including a missing value | `INTEGER` |
| `decimal` | Not used | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | Not used | `TEXT` |
| `OBJECT` | Not used | `OBJECT` |
| Any other value | Not used | `TEXT` |

>[!NOTE]
>
>When an attribute uses the `OBJECT` data type, the [Products API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} attempts to parse its stored value as JSON. If parsing succeeds, the API returns the value as a nested object. Use `OBJECT` for structured attribute data that cannot be represented as a single value. For instructions, see [Add product attributes dynamically](../../data-export/add-attribute-dynamically.md).

## Price books

The `priceBooks` feed sends data to the [Price books endpoint](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

Unlike the other connector feeds, the `priceBooks` feed is not collected by a [!DNL SaaS Data Export] indexer in [!DNL Adobe Commerce]. The connector generates this feed from the website and customer group configuration in the Admin.

For each website, the connector creates one base price book and one child price book for each customer group.

Use these formulas for `priceBookId`:

- Base price books for regular prices: `priceBookId = websiteCode`.
- Child price books for customer groups: `priceBookId = websiteCode::sha1(customerGroupId)`, where `sha1(customerGroupId)` is the SHA-1 hex digest of the customer group's integer ID.

The prices feed uses the same formula to assign each price entry to a price book. For information about how a storefront resolves `priceBookId` for a customer session, see [Headless storefront integration](../headless-storefront.md#graphql-commerceoptimizer-query).


| Source field or value | [!DNL Commerce Optimizer] API field | Mapping details |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | Adds this field to child price books. Its value identifies the base price book. |
| Website name | `name` | Uses the website name for base price books. Uses `Customer group name (Website name)` for child price books. |
| `websiteCode` | `parentId` | Present only on child price books; points to the base price book |
| Website base currency | `currency` | Includes this field only on base price books. Child price books omit it. |

## Prices

The `prices` feed sends [!DNL Adobe Commerce] data to the [Prices endpoint](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| Feed input field | [!DNL Commerce Optimizer] API field | Mapping details |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | Passes the SKU through unchanged. |
| `websiteCode`, `customerGroupCode` | `priceBookId` | Combines `websiteCode` with the SHA-1 hash of the customer group ID in `customerGroupCode`. If `customerGroupCode` is `0`, uses `websiteCode` alone. |
| `regular` | `regular` | Passes the regular price through unchanged. |
| `discounts[]` | `discounts[]` | If the source value is `null`, exports an empty array.<br>For entries with `code` set to `special_price` and a `percentage`, sets `percentage` to `100 - percentage` when the value is between `0` and `100`. Sets it to `0` at or outside that range.<br>Passes other entries, including price-based special prices, through unchanged. |
| `tierPrices[]` | `tierPrices[]` | Uses an empty array if the source value is missing or `null`. |

## Categories

The `categories` feed sends [!DNL Adobe Commerce] data to the [Categories endpoint](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Items with an empty `urlPath` (logical root categories) are skipped and never submitted.

| [!DNL Adobe Commerce] field | [!DNL Commerce Optimizer] API field | Mapping details |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | Exports the category position when present. Omits the field when it is missing. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Newline-delimited string split into array |
| `image` | `images[].url` | Single-element array; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` when both `true`, `[]` otherwise |

| `metaKeywords` | `metaTags/keywords` | Splits newline-delimited keywords into an array and trims whitespace. |
| `image` | `images[].url` | When `image` is present, exports one image with the `BASE` role. Exports an empty array when the image is empty or missing. |
| `isActive` + `includeInMenu` | `families` | Adds `top_menu` only when both values are `true`. Otherwise, exports an empty array. |
| `attributes[]` | `attributes[]` | Exports entries with a nonempty `attributeCode` as `{code, values[]}`. Converts values to strings. Omits `attributes` when no eligible entries exist. |

>[!MORELIKETHIS]
>
> - [Ingest product and price data with the Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — Learn the catalog data model for metadata, products, categories, price books, and prices
> - [Catalog data ingestion REST API Reference](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Review request and response schemas for each feed endpoint
> - [How the [!DNL Commerce Optimizer Connector] works with [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — Learn how store views, websites, and customer groups map to catalog sources and price books
> - [Price books in [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — Manage price books created by the connector export
> - [Headless storefront integration](../headless-storefront.md#graphql-commerceoptimizer-query) — Resolve `priceBookId` for customer sessions
