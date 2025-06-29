---
title: '[!DNL Catalog Service] Release Notes'
description: The latest release information for [!DNL Catalog Service] for Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
---
# [!DNL Catalog Service] Release Notes

These release notes describe the latest versions of [!DNL Catalog Service].
Support is provided for the current major released version. Release notes for older versions are provided for reference.
Updates include:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues

## Current major version

### V1.26 Release

_October 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The GraphQL schema now includes the `lastModifiedAt` attribute in the product information. This precise timestamp helps customers ensure that sitemaps accurately reflect the most recent updates to their products. It also helps search engines like Google determine when reindexing is necessary, optimizing the crawling process and preventing issues related to aggressive last modified dates used when precise information is not available. <!--DATA-6209-->

## Previous versions

+++ Previous versions

### V1.23 Release

_August 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) You can now retrieve product information without product override (prices) data. In previous releases, these queries returned the following error:
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### V1.22 Release

_August 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added support to retrieve all variants by product SKU. See the [Catalog Service API Reference](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### V1.22 Release

_August 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added support to retrieve all variants by product SKU. See the [Catalog Service API Reference](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### V1.19 Release

_May 23, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer


![Fix](../assets/fix.svg) <!--DATA-5033-->The `InStock` flag for option values now takes into account the scoped `enabled` status of the product variant.

![Fix](../assets/fix.svg) <!--DATA-5888-->Add support for product prices that require large numbers (up to 16 digits) and greater decimal precision (up to 4 decimal places). To apply the price configuration updates to your existing catalog, resync catalog data from the [Data Management dashboard ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard), or by using the [Adobe Commerce command-line interface](../landing/catalog-sync.md#command-line-interface).

#### Known limitations

The following features are not yet supported:

* The maximum size for dynamic attributes payload is 9 MB.
* The Group product price can be calculated with simple product prices.
* In an image array, only the first image contains roles.

Solve the following limitations by using API Mesh and the Core GraphQL API:

* Minimum Advertised Price
* Tier pricing
* Bundle products with fixed prices

For details and examples, see [Catalog Service and API Mesh](mesh.md)

### V1.18 Release

_April 11, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added support for PHP 8.3.

![New](../assets/new.svg) The [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) and [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) queries now return customizable options data for both simple and complex products.<!--DATA-5538-->

### V1.17 Release

_February 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) is now available. This revamped dashboard provides insights into data streams for [!DNL Product Recommendations], [!DNL Live Search], and [!DNL Catalog Service]. Support for this feature was introduced in v3.1.0 of the `catalog-service` metapackage.

### V1.16 Release

_February 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Product videos are now supported by the Catalog Service API.
![Fix](../assets/fix.svg) Out-of-stock options are now shown in the PDP widget.

#### Known limitations

These features are not yet supported:

* The maximum size for dynamic attributes payload is 9 MB.
* Group product price. This value can be calculated with simple product prices.
* In an image array, only the first image contains roles.

The following limitations can be solved by using API Mesh and the Core GraphQL API:

* Minimum Advertised Price
* [Tier pricing](mesh.md)

### V1.13 Release

_October 12, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service supports the `inStock` flag for product variants.
![New](../assets/new.svg) The `urlKey` and `externalId` fields have been added to the GraphQL schema.
![New](../assets/new.svg) Downloadable products and gift cards are now supported.

### V1.12 Release

_September 19, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now uses [SaaS price indexing](../price-index/price-indexing.md).
![Fix](../assets/fix.svg) This release contains bug fixes and improvements on the service side.

### V1.11 Release

_July 18, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now supports the [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/recommendations/) GraphQL query for Product Recommendations.

### V1.10 Release

_June 27, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The Catalog Service API now supports `related products`.

### V1.7 Release

_April 12, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now cleans up deleted product variants.
![Fix](../assets/fix.svg) Infrastructure scalability and performance improvements.

### V1.6 Release

_March 28, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added swatches to the [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) query.
![New](../assets/new.svg) Added the ability to get `entityId` using [API Mesh](mesh.md).

### V1.5 Release

_March 6, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL functionality.
![Fix](../assets/fix.svg) Improved performance and API scalability.

### V1.4 Release

_February 7, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Published catalog-service metapackage to simplify installation steps.
![Fix](../assets/fix.svg) API scalability and performance improvements.

### V1.3 Release

_January 17, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Simplified and improved the onboarding experience.
![New](../assets/new.svg) New customer sandbox endpoints are available for pre-production testing.
![New](../assets/new.svg) Support added for virtual products.
![Fix](../assets/fix.svg) API scalability and performance improvements.

### V1.1 Release

_November 18, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Catalog Service now supports Adobe's [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/).
![Fix](../assets/fix.svg) Improved API scalability and overall performance.

### V1.0 Release

_October 4, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Now support bundled and grouped products.
![New](../assets/new.svg) Added B2B visibility overrides. Products are now searchable and can be added to the cart for specific customer groups.
![Fix](../assets/fix.svg) Service is now more stable and has improved performance.

### 0.3 Release - Beta+

_September 12, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Images for variants support: product images are returned based on the selected options
![New](../assets/new.svg) Roles for prices support: allow only members of specific customer groups to see the price of products
![Fix](../assets/fix.svg) Improved stability and performance of the service
![New](../assets/new.svg) Updates are received when products are deleted from the catalog

### Beta Release

_August 9, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) The `products` and `refineProduct` queries return the following data:

* Predefined (system) product attributes.
* Dynamic product attributes and filter them by role (product display page/product list page).
* Product options.
* Product images and filter them by role (PDP/PLP).
* A specific price for simple products and price ranges for configurable products.
* Customer group prices and price ranges. They return a fallback default price on shoppers without a customer group.
* Product types that use B2B customer-specific pricing.
