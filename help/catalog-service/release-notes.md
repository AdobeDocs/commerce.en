---
title: '[!DNL Catalog Service] Release Notes'
description: The latest release information for [!DNL Catalog Service] for Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
---
# [!DNL Catalog Service] Release Notes

These release notes describe the latest versions of the hosted [!DNL Catalog Service] and the Catalog Service PHP extension.
Support is provided for the current released version. Release notes for older versions are provided for reference.
Updates include:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues

## Catalog service releases

These release notes cover updates to the Catalog Service for the last six months, including:

- Enhancements to the Catalog Service API schema, enabling new capabilities and improved catalog data retrieval.
- System-level and infrastructure improvements that boost overall performance, reliability, and stability. While there are no direct changes to user-facing functionality, these updates provide a smoother and more robust service experience.

### v1.8.29

_January 29, 2026_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6871, DATA-6872-->

![Fix](../assets/fix.svg) <!--DATA-6924-->Fixed an issue where linked products in the API response were missing images and price range information. All linked `ComplexProductView` entries now correctly include images and price ranges.

### v1.8.28

_December 4, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6852, DATA-6864-->

### v1.8.27

_November 11, 2025_

![New](../assets/new.svg) **Attribute Filtering by Name**–GraphQL queries now support filtering product attributes by name for both simple and complex product views. <!--DATA-6823--> This update enables more efficient queries and streamlined responses:

- Reduce response payload size by requesting only specific attributes
- Combine with the existing `roles` filter to narrow by visibility role and attribute name
- Examples below illustrate usage

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

### v1.8.26

_November 6, 2025_

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6852, DATA-6864-->

### v1.8.25

_November 3, 2025_

![New](../assets/new.svg) **Product Layers for multi-dimensional product customization**—Added support for channel-specific, locale-aware content delivery for Adobe Commerce Optimizer implementations.<!--DATA-6823-->

- Serve different product content to different customer segments
- Apply locale-specific customizations without duplicating base data
- Control field-level overrides with Layer Masks
- Support for premium, seasonal, and mobile-optimized content layers

  After layers are defined, they are retrieved via the existing `products` query. The layers functionality is transparently integrated into the existing GraphQL API. No schema changes are required - layers are applied server-side based on request headers.

  For details on implementing product layers, see [Catalog layer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-layer) in the _Adobe Commerce Optimizer Guide_.


![Fix](../assets/fix.svg) Fixed an issue where querying grouped products caused an error when the parent product did not have pricing configured. Child products in these grouped configurations now correctly return their own visibility roles when the parent lacks price data.<!--DATA-6779-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance performance and stability. <!--DATA-6721, DATA-6864-->

### v1.8.21

_September 12, 2025_

This update includes system-level and infrastructure improvements to enhance performance and stability.<!--DATA-6717-->


### v1.8.20

_September 9, 2025_

![Fix](../assets/fix.svg) **Tier prices filtered by minimum final price** <!--DATA-6643-->

Tier prices returned by the API are now filtered so that only tiers whose discounted price is **lower than** the product's minimum final price are included. Tiers with a price greater than or equal to the minimum final price are omitted because they would never be displayed on the storefront; the minimum final price would apply instead.

This applies to:

- **Simple products**: `price.tiers` only includes tiers with `tier.amount.value` &lt; `price.final.amount.value` (minimum final).
- **Complex products**: `priceRange.minimum.tiers` and `priceRange.maximum.tiers` use the same rule when building the price range.

### v1.8.16

_September 1, 2025_

![New](../assets/new.svg) **Added Tier Pricing support** to query volume pricing:<!--DATA-6643-->

To retrieve tier pricing information for products, follow these steps:

1. Use the `products` query with your desired SKUs
2. For **SimpleProductView**, access `price.tiers`
3. For **ComplexProductView**, access `priceRange.minimum.tiers` and `priceRange.maximum.tiers`
4. Each tier contains the discounted `tier` price and `quantity` conditions
5. Define quantity thresholds with `gte` (minimum, inclusive) and `lt` (maximum, exclusive)

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

### v1.8.15

_July 28, 2025_

This update includes system-level and infrastructure improvements to enhance performance and stability.<!--DATA-6316-->

### v1.8.14

_July 24, 2025_

![New](../assets/new.svg) **Compute priceHierarchical price book configuration**—Added support for hierarchical price books in price range calculations.

- When multiple price books are configured with parent-child relationships, the API now correctly computes price ranges by considering the hierarchy and inheritance of price rules.
- This enhancement allows for more accurate pricing information to be returned based on complex price book setups.
- Only supported for Adobe Commerce Optimizer deployments. For details, see [Price Books](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![New](../assets/new.svg) **Multi-select product options**–The GraphQL API now exposes whether a product option allows multiple selections. This applies to options on bundle and grouped products (for example, "choose multiple items" in a bundle).

- Use the `multi` field on `ProductViewOption` to know if the option allows multiple choices.
- When `multi` is `true`, the storefront can allow customers to select more than one value; when `false`, only a single value can be selected.

- **Example:**

  ```graphql
  query {
    products(skus: ["MY-BUNDLE-SKU"]) {
      ... on ComplexProductView {
        options {
          id
          title
          required
          multi
          values {
            id
            title
          }
        }
      }
    }
  }
  ```

![New](../assets/new.svg) **Case insensitive keys**—Added support for case-insensitive key lookups in queries. This enhancement allows clients to retrieve data without worrying about the exact casing of keys, improving usability and reducing errors. <!--DATA-6494, DCAT-2495-->

![Fix](../assets/fix.svg) **Improve error handling for missing price information**—If a price has not been received yet, the API returns `null` for the price field instead of throwing an error. This change allows clients to handle missing price data more gracefully.<!--DATA-6541-->

![Fix](../assets/fix.svg) System-level and infrastructure improvements to enhance security, performance, and stability. <!--DATA-6316,DATA-6511,-DATA-6511,DATA-6511-->

## Catalog Service extension

This section describes updates to the Catalog Service PHP metapackage (`magento/catalog-service`).

### v3.3.0

_October 14, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) **Data Services upgrade**—Updated the dependency for `magento/data-services` to version ^8.0.0.
This is a major version upgrade; verify that your environment and any custom code using Data Services APIs are compatible with 8.x before upgrading.

![New](../assets/new.svg) Updated version and metadata for the 3.3.0 release.

### v3.2.0

_April 12, 2024_

![New](../assets/new.svg) Updated version and metadata for the 3.2.0 release. No other other dependency changes included in this release.

### v3.1.0

_January 26, 2024_

![New](../assets/new.svg)  Added new package dependencies:

- **Category permission data exporter** (`magento/module-category-permission-data-exporter`) for exporting category permission data used by the catalog service.
- **Catalog Sync Admin** `magento/module-catalog-sync-admin` for Admin UI and configuration related to catalog sync.

![New](../assets/new.svg) Updated version and metadata for the 3.1.0 release.
