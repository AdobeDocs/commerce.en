---
title: Boundaries and Limits
description: Learn about the boundaries and limits for [!DNL Product Recommendations] to ensure it meets the needs of your business.
role: Admin, Developer
---
# Boundaries and limits

Review the following boundaries and limits to ensure that [!DNL Product Recommendations] meets the needs of your business. Understanding these constraints helps you plan implementation, configure filters, and avoid common issues.

## General

- **Product types** - Supported product types include _simple_, _configurable_, _virtual_, _downloadable_, and _gift card_. _Bundle_, _grouped_, and custom product types are not supported. If your catalog contains a large number of unsupported product types, you can expect a low [readiness score](create.md#readiness-indicators). See [Filter by product type](filters.md#type).
- **SKUs with spaces** - SKUs that contain spaces can reduce recommendation relevancy and should be avoided when possible.
- **Cart page** - Product Recommendations are not supported on the Cart page when your store is configured to [display the shopping cart page immediately after adding a product to the cart](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration). See [Create recommendations](create.md).
- **Child products** - Child products of a configurable product (visibility _Not Visible Individually_) are not displayed in a recommendation unit. Only the configurable (parent) product can appear. See [Filter products](filters.md#product).
- **Disabled or non-visible products** - Products that are disabled or not visible individually can never appear in recommendations and cannot be selected in product filters.
- **Special pricing** - [Special prices](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) with start and end dates are not supported in recommendation units. A product with a special price can appear in recommendations, but the unit does not display the special price, the start date, or the end date. Shoppers see the regular price (or other price data provided by your catalog/price feed) until they open the product page.

## Recommendation units

- **Active units per page type** - You can create up to 50 active recommendation units for each page type (Home, Category, Product Detail, Cart, Confirmation). The page type is grayed out in the create flow when the limit is reached.
- **Products per unit** - The number of products displayed in a recommendation unit can be set from 5 (default) to a maximum of 20.
- **Draft state** - After saving a recommendation as draft, you cannot modify the page type or recommendation type for that unit. Other settings can be edited before activation.

## Filters and conditions

- **Dynamic conditions** - Dynamic conditions (such as "products in same category as current product" or "relative price range") are available on every page type except the Home page. They are also not available on pages where recommendations are placed with Page Builder. See [Conditions](filters.md#conditions).

## Preview and non-production environments

- **Recently viewed preview** - The _Recently viewed_ recommendation type cannot be previewed in the Admin because the data is based on browser history and is not available in the Admin context. See [Preview recommendations](create.md#preview).
- **Recommendations from another data space** - When you [fetch recommendations from a different SaaS data space](settings.md) (for example, production) in a non-production storefront, you can view the recommendations but cannot click through to product pages from them. This is by design for preview and testing.
- **GraphQL and alternate data space** - When using Product Recommendations via [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/), the `alternateEnvironmentId` parameter (used to fetch recommendations from another data space) is not available. Use the REST API or the Admin Settings to switch the recommendations source in non-production.

## API and configuration

- **API keys (4.x and higher)** - You must provide public and private API keys for both sandbox and production environments. If you do not provide both pairs of API keys, you cannot access the Product Recommendations feature in the Admin. Data collection on your storefront and existing recommendations continue to work. See [Install and configure](install-configure.md).

## Cookie restrictions

- When [cookie restriction mode](setting-cookie.md) is enabled and shoppers have not accepted cookies, certain recommendation types that rely on behavioral data may not display or may show limited results.
- Recommendation types that do not rely on behavioral data (for example, _Most viewed_, _Visual similarity_) continue to work when cookie restrictions are enabled.
- When cookie restrictions are enabled, Product Recommendations does not collect or store behavioral data in cookies or local storage until the shopper consents.

## Page Builder

- **Metrics and store views** - Metrics for Page Builder recommendation units appear only on the default store view in the Product Recommendations workspace. To see Page Builder recommendation metrics on a non-default store view, you must open and [edit](edit.md) the Page Builder recommendation unit in that store view and save it; the metrics then appear for that store view. See [Page Builder integration](page-builder.md).

## B2B

- Product Recommendations honors [category permissions](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html), [shared catalogs](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html), and customer group-specific pricing. Shoppers see only recommendations for products they can access according to their segment and catalog assignment. See [Onboarding](onboarding.md).

## Data and readiness

- **Behavioral data** - Many recommendation types require sufficient storefront behavioral data (views, add-to-cart, purchases). New stores or low-traffic stores may see limited or no results for those types until adequate data is collected. Monitor [readiness indicators](create.md#readiness-indicators) in the Admin.
- **Staging without production data** - In a non-production environment without behavioral data, the only recommendation type you can test without fetching from production is _More like this_, which uses catalog-based similarity only. See [Staging environment](staging-environment.md).

## Troubleshooting

For help with catalog sync, recommendations not displaying, or other common issues, search the [Commerce Knowledge Base](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) or contact [support](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
