---
title: Facets
description: '[!DNL Adobe Commerce Optimizer] facets use multiple dimensions of attribute values as search criteria.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
---
# Facets

Facets is a method of high-performance filtering that uses multiple dimensions of attribute values as search criteria. Faceted search is similar, but considerably "smarter" than the standard [layered navigation](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html). The list of available filters is determined by the [filterable attributes](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html#filterable-attributes) of products returned in the search results. 

[!DNL Adobe Commerce Optimizer] uses the `productSearch` query, which returns faceting and other data that is specific to [!DNL Adobe Commerce Optimizer]. Refer to [`productSearch` query](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) in the developer documentation for code examples.

![Filtered search results](../../assets/storefront-search-results-run.png)

Within a facet, shoppers can select multiple options, such as "Basic" and "Snug" under "Style" and the search results update to display only those styles. Likewise, if a shopper selects options across facets, such as "Basic" under "Style" and "Indoor" under "Climate", the search results update to display that selected style and that selected climate.

Any defined facet may be used as a URL parameter and results will be filtered based on the parameter values: `http://yourstore.com?brand=acme&color=red`.

## Facets requirements

The category and product attribute requirements for faceting are similar to the filterable attributes used for layered navigation. Each storefront properties of an attribute must have the "Use in Search Results Layered Navigation" value set to "Yes".

[!DNL Adobe Commerce Optimizer] supports up to:

- 100 attributes configured as facets
- 50 sortable attributes
- 200 filterable attributes
- 200 searchable attributes

>[!NOTE]
>
> If there are more than 200 filterable attributes defined, it is not deterministic which 200 will actually be indexed.

If you have a large number of attributes to contend with, consider combining attributes into a single 'meta-attribute'. For example, shoes generally have numeric sizes, while shirts are commonly sized "S/M/L/XL". These two types of sizes can be combined into a single searchable attribute.

| Setting | Description |
|--- |--- |
| [Category display settings](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html) | Anchor - `Yes` |
| [Attribute properties](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html) | [Catalog Input type](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html) - `Yes/No`, `Dropdown`, `Multiple Select`, `Price`, `Visual swatch` (widget only), `Text swatch` (widget only) |
| Attribute storefront properties | Use in Search Results Layered Navigation - `Yes` |

## Facet aggregation

Facet aggregation is performed as follows: if the storefront has three facets (categories, color, and price) and the shopper filters on all three (color = blue, price is from $10.00-50.00, categories = `promotions`).

- `categories` aggregation - Aggregates `categories`, then applies the `color` and `price` filters, but not the `categories` filter.
- `color` aggregation - Aggregates `color`, then applies  the `price` and `categories` filters, but not the `color` filter.
- `price` aggregation - Aggregates `price`, then applies the `color` and `categories` filters, but not the `price` filter.

## Default attribute values

The following product attributes have [storefront properties](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) that are used by [!DNL Adobe Commerce Optimizer] and enabled by default.

| Property | Storefront Property | Attribute |
|---|---|---|
| Sortable | Used for Sorting in Product Listing | `price`|
| Searchable | Use in Search | `price` <br />`sku`<br />`name`|
| FilterableInSearch | Use in Layered Navigation - Filterable (with results)| `price`<br />`visibility`<br />`category_name`|

## Default non-system attribute properties

The following table shows the default search and filterable properties of non-system attributes, including those that are specific to the Luma sample data. Setting the *Use in Search* attribute property to `Yes` makes the attribute searchable in both [!DNL Adobe Commerce Optimizer] and native Adobe Commerce.

| Attribute Code | Searchable | Use in Layered Navigation |
|--- |--- |--- |
| activity | Yes | Filterable (with results) |
| attributes_brand | Yes | No |
| brand | Yes | No |
| climate | Yes | Filterable (with results) |
| collar | Yes | Filterable (with results) |
| color | Yes | Filterable (with results) |
| cost | Yes | No |
| eco_collection | Yes | Filterable (with results) |
| gender | Yes | Filterable (with results) |
| manufacturer | Yes | Filterable (with results) |
| material | Yes | Filterable (with results) |
| purpose | Yes | Filterable (with results) |
| strap_bags | Yes | Filterable (with results) |
| style_general | Yes | Filterable (with results) |

## Default system attribute properties

The following table shows the default search and filterable properties of system attributes.

| Attribute Code | Searchable | Use in Layered Navigation |
|--- |--- |--- |
| allow_open_amount | Yes | Filterable (with results) |
| description | Yes | No |
| name | Yes | No |
| price | Yes | Filterable (with results) |
| short_description | Yes | No |
| sku | Yes | No |
| status | Yes | No |
| tax_class_id | Yes | No |
| url_key | Yes | No |
| weight | Yes | No |
