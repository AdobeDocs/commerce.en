---
title: Adobe Commerce Optimizer Release Notes
description: Monthly release information for [!DNL Adobe Commerce Optimizer], including updates to the data ingestion REST API and GraphQL API for storefront catalog data retrieval.
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Release notes

The following release notes contain updates to [!DNL Adobe Commerce Optimizer], including:

* New features and improvements to [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour).
* Updates to the [data ingestion REST API](https://developer.adobe.com/commerce/services/reference/rest/) and [GraphQL API for storefront catalog data retrieval](https://developer.adobe.com/commerce/services/reference/graphql/).

  {{aco-api-updates-and-dropins}}

## May 2026

Currently, there are no [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) releases this month. See API updates below.

>[!BEGINSHADEBOX]

### API updates

_May TBD, 2026_

<!-- v1.2 -->

![Fix](../assets/fix.svg) Tagged descendant categories are now correctly included in family-filtered `navigation` trees when an untagged intermediate node exists in the path.
<!--DATA-7183-->

![Fix](../assets/fix.svg) Empty string slug values in the `categoryTree` query are now gracefully ignored.
<!--DATA-7184-->

![Fix](../assets/fix.svg)   Search results are now sorted alphabetically without case sensitivity, ensuring consistent and predictable ordering. Categories with shorter prefixes appear first when names are otherwise identical.
<!--DATA-2066-->

_May 4, 2026_

<!--v1.53-->

Storefront product prices now display the correct currency code (for example, USD) for all product types. Previously, some products showed `NONE` instead of the expected currency, resulting in missing prices.

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

_April 29, 2026_

<!--v1.52 release-->

**Request batching required** — The GraphQL API now enforces a maximum of 100 SKUs per request when you retrieve catalog data. See [documented limits and boundaries](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits#product-discovery).

<!--DATA-7156-->

_April 17, 2026_

<!--v1.51 release-->

**Find categories by name with GraphQL** — The new [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) query returns matching categories with pagination for storefronts and integrations. See the API reference for parameters and response fields. <!--COMOPT-1819-->

_April 7, 2026_

<!--v1.50 release-->

**Simpler category lookups** — The [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) query treats `family` as optional, so you can resolve categories by slug without supplying a family.

{{aco-release}}

>[!ENDSHADEBOX]

## March 2026

There were no [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) releases this month. See API updates below.

>[!BEGINSHADEBOX]

### API updates

_March 24, 2026_

Dynamic bundles now return a computed price range. <!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## February 2026

**Release date**: February 19, 2026

>[!BEGINSHADEBOX]

### Catalog view for merchandising rules and recommendations (beta)

You can now specify a catalog view when you [create recommendation units](./merchandising/recommendations/create.md) or [merchandising rules](./merchandising/rules/add.md).

### API updates

_February 19, 2026_

<!--v1.48-->

**Richer category content for storefronts** — The [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) query now returns descriptions, images, and SEO meta tags so storefronts can render richer category pages.<!--DATA-6933-->

_February 12, 2026_

<!--v1.49-->

**Enhanced product data by category** — The GraphQL API adds the [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} type so you can query and filter products by category with fewer round trips.

{{aco-release}}

>[!ENDSHADEBOX]

## January 2026

There were no [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) releases this month. See API updates below.

>[!BEGINSHADEBOX]

### API updates

_January 19, 2026_

* **Richer categories support with the REST API** — [Categories API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) operations now accept optional `metaTags`, `images`, and `description` values in addition to `families`, so you can provide richer merchandising and SEO detail for categories.

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

There were no [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) releases this month. See API updates below.

>[!BEGINSHADEBOX]

### API updates

_November 21, 2025_

**Updated authentication instructions for the data ingestion REST API** — The instructions now reference OAuth access tokens and the correct Developer Console credential scopes for the data ingestion service. If your credential scopes are outdated, regenerate them to keep access.

_November 3, 2025_

<!-- v1.43 -->

**Layered, localized product content in GraphQL** — You can now deliver channel-specific, locale-aware product content from [!DNL Adobe Commerce Optimizer].

* Tailor product content by customer segment
* Apply locale-specific overrides without duplicating base catalog data
* Control field-level overrides with Layer Masks
* Use premium, seasonal, and mobile-optimized content layers

No GraphQL API schema change: layers apply through the existing `products` query and request headers. See [Catalog layer](./setup/catalog-layer.md).

{{aco-release}}

>[!ENDSHADEBOX]

## October 2025

**Release date**: October 14, 2025

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

The [!DNL Commerce Optimizer Salesforce Commerce Connector] is a new App Builder starter kit that syncs Salesforce B2C Commerce catalog data into [!DNL Commerce Optimizer].<!--COMOPT-536-->

**For Admins:**

* Salesforce catalog changes (products, prices, metadata, price books) sync to [!DNL Commerce Optimizer] automatically.
* Runs outside [!DNL Adobe Commerce] for fewer integration touch points.
* Scheduled updates keep [!DNL Commerce Optimizer] data current for merchandising and recommendations.

**For Developers:**

* Extensible framework for ingesting Salesforce catalog into SaaS Merchandising Services.
* Reference implementations, design docs, and code samples for faster builds and troubleshooting.

### Layered search

* **Layered search (GA)** — Product search now supports `startsWith` and `contains` matching. See [Layered search and expanded search types](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### API updates

* _October 17, 2025_

  **Add REST API support to ingest product layers** — Use the [Catalog layers API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) to customize and override base product data for specific contexts, locales, or business requirements. After you create layers, you can apply and manage them from [Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->

* _October 14, 2025_

  **Programmatic category trees** — Create, update, and manage category trees for navigation and grouping via REST (global or channel-specific), at scale—up to 10,000 trees and 500 categories per tree. See [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} in the _Catalog data ingestion REST API Reference_.<!--DCAT-2649-->

* _October 8, 2025_

  **Clearer category mapping for data ingestion** — New guidelines explain category slug format and hierarchy rules, and clarify that product `routes.path` values must match an existing category slug (for example, `men/clothing`).

{{aco-release}}

>[!ENDSHADEBOX]

## September 2025

There were no [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) releases this month. See API updates below.

>[!BEGINSHADEBOX]

### API updates

_September 23, 2025_

* **Manage categories using the REST API** — Use the [Categories API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) to create and manage categories. Categories organize products into logical groups and support nested hierarchies through slug-based paths. After you assign categories to products, retrieve them with the GraphQL `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)` and `[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)` queries to render storefront menus and category trees.<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## August 2025

**Release date**: August 28, 2025

>[!BEGINSHADEBOX]

### EU region now available

EU production region (**eu1**) is available for IMS organizations. When you [add a [!DNL Commerce Optimizer] instance](./get-started.md#step-1-create-an-instance) in Cloud Manager, choose **[!UICONTROL European Union]** as the **[!UICONTROL Region]** (production only).

The base production URLs for the European Union region are:

* Admin: `https://eu1.admin.commerce.adobe.com`
* REST and GraphQL: `https://eu1.api.commerce.adobe.com`

![Cloud Manager create instance dialog with Region field](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
