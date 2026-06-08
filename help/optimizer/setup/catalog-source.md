---
title: Catalog source
description: Learn what catalog sources are and how they define the authoritative scope of products, attributes, and categories for search, filter, and sort behavior.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
---

# Catalog source

A catalog source represents an authoritative scope of products, attributes, and categories. Catalog sources typically map to language, audience, or system-of-origin boundaries and determine search, filter, and sort behavior.

## Catalog source versus related concepts

Understanding how a catalog source relates to other [!DNL Adobe Commerce Optimizer] concepts helps you model your data correctly:

- **Catalog source** - The underlying data context that supplies product information. A catalog source is typically a locale (for example, `en-US`, `fr-CA`) or an external system such as a PIM or ERP. Products, attributes metadata, and categories are all scoped per catalog source. Think of a catalog source as *where* the raw catalog data comes from and *how* it affects product discovery (search results, filtering, and sorting behavior).

- **[Catalog view](catalog-view.md)** - A configured view of your catalog for a specific business need. When you create a catalog view, you select which catalog source (or locale) to use, then add [policies](policies.md) to filter which products are visible and link [price books](pricebooks.md) to control pricing. A single catalog source can power many catalog views (for example, one `en-US` source with separate catalog views for different brands or regions). Think of a catalog view as *how* you expose that data to a storefront, channel, or audience.

- **[Catalog layer](catalog-layer.md)** - A layer applied on top of base catalog data to modify product attributes (name, description, images, metadata) without changing the source data. Use catalog layers when differences must affect storefront display only - not product discovery.

## Rules and limitations

- A catalog source is created by ingesting a product via the Data Ingestion API. See [Developer Docs - Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) for more information.
- Product uniqueness is determined by SKU + catalog source.
- Shoppers do not access catalog sources directly. Catalog data is exposed to the storefront via [catalog views](catalog-view.md).

## Modeling guidance

Use the following guidance when deciding how to structure your catalog sources:

- Create a separate catalog source per different catalog language.
- Use separate catalog sources when product and attribute differences must affect search, filtering, or sorting behavior (for example, different searchability, filterability, or facet configuration for the same attribute).
- Use [catalog layers](catalog-layer.md) when product and attribute differences must affect storefront display only, not product discovery.

>[!MORELIKETHIS]
>
> * [Catalog views](catalog-view.md) - Configure filtered, priced views on top of a catalog source
> * [Catalog layers](catalog-layer.md) - Modify product presentation without changing source data
> * [Policies](policies.md) - Create attribute-based filters for catalog views
> * [Price books](pricebooks.md) - Manage pricing structures for different customer segments
