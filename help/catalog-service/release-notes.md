---
title: "[!DNL Commerce Storefront Catalog Service Release Notes]"
description: The latest release information for [!DNL Catalog Service] for Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# [!DNL Commerce Storefront Catalog Service] Release Notes

These release notes cover the latest Commerce Catalog Service updates, including:

- **[Storefront Catalog Service releases](#storefront-catalog-service)**

  - Catalog Service API schema enhancements for improved data retrieval
  - Security, performance, and reliability improvements for the Catalog Service API and underlying infrastructure.

  See [Storefront Services schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) in the Commerce Developer documentation for more information about these APIs.

- **[Catalog Service metapackage releases](#catalog-service-metapackage)**

  - Updated dependencies for improved performance, stability, and compatibility with other Adobe Commerce components.

- **[Catalog Service Installer releases](#catalog-service-installer)**

  - Updated dependencies to maintain compatibility between the Catalog Service and your Commerce stack.

>[!NOTE]
>
>If your Commerce project uses Adobe Commerce Optimizer to deliver catalog data to Commerce Edge Delivery Service or headless storefronts, see the [Adobe Commerce Optimizer release notes](../optimizer/release-notes.md) for the latest API updates.

Updates are categorized by type:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues

Support is provided for the latest version. Release notes for older versions are included for reference.

## Storefront Catalog Service

## June 2026

**Release date**: June TBD, 2026

<!-- v1.3 -->

![New](../assets/new.svg) **New canEditQuantity field**—Added and propagated the canEditQuantity field on bundle product selections (ProductViewOptionValueProduct), surfacing Commerce's existing quantity-mutability setting through the  GraphQL schema so storefront consumers can tell whether a bundle selection quantity is editable.
<!--COMOPT-2050-->

### May 2026

**Release date**: May 20, 2026
<!-- v1.55 -->

![New](../assets/new.svg) Enforced limit of maximum 100 SKUs per request for both Adobe Commerce and Adobe Commerce as a Cloud Service clients as per [documented limits and boundaries](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits).
<!--DATA-7163-->

**Release date**: May 13, 2026
<!--v1.54-->

![New](../assets/new.svg) **Category sort order in GraphQL**—The `CategoryView` GraphQL type now includes a position field, so storefronts can display categories in the order merchants configure in the catalog hierarchy.
<!--DATA-7166-->

**Release date**: May 4, 2026
<!-- v1.53 -->

![Fix](../assets/fix.svg) Storefront product prices now display the correct currency code (for example, USD) for all product types. Previously, some products showed `NONE` instead of the expected currency, resulting in missing prices. This update ensures consistent and accurate price rendering across the storefront.<!--DATA-7115-->

### April 2026

**Release date**: April 29, 2026
<!--v1.52-->

![New](../assets/new.svg) Enforced limit of maximum 100 SKUs per request for Adobe Commerce Optimizer and Adobe Commerce as a Cloud Service
clients as per [documented limits and boundaries](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits). <!--DATA-7156-->

**Release date**: April 17, 2026
<!--v1.51-->

![New](../assets/new.svg) Added a new `searchCategory` GraphQL query that enables clients to search categories by name with paginated results. The query accepts a required `searchTerm` (minimum 3 characters) and optional `family`, `pageSize`, and `currentPage` parameters. Results include matching `CategoryTreeView` objects with full category metadata, a `totalCount`, and `pageInfo` for pagination. <!--COMOPT-1819-->

This query is available only for customers using Adobe Commerce Optimizer Merchandising Services. See [searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/).

### March 2026

**Release date**: March 24, 2026
<!--v1.49-->

![New](../assets/new.svg) Added support to compute and return the price range for dynamic bundles.
<!--DATA-7115-->

### December 2025

**Release date**: December 11, 2025
<!-- v1.46 -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. 
<!--DATA-6852, DATA-6864-->

### November 2025

**Release date**: November 17, 2025
<!-- v1.45 -->

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

**Release date**: November 6, 2025
<!-- v1.44 -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6852, DATA-6864-->

![Fix](../assets/fix.svg) Grouped products can now be queried when the parent has no pricing; child products return their own visibility roles.<!--DATA-6779-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6721, DATA-6864-->

### September 2025

**Release date**: September 8, 2025
<!-- v1.42 -->

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

**Release date**: September 2, 2025
<!-- v1.41 -->

![Fix](../assets/fix.svg) **Improved error handling for missing price information**—When price data is not yet received, the API returns `null` for the price field instead of throwing an error, allowing clients to handle missing data gracefully.<!--DATA-6612-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability.<!--DATA-6671-->

### July 2025

**Release date**: July 30, 2025
<!-- v1.40 -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6619-->

**Release date**: July 24, 2025
<!-- v1.39 -->

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

**Release date**: July 15, 2025
<!-- v1.38 -->

![New](../assets/new.svg) **Gift card product types**–Catalog Storefront Service now supports product attributes as JSON objects or arrays, enabling flexible management of complex types such as gift cards.<!--DATA-6573-->

+++Previous versions

### June 2025

**Release date**: June 20, 2025
<!-- v1.37 -->

![New](../assets/new.svg) **Hierarchical price book configuration**—Accurate price ranges for parent-child price books. Calculations respect hierarchy and inherited rules; reduces pricing errors when multiple price books are linked. Adobe Commerce Optimizer only. See [Price Books](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![New](../assets/new.svg) **Case-insensitive keys**—Key lookups in queries are now case-insensitive, reducing errors from key casing. <!--DATA-6494, DCAT-2495-->

**Release date**: June 20, 2025
<!-- v1.36 -->

![New](../assets/new.svg) **Public IO Events for Catalog Storefront**—Added public IO events for real-time integration and observability (CSS and EDS).<!--DATA-6329-->

![New](../assets/new.svg) **Server-Side Rendering (SSR)**—Architectural improvements to support SSR for better performance, SEO, and UX on large catalogs.<!--DATA-6278, DATA-6280-->

![New](../assets/new.svg) **Infrastructure & Security**—New AWS roles, ServiceNow integration, and CI/CD pipelines for the events service.

![New](../assets/new.svg) **Event formats & observability**—Streamlined payloads, enhanced monitoring, improved variant event data.<!--DATA-6332, DATA-6402, -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6404, DATA-6410, -->

**Release date**: June 13, 2025
<!-- v1.35 -->

![New](../assets/new.svg) **Retrieve uncached data**–Enable the `Magento-Is-Preview` header to pass uncached data from the catalog endpoint to the Search Service.<!--DATA-6345-->

![New](../assets/new.svg) **Multi-select product options**–GraphQL API now exposes whether product options allow multiple selections (for example, bundle "choose multiple items").<!--DATA-6487-->

![New](../assets/new.svg) Updated price validation on data ingestion to support products without prices.<!--DATA-6098-->

![Fix](../assets/fix.svg) Improved error handling for simple bundle pricing in Adobe Commerce Optimizer.<!--DATA-6541-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6273, DATA-6485, -->

### April 2025

**Release date**: April 8, 2025
<!-- v1.34 -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-5732-->

<!-- v1.33 -->
![Fix](../assets/fix.svg) Infrastructure now supports extremely large catalogs (up to ~440 million SKUs) without impacting existing workloads.

### March 2025

**Release date**: March 28, 2025
<!-- v1.32 -->

![Fix](../assets/fix.svg) Attributes without roles are no longer indexed by default for the composable catalog, improving indexing time and reducing storage. Legacy behavior can be re-enabled via a feature flag.

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.
<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### February 2025

**Release date**: February 18, 2025
<!-- v1.31 -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6389, DATA-6367, DATA-6373-->

### December 2024

**Release date**: December 9, 2024
<!-- v1.30 -->

Major release: [composable catalog data model](https://developer.adobe.com/commerce/services/optimizer/) for headless storefronts, header management, and product data handling.

![New](../assets/new.svg) **Composable Catalog Data Model (CCDM)**—Supports customers using the composable catalog for headless storefronts. New endpoints accept Catalog View and Policy IDs (backward compatible). Configurable product details and prices with built-in pagination.<!--DATA-6018, DATA-6288-->

![New](../assets/new.svg) **Header Management**–`AC-Locale` renamed to `AC-Scope-Locale` for composable catalog API operations; header mapping and default values specified.<!--DATA-6303, DATA-6078-->

![New](../assets/new.svg) **Product Data & Pricing**–Support for composable catalog data model and improved price handling for configurable products.<!--DATA-6279-->

`CurrencyEnum` updated to support `NONE` for product search queries, aligning with federation logic.<!--DATA-6285-->

![Fix](../assets/fix.svg) **Infrastructure & upgrades**—System-level improvements for security, performance, and stability.

![Fix](../assets/fix.svg) Bundle product options now display only enabled products.<!--DATA-6347-->

**Release date**: December 9, 2024
<!-- v1.29 -->

![New](../assets/new.svg) **Image ordering in product queries**—Product images in the GraphQL `images` field now follow catalog export `sortOrder` for consistent storefront and API behavior.<!--DATA-6258-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.<!--DATA-6619-->

**Release date**: December 2024
<!-- v1.28 -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.
<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### October 2024

**Release date**: October 22, 2024
<!-- v1.26 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) GraphQL schema now includes `lastModifiedAt` in product information for accurate sitemaps and search-engine reindexing (e.g., Google).
<!--DATA-6209-->

### September 2024

**Release date**: September 26, 2024
<!-- v1.27 -->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability.
<!--DATA-6243-->

### August 2024

**Release date**: August 22, 2024
<!-- v1.23 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Product information can now be retrieved without product override (prices) data. Previously, these queries returned: `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.`
<!--DATA-6121-->

**Release date**: August 13, 2024
<!-- v1.22 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added support to retrieve all variants by product SKU. See the [Catalog Service API Reference](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).
<!--DATA-6067-->

### May 2024

**Release date**: May 23, 2024
<!-- v1.19 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer


![Fix](../assets/fix.svg) The `InStock` flag for option values now respects the scoped `enabled` status of the product variant.

<!--DATA-5033-->

![Fix](../assets/fix.svg) Added support for product prices with up to 16 digits and 4 decimal places. Resync from the [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) or [CLI](../data-export/data-export-cli-commands.md) to apply updates.
<!--DATA-5033-->

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

### April 2024

**Release date**: April 11, 2024
<!-- v1.18 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added support for PHP 8.3.

![New](../assets/new.svg) The [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) and [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) queries now return customizable options data for both simple and complex products.<!--DATA-5538-->

### February 2024

**Release date**: February 22, 2024
<!-- v1.17 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) is now available for data streams (Product Recommendations, Live Search, Catalog Service). Requires `catalog-service` metapackage v3.1.0+.

**Release date**: February 13, 2024
<!-- v1.16 -->

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

### October 2023

**Release date**: October 12, 2023
<!-- v1.13 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service supports the `inStock` flag for product variants.
![New](../assets/new.svg) The `urlKey` and `externalId` fields have been added to the GraphQL schema.
![New](../assets/new.svg) Downloadable products and gift cards are now supported.

### September 2023

**Release date**: September 19, 2023
<!-- v1.12 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now uses [SaaS price indexing](../price-index/price-indexing.md).
![Fix](../assets/fix.svg) This release contains bug fixes and improvements on the service side.

### July 2023

**Release date**: July 18, 2023
<!-- v1.11 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now supports the [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL query for Product Recommendations.

### June 2023

**Release date**: June 27, 2023
<!-- v1.10 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The Catalog Service API now supports `related products`.

### April 2023

**Release date**: April 12, 2023
<!-- v1.7 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Catalog Service now cleans up deleted product variants.
![Fix](../assets/fix.svg) Infrastructure scalability and performance improvements.

### March 2023

**Release date**: March 28, 2023
<!-- v1.6 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added swatches to the [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) query.
![New](../assets/new.svg) Added the ability to get `entityId` using [API Mesh](mesh.md).

**Release date**: March 6, 2023
<!-- v1.5 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL functionality.
![Fix](../assets/fix.svg) Improved performance and API scalability.

### February 2023

**Release date**: February 7, 2023
<!-- v1.4 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Published catalog-service metapackage to simplify installation steps.
![Fix](../assets/fix.svg) API scalability and performance improvements.

### January 2023

**Release date**: January 17, 2023
<!-- v1.3 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Simplified and improved the onboarding experience.
![New](../assets/new.svg) New customer sandbox endpoints are available for pre-production testing.
![New](../assets/new.svg) Support added for virtual products.
![Fix](../assets/fix.svg) API scalability and performance improvements.

### November 2022

**Release date**: November 18, 2022
<!-- v1.1 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Catalog Service now supports Adobe's [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/).
![Fix](../assets/fix.svg) Improved API scalability and overall performance.

### October 2022

**Release date**: October 4, 2022
<!-- v1.0 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Support for bundled and grouped products.
![New](../assets/new.svg) Added B2B visibility overrides. Products are now searchable and can be added to the cart for specific customer groups.
![Fix](../assets/fix.svg) Service is now more stable and has improved performance.

### September 2022

**Release date**: September 12, 2022
<!-- v0.3 -->

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Variant images: product images returned based on selected options.
![New](../assets/new.svg) Price roles: only members of specific customer groups can see product prices.
![Fix](../assets/fix.svg) Improved stability and performance of the service.
![New](../assets/new.svg) Updates are received when products are deleted from the catalog.

### August 2022

**Release date**: August 9, 2022
<!-- Beta -->

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

- For Adobe Commerce on cloud or on premises, Adobe recommends using Composer to upgrade the Catalog Service metapackage in your cloud environments the latest release.

### v3.4.0 release

**Release date**: June 8, 2026

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) **Support for data feed sync status monitoring**—Updated the Catalog Service metapackage dependencies to include the Data Exporter Status extension (`magento/module-data-exporter-status`). This enables [data feed sync status monitoring](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) from the Commerce Admin without requiring any additional installation or configuration steps

![New](../assets/new.svg) Updated dependencies to maintain compatibility between the Catalog Service and your Commerce stack.

### v3.3.0 release

**Release date**: October 14, 2025

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) **Data Services upgrade**—`magento/data-services` dependency updated to ^8.0.0. Verify environment and custom Data Services API usage for 8.x compatibility before upgrading.

![New](../assets/new.svg) Updated version and metadata for the 3.3.0 release.

### v3.2.0 release

**Release date**: April 12, 2024

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Version and metadata updated for 3.2.0. No other dependency changes.

### v3.1.0 release

**Release date**: January 26, 2024

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added new package dependencies:

- **Category permission data exporter** (`magento/module-category-permission-data-exporter`) for exporting category permission data used by the catalog service.
- **Catalog Sync Admin** `magento/module-catalog-sync-admin` for Admin UI and configuration related to catalog sync.

![New](../assets/new.svg) Updated version and metadata for the 3.1.0 release.

## Catalog Service Installer

The installer is delivered with the Catalog Service extension and handles installation and environment checks so the Catalog Service matches your Commerce stack.

- For **Adobe Commerce as a Cloud Service** customers, the latest installer version is installed in your environment.

- For **Adobe Commerce on cloud infrastructure** or **on premises**, keep the installer aligned with the [Catalog Service metapackage](#catalog-service-metapackage).

Whenever you use Composer to upgrade the `magento/catalog-service`, the installer package is automatically updated to the latest version. You can also use Composer to upgrade  `magento/catalog-service-installer` separately when these release notes describe a change you need, for example, support for a new PHP version. That way your installation tooling stays compatible with the Catalog Service version you run.

### v1.0.6 release

**Release date**: March 25, 2026

![New](../assets/new.svg) **PHP 8.5**—Ensures compatibility when Catalog Service operates on PHP 8.5.

## Related documentation

- For projects deployed on **Adobe Commerce on cloud, on premises, or Adobe Commerce as a Cloud Service, see the following documentation:

  - [Catalog Service Guide](overview.md)
  - [Catalog Service GraphQL API Reference](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
  - [Adobe Commerce Admin Guide](https://experienceleague.adobe.com/en/docs/commerce-admin/)
  - [Adobe Commerce as a Cloud Service Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
  - [Adobe Commerce on Cloud Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- For projects using **Adobe Commerce Optimizer** or **Adobe Commerce Optimizer Connector**, see the following documentation:

  - [Merchandising Services Developer Guide](https://developer.adobe.com/commerce/services/optimizer/)
  - [Merchandising GraphQL API Reference](https://developer.adobe.com/commerce/services/reference/graphql/)
  - [Adobe Commerce Optimizer Guide](../optimizer/overview.md)
