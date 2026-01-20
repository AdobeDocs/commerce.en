---
title: Facets
description: '[!DNL Live Search] facets use multiple dimensions of attribute values as search criteria.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
---
# Facets

Faceting is a method of high-performance filtering that uses multiple dimensions of attribute values as search criteria. Faceted search is similar, but considerably "smarter" than the standard [layered navigation](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html). The list of available filters is determined by the [filterable attributes](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html#filterable-attributes) of products returned in the search results. 

[!DNL Live Search] uses the `productSearch` query, which returns faceting and other data that is specific to [!DNL Live Search]. Refer to [`productSearch` query](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) in the developer documentation for code examples.

![Filtered search results](assets/storefront-search-results-run.png)

Within a facet, shoppers can select multiple options, such as "Basic" and "Snug" under "Style" and the search results update to display only those styles. Likewise, if a shopper selects options across facets, such as "Basic" under "Style" and "Indoor" under "Climate", the search results update to display that selected style and that selected climate.

Any defined facet may be used as a URL parameter and results will be filtered based on the parameter values: `http://yourstore.com?brand=acme&color=red`.

## Faceting requirements

The category and product attribute requirements for faceting are similar to the filterable attributes used for layered navigation. Each storefront properties of an attribute must have the "Use in Search Results Layered Navigation" value set to "Yes". You can review and update the attribute configuration from the [!DNL Stores] > [!DNL Attribute] menu in the Admin. 

>[!NOTE]
>
>If you define a product category as a facet, the facet displays the `url_path` of the category and the subcategory.
>
>![Category facet](assets/facet-category.png)

See [boundaries and limits](./boundaries-limits.md#facets) to learn more about the facet requirements in [!DNL Live Search].

If you have a large number of attributes to contend with, consider combining attributes into a single 'meta-attribute'. For example, shoes generally have numeric sizes, while shirts are commonly sized "S/M/L/XL". These two types of sizes can be combined into a single searchable attribute.

| Setting | Description |
|--- |--- |
| [Category display settings](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html) | Anchor - `Yes` |
| [Attribute properties](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html) | [Catalog Input type](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html) - `Yes/No`, `Dropdown`, `Multiple Select`, `Price`, `Visual swatch` (widget only), `Text swatch` (widget only) |
| Attribute storefront properties | Use in Search Results Layered Navigation - `Yes` |

## Facet aggregation

Facet aggregation is performed as follows: if the storefront has three facets (categories, color, and price) and the shopper filters on all three (color = blue, price is from $10.00-50.00, categories = `promotions`).

* `categories` aggregation - Aggregates `categories`, then applies the `color` and `price` filters, but not the `categories` filter.
* `color` aggregation - Aggregates `color`, then applies  the `price` and `categories` filters, but not the `color` filter.
* `price` aggregation - Aggregates `price`, then applies the `color` and `categories` filters, but not the `price` filter.
