---
title: Facet Types
description: Learn about the different types of facets in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Types of Facets

[!DNL Adobe Commerce Optimizer] uses a variety of facets types and they appear in the *Filters* list only when relevant. The list of available facets changes according to the products returned. The following characteristics affect their presentation and behavior:

- Pinned facets  - The most commonly-used facets can be pinned to the top of the list. The remaining facets are listed in *Sort type* order after the pinned facets.
- Dynamic facets - Product attributes that [Adobe Sensei](https://www.adobe.com/sensei.html) finds most relevant to a product set and query. The calculation takes into account the attribute metadata of the entire catalog and determines at query time the most relevant facets for the query.
- Price facets - Return products by price range. You can specify the number of selections and the price range interval on the [*Settings*](../../settings.md) workspace.

## Facet labels

You can edit facet labels from the [faceting workspace](workspace.md).

## Sort type

All facets rendered for the storefront are sorted alphabetically or by count.

| Sort type | Description |
|--- |--- |
| Alphabetic | In the storefront *Filters* list, facets are sorted alphabetically. |
| Count | Facets can also be sorted by the number of values found per facet in the current set of returned products. |
