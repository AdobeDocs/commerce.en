---
title: Adobe Commerce Optimizer Connector Field Mappings
description: Reference tables for how Adobe Commerce catalog fields map to Adobe Commerce Optimizer API fields for products, categories, prices, price books, and product attributes.
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# Field mappings

This page documents how the Adobe Commerce Optimizer Connector transforms Adobe Commerce feed data into the format required by the Adobe Commerce Optimizer Catalog Data Ingestion API. See [Connector Reference](connector-reference.md#supported-feeds) for the list of supported feeds and their API endpoints.

## Products

| Commerce field                                | Adobe Commerce Optimizer API field | Notes |
|-----------------------------------------------|--------------|-------|
| `sku`                                         | `sku` | |
| `storeViewCode`                               | `source/locale` | |
| `name`                                        | `name` | |
| `urlKey`                                      | `slug` | |
| `productId`                                   | `externalIds[0].id` | `origin` fixed to `"AdobeCommerce"` |
| `status`                                      | `status` | Uppercased; set to `DISABLED` for composite products with no assigned children |
| `description`                                 | `description` | |
| `shortDescription`                            | `shortDescription` | |
| `visibility`                                  | `visibleIn` | Comma-separated value split and mapped: `Catalog`→`CATALOG`, `Search`→`SEARCH`; unmapped values dropped |
| `metaTitle`                                   | `metaTags/title` | |
| `metaDescription`                             | `metaTags/description` | |
| `metaKeyword`                                 | `metaTags/keywords` | Newline-delimited string split into array |
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

| Commerce field | Adobe Commerce Optimizer API field | Notes |
|---------------|--------------|-------|
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

| Commerce `dataType` | Commerce `frontendInput` | Adobe Commerce Optimizer API `dataType` |
|--------------------|--------------------------|-------------------|
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` or `select` | `TEXT` |
| `int` | any other | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| any other | - | `TEXT` |

## Price books

Price books are generated entirely by the connector from website and customer group configuration - they have no direct Commerce feed counterpart.

One **base price book** is created per website, plus one **child price book** per website-customer group pair.

**Price book ID formula:**

- **Base** (regular prices): `priceBookId = websiteCode`
- **Child** (customer group or shared catalog): `priceBookId = websiteCode::sha1(customerGroupId)` where `sha1(customerGroupId)` is the SHA-1 hex digest of the customer group's integer ID

The prices feed uses the same formula when resolving which price book a price entry belongs to. For how storefronts resolve the `priceBookId` for a customer session, see [Headless Storefront Integration](../headless-storefront.md#graphql-commerceoptimizer-query).

| Generated field | Adobe Commerce Optimizer API field | Notes |
|----------------|--------------|-------|
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| Website name | `name` | Base price book: website name. Child: `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | Present only on child price books; points to the base price book |
| Website base currency | `currency` | Present only on base price books; inherited by children |

## Prices

| Commerce field | Adobe Commerce Optimizer API field | Notes                                                                         |
|---------------|--------------|-------------------------------------------------------------------------------|
| `sku` | `sku` |                                                                               |
| `websiteCode`, `customerGroupId` | `priceBookId` |                                                                               |
| `regular` | `regular` |                                                                               |
| `discounts[]` | `discounts[]` | example of discounts: special price, catalog rule price, shared catalog price |
| `tierPrices[]` | `tierPrices[]` |                                                              |

## Categories

Items with an empty `urlPath` (logical root categories) are skipped and never submitted.

| Commerce field | Adobe Commerce Optimizer API field | Notes |
|---------------|--------------|-------|
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Newline-delimited string split into array |
| `image` | `images[].url` | Single-element array; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` when both `true`, `[]` otherwise |
