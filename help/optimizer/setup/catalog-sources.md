---
title: Catalog sources
description: Learn what catalog sources are and how they define the authoritative scope of products, attributes, and categories for search, filter, and sort behavior.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Catalog sources

Catalog sources represent authoritative scopes of products, attributes, and categories. They typically map to language, audience, or system-of-origin boundaries and determine search, filter, and sort behavior.

## Catalog sources versus related concepts

Understanding how catalog sources relate to other [!DNL Adobe Commerce Optimizer] concepts helps you model your data correctly:

* **Catalog source** - The underlying data context that supplies product information. A catalog source is typically a locale (for example, `en-US`, `fr-CA`) or an external system such as a PIM or ERP. Products, attributes metadata, and categories are all scoped per catalog source. Think of a catalog source as *where* the raw catalog data comes from and *how* it affects product discovery (search results, filtering, and sorting behavior).

* **[Catalog view](catalog-view.md)** - A configured view of your catalog for a specific business need. When you create a catalog view, you select which catalog source (or locale) to use, then add [policies](policies.md) to filter which products are visible and link [price books](pricebooks.md) to control pricing. A single catalog source can power many catalog views (for example, one `en-US` source with separate catalog views for different brands or regions). Think of a catalog view as *how* you expose that data to a storefront, channel, or audience.

* **[Catalog layer](catalog-layer.md)** - A layer applied on top of base catalog data to modify product attributes (name, description, images, metadata) without changing the source data. Use catalog layers when differences must affect storefront display only - not product discovery.

## Rules and limitations

* Each catalog source is created by ingesting a product via the Data Ingestion API. See [Developer Docs - Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) for more information.
* Product uniqueness is determined by SKU + catalog source.
* Shoppers do not access catalog sources directly. Catalog data is exposed to the storefront via [catalog views](catalog-view.md).

## Modeling guidance

Use the following guidance when deciding how to structure your catalog sources:

* Create a separate catalog source for each catalog language.
* Use separate catalog sources when product and attribute differences must affect search, filtering, or sorting behavior (for example, different searchability, filterability, or facet configuration for the same attribute).
* Use [catalog layers](catalog-layer.md) when product and attribute differences must affect storefront display only, not product discovery.

>[!MORELIKETHIS]
>
> * [Catalog views](catalog-view.md) - Configure filtered, priced views on top of a catalog source
> * [Catalog layers](catalog-layer.md) - Modify product presentation without changing source data
> * [Policies](policies.md) - Create attribute-based filters for catalog views
> * [Price books](pricebooks.md) - Manage pricing structures for different customer segments
