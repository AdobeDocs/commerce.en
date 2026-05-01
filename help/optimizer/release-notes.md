---
title: Adobe Commerce Optimizer Release Notes
description: The latest release information for the [!DNL Adobe Commerce Optimizer].
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
---
# Release Notes

The following release notes contain updates to [!DNL Adobe Commerce Optimizer].

## April 2026

**Release date**: April 7, 2026

>[!BEGINSHADEBOX]

### Catalog rules (beta)

[Category rules](./merchandising/rules/add.md) extend merchandising rules so you can target categories and control product order on category pages with the same ranking and actions (pin, boost, bury) as search.

### Price filter (beta)

Recommendation filters now include a [price range filter](./merchandising/recommendations/filters.md#price) (minimum and maximum).

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

{{aco-api-updates-and-dropins}}

#### April 29, 2026

<!--v1.52 release-->

![New](../assets/new.svg) **Request batching required** — Enforced limit of maximum 100 SKUs per request as per [documented limits and boundaries](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits). <!--DATA-7156-->

#### April 17, 2026

<!--v1.51 release-->

![New](../assets/new.svg) **Find categories by name with GraphQL** — The new [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) query returns matching categories with pagination for storefronts and integrations. See the API reference for parameters and response fields. <!--COMOPT-1819-->


#### April 7, 2026

<!--v1.50 release-->

![New](../assets/new.svg) **Simpler category lookups** — The [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) query treats `family` as optional, so you can resolve categories by slug without supplying a family.

{{aco-release}}

>[!ENDSHADEBOX]

## February 2026

**Release date**: February 19, 2026

>[!BEGINSHADEBOX]

### Catalog view for merchandising rules and recommendations (beta)

You can now specify a catalog view when you [create recommendation units](./merchandising/recommendations/create.md) or [merchandising rules](./merchandising/rules/add.md).

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

{{#aco-api-updates-and-dropins}}

#### February 19, 2026

<!--V1.48-->

![New](../assets/new.svg) **Richer category content for storefronts** — The [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) query now returns descriptions, images, and SEO meta tags so storefronts can render richer category pages.<!--DATA-6933-->

#### February 12, 2026

<!--1.49-->

![New](../assets/new.svg) **Enhanced product data by category** — The GraphQL API adds the [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} type so you can query and filter products by category with fewer round trips.

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

**Release date**: November 3, 2025

>[!BEGINSHADEBOX]

[!DNL Adobe Commerce Optimizer] had no standalone product or Admin release notes this month.

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

{{aco-api-updates-and-dropins}}

#### November 3, 2025

<!-- v1.43 -->

![New](../assets/new.svg) **Layered, localized product content in GraphQL** — Added support for channel-specific, locale-aware content delivery for Adobe Commerce Optimizer implementations.<!--DATA-6632-->

* Tailor product content by customer segment
* Apply locale-specific overrides without duplicating base catalog data
* Control field-level overrides with Layer Masks
* Support for premium, seasonal, and mobile-optimized content layers

No schema change: layers apply through the existing `products` query and request headers. See [Catalog layer](./setup/catalog-layer.md).

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

### Layered Search

* **Layered search (GA)** — Product search now supports `startsWith` and `contains` matching. [Learn more](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.
{{#aco-api-updates-and-dropins}}

#### October 14, 2025

* **Programmatic category trees** — Create, update, and manage category trees for navigation and grouping via REST (global or channel-specific), at scale—up to 10,000 trees and 500 categories per tree. See [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} in the _Catalog data ingestion REST API Reference_.<!--DCAT-2649-->

{{aco-release}}

>[!ENDSHADEBOX]

## August 2025

**Release date**: August 28, 2025

>[!BEGINSHADEBOX]

### EU region now available

EU production region (**eu1**) is available for IMS organizations. When you [add a Commerce Optimizer instance](./get-started.md#step-1-create-an-instance) in Cloud Manager, choose **European Union** as the **Region** (production only).

The base production URLs for the European Union region are:

* Admin: `https://eu1.admin.commerce.adobe.com`
* REST and GraphQL: `https://eu1.api.commerce.adobe.com`

![create instance](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
