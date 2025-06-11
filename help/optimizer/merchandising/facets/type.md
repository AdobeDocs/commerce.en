---
title: Facet Types
description: Learn about the different types of facets in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Types of Facets

[!DNL Adobe Commerce Optimizer] uses a variety of facets types and they appear in the *Filters* list only when relevant. The list of available facets changes according to the products returned. The following characteristics affect their presentation and behavior:

- Pinned facets  - The most commonly-used facets can be pinned to the top of the list. The remaining facets are listed in *Sort type* order after the pinned facets.
- Dynamic facets - Product attributes that [Adobe Sensei](https://www.adobe.com/sensei.html) finds most relevant to a product set and query. The calculation takes into account the attribute metadata of the entire catalog and determines at query time the most relevant facets for the query.

    >[!NOTE]
    >
    >If you notice that timeout errors are appearing in the GraphQL query response after creating dynamic facets, change all facets to pinned to see if that resolves the performance issues.

- Popular facets - Product attributes that are most often present in search results.
- Price facets - Return products by price range. You can specify the number of selections and the price range interval on the [*Settings*](../../settings.md) workspace.

At query time, [!DNL Adobe Commerce Optimizer] generates the search results in groups of dynamic and popular facets.

![Facets - Price](../../assets/storefront-search-results-run-price.png)

## Storefront options

Facets that are rendered for the [!DNL Adobe Commerce Optimizer] storefront are processed by the search adapter, which routes requests and renders the results in the storefront. All [!DNL Adobe Commerce Optimizer] storefront facets can be sorted alphabetically or by count, and can have either single- or multi-select options.

### Facet labels

For [!DNL Adobe Commerce Optimizer] storefronts, the facet label is determined by the [*Attribute Properties*](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html). You can edit facet labels from the [faceting workspace](workspace.md).

### Sort type

All facets rendered for the storefront are sorted alphabetically or by count.

| Sort type | Description |
|--- |--- |
| Alphabetic | In the storefront *Filters* list, facets are sorted alphabetically. |
| Count | Facets can also be sorted by the number of values found per facet in the current set of returned products. |
