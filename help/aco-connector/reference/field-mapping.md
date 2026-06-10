---
title: Field Mapping for [!DNL Adobe Commerce Optimizer Connector] Feeds
description: "Learn about [!DNL Adobe Commerce Optimizer Connector] field mapping from [!DNL Adobe Commerce] catalog data to [!DNL Adobe Commerce Optimizer] ingestion API formats for all feeds."
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
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

| [!DNL Adobe Commerce] field | [!DNL Commerce Optimizer] API field | Notes |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId`| `externalIds[0].id` | `origin` fixed to `"AdobeCommerce"` |
| `status` | `status` | Uppercased; set to `DISABLED` for composite products with no assigned children |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | Comma-separated value split and mapped: `Catalog`→`CATALOG`, `Search`→`SEARCH`; unmapped values dropped |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Newline-delimited string split into array |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | JSON-encoded object `{inStock, lowStock, weight, weightType}`; always present as the first attribute entry |
| `attributes[]`                                | `attributes[]` | Each entry mapped to `{code, values[], variantReferenceId}`; `inStock`, `lowStock`, `weight`, `weightType` are excluded (they go into `aco_ac_attributes`) |
| `images[]`                                    | `images[]` | `url`, `label`; standard roles mapped: `image`→`BASE`, `small_image`→`SMALL`, `thumbnail`→`THUMBNAIL`, `swatch_image`→`SWATCH`; non-standard roles go to `customRoles[]` |
| `categoryData[].categoryPath`                 | `routes[].path` | |
| `categoryData[].productPosition`              | `routes[].position` | |
| `links[].type` + `links[].sku`                | `links[]` | `type` uppercased; entries without `sku` dropped |
| `parents[].productType` + `parents[].sku`     | `links[]` | Type mapped: `configurable`→`VARIANT_OF`, `bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options`                        | `configurations[]` | `id`→`attributeCode`, `label`; option type `SWATCH` when `swatchType` is set, else `CONFIGURABLE`; default variant from `isDefault`; values include `variantReferenceId`, `label`, `colorHex`, `imageUrl` |
| `bundle options`                              | `bundles[]` | `label`→`group`; `required`; `renderType` `checkbox`/`multi`→`multiSelect: true`; default SKUs from `isDefault`; items include `sku`, `qty`, `userDefinedQty` (`qtyMutability`) |

## Product attributes metadata

| [!DNL Adobe Commerce] field | [!DNL Commerce Optimizer] API field | Notes |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | See conversion table below |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | Added to array when `true` |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | Added to array when `true` |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | Added to array when `true` |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | Added to array when `true` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

**Data type conversion:**

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | [!DNL Commerce Optimizer] API `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` or `select` | `TEXT` |
| `int` | any other | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| any other | - | `TEXT` |

## Price books

Unlike the other connector feeds, the `priceBooks` feed is not collected by a [!DNL SaaS Data Export] indexer in [!DNL Adobe Commerce]. The connector generates this feed from the website and customer group configuration in the Admin.

One **base price book** is created per website, plus one **child price book** per website-customer group pair.

**Price book ID formula:**

- **Base** (regular prices): `priceBookId = websiteCode`
- **Child** (customer group or shared catalog): `priceBookId = websiteCode::sha1(customerGroupId)` where `sha1(customerGroupId)` is the SHA-1 hex digest of the customer group's integer ID

The prices feed uses the same formula when resolving which price book a price entry belongs to. For how storefronts resolve the `priceBookId` for a customer session, see [Headless storefront integration](../headless-storefront.md#graphql-commerceoptimizer-query).

| Generated field | [!DNL Commerce Optimizer] API field | Notes |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| Website name | `name` | Base price book: website name. Child: `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | Present only on child price books; points to the base price book |
| Website base currency | `currency` | Present only on base price books; inherited by children |

## Prices

| [!DNL Adobe Commerce] field | [!DNL Commerce Optimizer] API field | Notes |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | example of discounts: special price, catalog rule price, shared catalog price |
| `tierPrices[]` | `tierPrices[]` | |

## Categories

Items with an empty `urlPath` (logical root categories) are skipped and never submitted.

| [!DNL Adobe Commerce] field | [!DNL Commerce Optimizer] API field | Notes |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Newline-delimited string split into array |
| `image` | `images[].url` | Single-element array; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` when both `true`, `[]` otherwise |

>[!MORELIKETHIS]
>
> - [Ingest product and price data with the Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — Learn the catalog data model for metadata, products, categories, price books, and prices
> - [Catalog data ingestion REST API Reference](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Review request and response schemas for each feed endpoint
> - [How the [!DNL Commerce Optimizer Connector] works with [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — Learn how store views, websites, and customer groups map to catalog sources and price books
> - [Price books in [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — Manage price books created by the connector export
> - [Headless storefront integration](../headless-storefront.md#graphql-commerceoptimizer-query) — Resolve `priceBookId` for customer sessions
