---
title: "[!DNL Commerce Storefront Catalog Service Release Notes]"
description: "The latest release information for [!DNL Catalog Service] for Adobe Commerce."
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
---
# [!DNL Commerce Storefront Catalog Service] Release Notes

These release notes cover the latest Commerce Catalog Service updates, including:

- **Storefront Catalog Service releases**

  - Catalog Service API schema enhancements for improved data retrieval.
  - Security, performance, and reliability improvements for the Catalog Service API and underlying infrastructure.

- **Catalog Service metapackage releases**

  - Updated dependencies for improved performance, stability, and compatibility with other Adobe Commerce components.

Updates are categorized by type:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues

Support is provided for the latest version. Release notes for older versions are included for reference.

## Storefront Catalog Service

### v1.47 release

_February 12, 2025_

![New](../assets/new.svg) The API service now supports `CategoryProductView` type, enabling enhanced views and queries for products by category. This update allows developers to efficiently retrieve and filter product data based on category, improving flexibility and performance for category-driven use cases. For details, see [Implement categories on the storefront](https://developer-stage.adobe.com/commerce/services/optimizer/merchandising-services/categories-storefront-implementation/). Only supported on Commerce implementations using the [composable catalog data model](https://developer.adobe.com/commerce/services/optimizer/)for headless storefronts<!--DATA-6949-->

### v1.46 release

_December 11, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6852, DATA-6864-->

### v1.45 release

_November 17, 2025_

![New](../assets/new.svg) **Attribute Filtering by Name**–The `productSearch` GraphQL query now supports filtering product attributes with the `names` field. <!--DATA-6831--> With this filter, you can:

- Reduce response payload size by requesting only specific attributes
- Combine with the existing `roles` filter to narrow by visibility role and attribute name
- Examples:

  **Filter by attribute names only**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **Filter by both roles and names:**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>To retrieve all attributes without filtering, omit the `names` argument or provide an empty array.

### v1.44 release

_November 6, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6852, DATA-6864-->

### v1.43 release

_November 3, 2025_

![New](../assets/new.svg) **Product Layers for multi-dimensional product customization**—Added support for channel-specific, locale-aware content delivery for Adobe Commerce Optimizer implementations.<!--DATA-6632-->

- Serve different product content to different customer segments
- Apply locale-specific customizations without duplicating base data
- Control field-level overrides with Layer Masks
- Support for premium, seasonal, and mobile-optimized content layers

  Layers are retrieved using the existing `products` query, are applied server-side from request headers, and require no schema changes. See [Catalog layer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-layer) in the _Adobe Commerce Optimizer Guide_.

![Fix](../assets/fix.svg) Grouped products can now be queried when the parent has no pricing; child products return their own visibility roles.<!--DATA-6779-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6721, DATA-6864-->

### v1.42 release

_September 8, 2025_

![New](../assets/new.svg) **Added Tier Pricing support** to query volume pricing:<!--DATA-6643-->

To retrieve tier pricing:

1. Use the `products` query with your desired SKUs
2. For **SimpleProductView**, access `price.tiers`
3. For **ComplexProductView**, access `priceRange.minimum.tiers` and `priceRange.maximum.tiers`
4. Each tier contains the discounted `tier` price and `quantity` conditions
5. Define quantity thresholds with `gte` (greater than or equal to) and `lt` (less than)

**Example:**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![Fix](../assets/fix.svg) **Tier prices filtered by minimum final price** <!--DATA-6643-->

The API now returns only tiers whose discounted price is **lower than** the product's minimum final price. Higher tiers are omitted because the minimum final price would apply on the storefront instead.

Applies to:

- **Simple products**: `price.tiers` only includes tiers with `tier.amount.value` &lt; `price.final.amount.value` (minimum final).
- **Complex products**: `priceRange.minimum.tiers` and `priceRange.maximum.tiers` use the same rule when building the price range.

### v1.41 release

_September 2, 2025_

![Fix](../assets/fix.svg) **Improved error handling for missing price information**—When price data is not yet received, the API returns `null` for the price field instead of throwing an error, allowing clients to handle missing data gracefully.<!--DATA-6612-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability.<!--DATA-6671-->

### v1.40 release

_July 30, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6619-->

### v1.39 release

_July 24, 2025_

![New](../assets/new.svg) **Retrieve recommendation units by unit ID**–New GraphQL endpoint `recommendationsByUnitIds` retrieves recommendation units by their unique ID for more flexible, targeted access.

- `unitIds` is required (list of recIds to fetch).
- Context parameters (`currentSku`, `cartSkus`, `userViewHistory`, `userPurchaseHistory`, `category`) behave the same as in the existing recommendations query.

- **Example**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6316-->

### v1.38 release

_July 15, 2025_

![New](../assets/new.svg) **Gift card product types**–Catalog Storefront Service now supports product attributes as JSON objects or arrays, enabling flexible management of complex types such as gift cards.<!--DATA-6573-->


### v1.37 release

_June 20, 2025_

![New](../assets/new.svg) **Hierarchical price book configuration**—Accurate price ranges for parent-child price books. Calculations respect hierarchy and inherited rules; reduces pricing errors when multiple price books are linked. Adobe Commerce Optimizer only. See [Price Books](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![New](../assets/new.svg) **Case-insensitive keys**—Key lookups in queries are now case-insensitive, reducing errors from key casing. <!--DATA-6494, DCAT-2495-->

### v1.36 release

_June 20, 2025_

![New](../assets/new.svg) **Public IO Events for Catalog Storefront**—Added public IO events for real-time integration and observability (CSS and EDS).<!--DATA-6329-->

![New](../assets/new.svg) **Server-Side Rendering (SSR)**—Architectural improvements to support SSR for better performance, SEO, and UX on large catalogs.<!--DATA-6278, DATA-6280-->

![New](../assets/new.svg) **Infrastructure & Security**—New AWS roles, ServiceNow integration, and CI/CD pipelines for the events service.

![New](../assets/new.svg) **Event formats & observability**—Streamlined payloads, enhanced monitoring, improved variant event data.<!--DATA-6332, DATA-6402, -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6404, DATA-6410, -->

+++ Previous versions

## v1.35 release

_June 13, 2025_

![New](../assets/new.svg) **Retrieve uncached data**–Enable the `Magento-Is-Preview` header to pass uncached data from the catalog endpoint to the Search Service.<!--DATA-6345-->

![New](../assets/new.svg) **Multi-select product options**–GraphQL API now exposes whether product options allow multiple selections (for example, bundle "choose multiple items").<!--DATA-6487-->

![New](../assets/new.svg) Updated price validation on data ingestion to support products without prices.<!--DATA-6098-->

![Fix](../assets/fix.svg) Improved error handling for simple bundle pricing in Adobe Commerce Optimizer.<!--DATA-6541-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6273, DATA-6485, -->

## v1.34 release

_March 23, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-5732-->

## v1.33 release

_April 29, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements. Infrastructure now supports extremely large catalogs (up to ~440 million SKUs) without impacting existing workloads.

### v1.32 release

_March 28, 2025_

![Fix](../assets/fix.svg) Attributes without roles are no longer indexed by default for the composable catalog, improving indexing time and reducing storage. Legacy behavior can be re-enabled via a feature flag.

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability. <!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### v1.31 release

_February 18, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6389, DATA-6367, DATA-6373-->

### v1.30 release

_December 9, 2024_

Major release: [composable catalog data model](https://developer.adobe.com/commerce/services/optimizer/) for headless storefronts, header management, and product data handling.

![New](../assets/new.svg) **Composable Catalog Data Model (CCDM)**—Supports customers using the composable catalog for headless storefronts. New endpoints accept Catalog View and Policy IDs (backward compatible). Configurable product details and prices with built-in pagination.<!--DATA-6018, DATA-6288-->

![New](../assets/new.svg) **Header Management**–`AC-Locale` renamed to `AC-Scope-Locale` for composable catalog API operations; header mapping and default values specified.<!--DATA-6303, DATA-6078-->

![New](../assets/new.svg) **Product Data & Pricing**–Support for composable catalog data model and improved price handling for configurable products.<!--DATA-6279-->

`CurrencyEnum` updated to support `NONE` for product search queries, aligning with federation logic.<!--DATA-6285-->

![Fix](../assets/fix.svg) **Infrastructure & upgrades**—System-level improvements for security, performance, and stability.

![Fix](../assets/fix.svg) Bundle product options now display only enabled products.<!--DATA-6347-->

### v1.29 release

_December 9, 2024_

![New](../assets/new.svg) **Image ordering in product queries**—Product images in the GraphQL `images` field now follow catalog export `sortOrder` for consistent storefront and API behavior.<!--DATA-6258-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6619-->

### v1.28 release

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### v1.27 release

_September 26, 2024_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6243-->

### v1.26 release

_October 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) GraphQL schema now includes `lastModifiedAt` in product information for accurate sitemaps and search-engine reindexing (e.g., Google). <!--DATA-6209-->

### v1.23 release

_August 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Product information can now be retrieved without product override (prices) data. Previously, these queries returned: `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### v1.22 release

_August 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added support to retrieve all variants by product SKU. See the [Catalog Service API Reference](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### v1.19 release

_May 23, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer


![Fix](../assets/fix.svg) <!--DATA-5033-->The `InStock` flag for option values now respects the scoped `enabled` status of the product variant.

![Fix](../assets/fix.svg) <!--DATA-5888-->Added support for product prices with up to 16 digits and 4 decimal places. Resync from the [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) or [CLI](../landing/catalog-sync.md#command-line-interface) to apply updates.

#### Known limitations

The following features are not yet supported:

- The maximum size for dynamic attributes payload is 9 MB.
- The Group product price can be calculated with simple product prices.
- In an image array, only the first image contains roles.

Use API Mesh and the Core GraphQL API for:

- Minimum Advertised Price
- Tier pricing
- Bundle products with fixed prices

For details and examples, see [Catalog Service and API Mesh](mesh.md).

### v1.18 release

_April 11, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added support for PHP 8.3.

![New](../assets/new.svg) The [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) and [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) queries now return customizable options data for both simple and complex products.<!--DATA-5538-->

### v1.17 release

_February 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) is now available for data streams (Product Recommendations, Live Search, Catalog Service). Requires `catalog-service` metapackage v3.1.0+.

### v1.16 release

_February 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Product videos are now supported by the Catalog Service API.
![Fix](../assets/fix.svg) Out-of-stock options are now shown in the PDP widget.

#### Known limitations

These features are not yet supported:

- The maximum size for dynamic attributes payload is 9 MB.
- Group product price. This value can be calculated with simple product prices.
- In an image array, only the first image contains roles.

Use API Mesh and the Core GraphQL API for:

- Minimum Advertised Price
- [Tier pricing](mesh.md)

### v1.13 release

_October 12, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service supports the `inStock` flag for product variants.
![New](../assets/new.svg) The `urlKey` and `externalId` fields have been added to the GraphQL schema.
![New](../assets/new.svg) Downloadable products and gift cards are now supported.

### v1.12 release

_September 19, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now uses [SaaS price indexing](../price-index/price-indexing.md).
![Fix](../assets/fix.svg) This release contains bug fixes and improvements on the service side.

### v1.11 release

_July 18, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now supports the [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL query for Product Recommendations.

### v1.10 release

_June 27, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The Catalog Service API now supports `related products`.

### v1.7 release

_April 12, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now cleans up deleted product variants.
![Fix](../assets/fix.svg) Infrastructure scalability and performance improvements.

### v1.6 release

_March 28, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added swatches to the [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) query.
![New](../assets/new.svg) Added the ability to get `entityId` using [API Mesh](mesh.md).

### v1.5 release

_March 6, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL functionality.
![Fix](../assets/fix.svg) Improved performance and API scalability.

### v1.4 release

_February 7, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Published catalog-service metapackage to simplify installation steps.
![Fix](../assets/fix.svg) API scalability and performance improvements.

### v1.3 release

_January 17, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Simplified and improved the onboarding experience.
![New](../assets/new.svg) New customer sandbox endpoints are available for pre-production testing.
![New](../assets/new.svg) Support added for virtual products.
![Fix](../assets/fix.svg) API scalability and performance improvements.

### v1.1 release

_November 18, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Catalog Service now supports Adobe's [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/).
![Fix](../assets/fix.svg) Improved API scalability and overall performance.

### v1.0 release

_October 4, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Support for bundled and grouped products.
![New](../assets/new.svg) Added B2B visibility overrides. Products are now searchable and can be added to the cart for specific customer groups.
![Fix](../assets/fix.svg) Service is now more stable and has improved performance.

### 0.3 release - Beta+

_September 12, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Variant images: product images returned based on selected options.
![New](../assets/new.svg) Price roles: only members of specific customer groups can see product prices.
![Fix](../assets/fix.svg) Improved stability and performance of the service.
![New](../assets/new.svg) Updates are received when products are deleted from the catalog.

### Beta Release

_August 9, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) The `products` and `refineProduct` queries return the following data:

- Predefined (system) product attributes.
- Dynamic product attributes and filter them by role (product display page/product list page).
- Product options.
- Product images and filter them by role (PDP/PLP).
- A specific price for simple products and price ranges for configurable products.
- Customer group prices and price ranges. They return a fallback default price on shoppers without a customer group.
- Product types that use B2B customer-specific pricing.

+++

## Catalog Service metapackage

Updates to the Catalog Service PHP metapackage (`magento/catalog-service`).

- For Adobe Commerce as a Cloud Service customers, the latest version is installed in your environment.

- For Adobe Commerce on cloud on-premises, Adobe recommends using Composer to upgrade the Catalog Service metapackage in your cloud environments the latest release.

### v3.3.0 release

_October 14, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) **Data Services upgrade**—`magento/data-services` dependency updated to ^8.0.0. Verify environment and custom Data Services API usage for 8.x compatibility before upgrading.
ea
![New](../assets/new.svg) Updated version and metadata for the 3.3.0 release.

### v3.2.0 release

_April 12, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Version and metadata updated for 3.2.0. No other dependency changes.

### v3.1.0 release

_January 26, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added new package dependencies:

- **Category permission data exporter** (`magento/module-category-permission-data-exporter`) for exporting category permission data used by the catalog service.
- **Catalog Sync Admin** `magento/module-catalog-sync-admin` for Admin UI and configuration related to catalog sync.

![New](../assets/new.svg) Updated version and metadata for the 3.1.0 release.

## Related documentation

- For projects deployed on **Adobe Commerce on cloud, on-premises, or Adobe Commerce as a Cloud Service, see the following documentation:

  - [Catalog Service Guide](overview.md)
  - [Catalog Service GraphQL API Reference](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
  - [Adobe Commerce Admin Guide](https://experienceleague.adobe.com/en/docs/commerce-admin/)
  - [Adobe Commerce as a Cloud Service Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
  - [Adobe Commerce on Cloud Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- For projects using **Adobe Commerce Optimizer** or **Adobe Commerce Optimizer Connector**, see the following documentation:

  - [Merchandising Services Developer Guide](https://developer.adobe.com/commerce/services/optimizer/)
  - [Merchandising GraphQL API Reference](https://developer.adobe.com/commerce/services/reference/graphql/)
  - [Adobe Commerce Optimizer Guide](../optimizer/overview.md)
