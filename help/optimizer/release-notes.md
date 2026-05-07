---
title: Adobe Commerce Optimizer Release Notes
description: Monthly release information for [!DNL Adobe Commerce Optimizer], including updates to the data ingestion REST API, GraphQL API for to retrieve storefront catalog data.
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
---
# Release Notes

The following release notes contain updates to [!DNL Adobe Commerce Optimizer] including:

* New features and improvements to the [Adobe Commerce Optimizer Admin  interface](overview.md#quick-tour).
* Updates to the [data ingestion REST API](https://developer.adobe.com/commerce/services/reference/rest/) and [GraphQL API for storefront catalog data retrieval](https://developer.adobe.com/commerce/services/reference/graphql/).

  {{aco-api-updates-and-dropins}}

## May 2026

>[!BEGINSHADEBOX]

No current standalone product or Admin release notes for [!DNL Adobe Commerce Optimizer].

### API updates

**Release date**: May 4, 2026

<!--v1.53-->

Storefront product prices now display the correct currency code (for example., USD) for all product types. Previously, some products showed `NONE` instead of the expected currency, resulting in missing prices. This update ensures consistent and accurate price rendering across the storefront.

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## April 2026

**Release date**: April 7, 2026

>[!BEGINSHADEBOX]

### Catalog rules (beta)

[Category rules](./merchandising/rules/add.md) extend merchandising rules so you can target categories and control product order on category pages with the same ranking and actions (pin, boost, bury) as search.

### Price filter (beta)

Recommendation filters now include a [price range filter](./merchandising/recommendations/filters.md#price) (minimum and maximum).

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

**Release date**: April 29, 2026

<!--v1.52 release-->

**Request batching required** — Enforced limit of maximum 100 SKUs per request when retrieving catalog data using the GraphQL API as per [documented limits and boundaries](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits#product-discovery).

<!--DATA-7156-->

**Release date**: April 17, 2026

<!--v1.51 release-->

**Find categories by name with GraphQL** — The new [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) query returns matching categories with pagination for storefronts and integrations. See the API reference for parameters and response fields. <!--COMOPT-1819-->

**Release date**: April 7, 2026

<!--v1.50 release-->

**Simpler category lookups** — The [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) query treats `family` as optional, so you can resolve categories by slug without supplying a family.

{{aco-release}}

>[!ENDSHADEBOX]

## March 2026

>[!BEGINSHADEBOX]

[!DNL Adobe Commerce Optimizer] had no standalone product or Admin release notes this month.

### API updates

**Release date**: March 24, 2026

Added support to compute and return the price range for dynamic bundles. <!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## February 2026

**Release date**: February 19, 2026

>[!BEGINSHADEBOX]

### Catalog view for merchandising rules and recommendations (beta)

You can now specify a catalog view when you [create recommendation units](./merchandising/recommendations/create.md) or [merchandising rules](./merchandising/rules/add.md).

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

* **Release date**: February 19, 2026

<!--V1.48-->

  **Richer category content for storefronts** — The [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) query now returns descriptions, images, and SEO meta tags so storefronts can render richer category pages.

  <!--DATA-6933-->

* **Release date**: February 12, 2026

   <!--1.49-->

  **Enhanced product data by category** — The GraphQL API adds the [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} type so you can query and filter products by category with fewer round trips.

{{aco-release}}

>[!ENDSHADEBOX]

## January 2026

>[!BEGINSHADEBOX]

[!DNL Adobe Commerce Optimizer] had no standalone product or Admin release notes this month.

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

**Release date**: January 19, 2026

* **Richer categories support with the REST API** — When using the [Categories API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories), you can now include optional `metaTags`, `images`, and `description` values in addition to `families` to provide more detailed and visually engaging information for product categories. [Categories operations](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) now support optional `metaTags`, `images`, and `description` fields.

{{aco-release}}

>[!ENDSHADEBOX]

## December 2025

**Release date**: December 10, 2025

>[!BEGINSHADEBOX]

### Opportunities

Merchandisers can now get AI-powered recommendations through [Adobe Sites Optimizer](./manage-results/opportunities.md) to detect site issues and suggest performance fixes.

### Catalog layers

Merchandisers can now use [Catalog layers](./setup/catalog-layer.md) to overlay product data without editing the source catalog, manage layer priority, and use Adobe Sites Optimizer auto-fix.

{{aco-release}}

>[!ENDSHADEBOX]

## November 2025

>[!BEGINSHADEBOX]

[!DNL Adobe Commerce Optimizer] had no standalone product or Admin release notes this month.

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

* **Release date**: November 21, 2025

  **Updated authentication instructions for the data ingestion REST API** — Authentication instructions have been updated to reference OAuth access tokens and the correct Developer Console credential scopes when calling the data ingestion service. If your credential scopes are outdated, regenerate your credentials to ensure continued access.

* **Release date**: November 3, 2025

  <!-- v1.43 -->

  **Layered, localized product content in GraphQL** — Added support for channel-specific, locale-aware content delivery for Adobe Commerce Optimizer implementations.
  * Tailor product content by customer segment
  * Apply locale-specific overrides without duplicating base catalog data
  * Control field-level overrides with Layer Masks
  * Support for premium, seasonal, and mobile-optimized content layers

   No GraphQL API schema change: layers apply through the existing `products` query and request headers. See [Catalog layer](./setup/catalog-layer.md).

{{aco-release}}

>[!ENDSHADEBOX]

## October 2025

**Release date**: October 14, 2025

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

The [!DNL Commerce Optimizer Salesforce Commerce Connector] is a new App Builder starter kit that syncs Salesforce B2C Commerce catalog data into [!DNL Commerce Optimizer].<!--COMOPT-536-->

**For Admins:**

* Salesforce catalog changes (products, prices, metadata, price books) sync to Commerce Optimizer automatically.
* Runs outside Adobe Commerce for fewer integration touch points.
* Scheduled updates keep Optimizer data current for merchandising and recommendations.

**For Developers:**

* Extensible framework for ingesting Salesforce catalog into SaaS Merchandising Services.
* Reference implementations, design docs, and code samples for faster builds and troubleshooting.<!--COMOPT-536-->

### Layered search

* **Layered search (GA)** — Product search now supports `startsWith` and `contains` matching. [Learn more](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

* **Release date**: October 17, 2025

  **Add REST API support to ingest product layers** — Use the [Catalog layers API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) to customize and override base product data for specific contexts, locales, or business requirements. Once you have created layers, you can apply and manage them from [Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->

* **Release date**: October 14, 2025

  **Programmatic category trees** — Create, update, and manage category trees for navigation and grouping via REST (global or channel-specific), at scale—up to 10,000 trees and 500 categories per tree. See [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} in the _Catalog data ingestion REST API Reference_.<!--DCAT-2649-->

* **Release date**: October 8, 2025

  **Improved instructions for category mapping in data ingestion API** — Improved guidelines for category slug format and hierarchy rules, and clarified that product `routes.path` values must match an existing category slug (for example, `men/clothing`). These updates help ensure accurate category mapping and smoother data integration.

{{aco-release}}

>[!ENDSHADEBOX]

## September 2025

>[!BEGINSHADEBOX]

[!DNL Adobe Commerce Optimizer] had no standalone product or Admin release notes this month.

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

**Release date**: September 23, 2025

* **Manage categories using the REST API** — Use the [Categories API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) to create and manage categories. Categories organize products into logical groups and support nested hierarchies using slug-based paths. After you create and assign them to products, you can use the GraphQL API to retrieve category data to render storefront menus and manage hierarchical category trees using the GraphQL `navigation` and `categoryTree` queries.<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## August 2025

**Release date**: August 28, 2025

>[!BEGINSHADEBOX]

### EU region now available

EU production region (**eu1**) is available for IMS organizations. When you [add a Commerce Optimizer instance](./get-started.md#step-1-create-an-instance) in Cloud Manager, choose **[!UICONTROL European Union]** as the **[!UICONTROL Region]** (production only).

The base production URLs for the European Union region are:

* Admin: `https://eu1.admin.commerce.adobe.com`
* REST and GraphQL: `https://eu1.api.commerce.adobe.com`

![Cloud Manager create instance dialog with Region field](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
