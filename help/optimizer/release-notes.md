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

Merchandising rules now include [category rules](./merchandising/rules/add.md), so you can target one or more categories and control product order on category pages using the same intelligent ranking and manual actions (pin, boost, bury) as for search.

### Price filter (beta)

Recommendation filters now support a [price filter](./merchandising/recommendations/filters.md#price) that you can use to set a minimum and maximum price range for products.

{{aco-release}}

>[!ENDSHADEBOX]

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

>[!NOTE]
>
>[Drop-in components](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/) for [!DNL Commerce Storefront on Edge Delivery Services] are updated to incorporate the latest GraphQL API implementation, so the standard storefront integration reflects new fields, limits, and query behavior automatically.

#### April 29, 2026 <!--v1.52 release-->

![New](../assets/new.svg) **Request batching required** — Enforced limit of maximum 100 SKUs per request as per [documented limits and boundaries](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits). <!--DATA-7156-->

#### April 17, 2026 <!--v1.51 release-->

![New](../assets/new.svg) **Find categories by name with GraphQL** — Added a new `[searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/)` GraphQL query that enables clients to search categories by name with paginated results. The query accepts a required `searchTerm` (minimum 3 characters) and optional `family`, `pageSize`, and `currentPage` parameters. Results include matching `CategoryTreeView` objects with full category metadata, a `totalCount`, and `pageInfo` for pagination. <!--COMOPT-1819-->


#### April 7, 2026 <!--v1.50 release-->

![New](../assets/new.svg) **Simpler category lookups** — The [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) GraphQL query now has the family input parameter as optional. This allows for a more flexible category retrieval by allowing access via slug without dependency on a specific family parameter.

## February 2026

**Release date**: February 19, 2026

>[!BEGINSHADEBOX]

### Catalog view for merchandising rules and recommendations (beta)

Added ability to specify a catalog view when you [create recommendation units](./merchandising/recommendations/create.md) or [merchandising rules](./merchandising/rules/add.md).

{{aco-release}}

>[!ENDSHADEBOX]

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

{{#aco-api-updates-and-dropins}}

#### February 19, 2026

![New](../assets/new.svg) **Richer category content for storefronts** — The `[categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree)` GraphQL query now returns category descriptions, images, and SEO meta tags. This update delivers the data that storefront developers need to display category imagery and improve search engine optimization with proper meta titles, descriptions, and keywords.<!--DATA-6933-->

#### February 12, 2026

![New](../assets/new.svg) **Enhanced product data by category** — The GraphQL API now supports the `[CategoryProductView](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"}` type, enabling enhanced views and queries for products by category. This update allows developers to efficiently retrieve and filter product data based on category, improving flexibility and performance for category-driven use cases.

## December 2025

**Release date**: December 10, 2025

>[!BEGINSHADEBOX]

### Opportunities

AI-powered site optimization recommendations are now available through [Adobe Sites Optimizer integration](./manage-results/opportunities.md). This feature helps merchandisers identify and address issues impacting commerce site performance through automated detection and intelligent recommendations.

### Catalog layers

Added [catalog layers](./setup/catalog-layer.md) so you can modify product data without changing source data, including layer priority management and integration with Adobe Sites Optimizer auto-fix features.

{{aco-release}}

>[!ENDSHADEBOX]

## November 2025

[!DNL Adobe Commerce Optimizer] had no standalone product or Admin release notes this month. The following Storefront Catalog Service API updates apply to [!DNL Adobe Commerce Optimizer] and [!DNL Adobe Commerce as a Cloud Service].

### API updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services.

{{#aco-api-updates-and-dropins}}

#### November 3, 2025

![New](../assets/new.svg) **Layered, localized product content in GraphQL** — Added support for channel-specific, locale-aware content delivery for Adobe Commerce Optimizer implementations.<!--DATA-6632-->

* Serve different product content to different customer segments
* Apply locale-specific customizations without duplicating base data
* Control field-level overrides with Layer Masks
* Support for premium, seasonal, and mobile-optimized content layers

Layers are retrieved using the existing `products` query, are applied server-side from request headers, and require no schema changes. See [Catalog layer](./setup/catalog-layer.md) in the _Adobe Commerce Optimizer Guide_.

## October 2025

**Release date**: October 14, 2025

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

The [!DNL Commerce Optimizer Salesforce Commerce Connector] is a new App Builder integration starter kit that enables Commerce administrators and developers to seamlessly connect Salesforce B2C Commerce catalog data with [!DNL Commerce Optimizer].<!--COMOPT-536-->

**For Admins:**

* Catalog updates in Salesforce (products, prices, metadata, pricebooks) are automatically synchronized with Commerce Optimizer—no manual intervention required.
* The integration operates independently from Adobe Commerce, reducing complexity and potential points of failure.
* Admins can rely on scheduled regular updates to ensure accurate catalog data within Commerce Optimizer, improving merchandising and product recommendations.

**For Developers:**

* The starter kit provides a streamlined, extensible framework for ingesting Salesforce catalog data into SaaS Merchandising Services.
* Reference implementations, design documentation, and code samples are available to accelerate custom integrations or troubleshooting.<!--COMOPT-536-->

### Layered Search

* GA release for the following advanced search capabilities: layered search using `startsWith` and `contains`. [Learn more](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### API Updates

The following API updates were released to support Adobe Commerce Optimizer Merchandising Services. The detail below matters most if you use [!DNL Adobe Commerce Optimizer] with a headless storefront or retrieve catalog data directly through the Storefront Catalog Service GraphQL API.

{{#aco-api-updates-and-dropins}}

#### October 14, 2025

* **Programmatic category trees** — Administrators and developers can programmatically create, update, and manage multiple category trees for navigation and product grouping through REST API. The API supports both global and channel-specific configurations and is designed for high scalability, supporting up to 10,000 category trees and 500 categories per tree. For details, see [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} in the _Catalog data ingestion REST API Reference_.<!--DCAT-2649-->

{{aco-release}}

>[!ENDSHADEBOX]

## August 2025

**Release date**: August 28, 2025

>[!BEGINSHADEBOX]

### EU region now available

European Union region (eu1) support for customer IMS organizations is now available. You can now select **European Union** as a **Region** when [adding a Commerce Optimizer instance](./get-started.md#step-1-create-an-instance) in the Cloud Manager. The European Union region is only available for production environments.

The base production URLs for the European Union region are:

* Admin: `https://eu1.admin.commerce.adobe.com`
* REST and GraphQL: `https://eu1.api.commerce.adobe.com`

![create instance](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
