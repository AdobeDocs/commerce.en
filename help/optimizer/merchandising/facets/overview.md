---
title: Facets Overview
description: Learn about facets in [!DNL Adobe Commerce Optimizer] and how they improve search results.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Facets

Facets is a method of high-performance filtering that uses multiple dimensions of attribute values as search criteria.

![Filtered search results](../../assets/storefront-search-results-run.png)

Within a facet, shoppers can select multiple options, such as "Basic" and "Snug" under "Style" and the search results update to display only those styles. Likewise, if a shopper selects options across facets, such as "Basic" under "Style" and "Indoor" under "Climate", the search results update to display that selected style and that selected climate.

Any defined facet may be used as a URL parameter and results will be filtered based on the parameter values: `http://yourstore.com?brand=acme&color=red`.

## Facet aggregation

Facet aggregation is performed as follows: if the storefront has three facets (categories, color, and price) and the shopper filters on all three (color = blue, price is from $10.00-50.00, categories = `promotions`).

- `categories` aggregation - Aggregates `categories`, then applies the `color` and `price` filters, but not the `categories` filter.
- `color` aggregation - Aggregates `color`, then applies  the `price` and `categories` filters, but not the `color` filter.
- `price` aggregation - Aggregates `price`, then applies the `color` and `categories` filters, but not the `price` filter.

## Default attribute values

The following [product attributes](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#operation/createProductMetadata) are used by [!DNL Adobe Commerce Optimizer] and enabled by default.

| Property | Description | Attribute |
|---|---|---|
| Sortable | Used for Sorting in Product Listing | `price`|
| Searchable | Use in Search | `price` <br />`sku`<br />`name`|

## Default non-system attribute properties

The following table shows the default search and filterable properties of non-system attributes. Setting the *Use in Search* attribute property to `Yes` makes the attribute searchable in [!DNL Adobe Commerce Optimizer].

| Attribute Code | Searchable |
|--- |--- |--- |
| activity | Yes | 
| attributes_brand | Yes | 
| brand | Yes |
| climate | Yes | 
| collar | Yes | 
| color | Yes | 
| cost | Yes |
| eco_collection |
| gender | Yes | 
| manufacturer | Yes | 
| material | Yes | 
| purpose | Yes | 
| strap_bags | Yes | 
| style_general | Yes | 

## Default system attribute properties

The following table shows the default search and filterable properties of system attributes.

| Attribute Code | Searchable |
|--- |--- |--- |
| allow_open_amount | Yes | 
| description | Yes |
| name | Yes |
| price | Yes | 
| short_description | Yes |
| sku | Yes |
| status | Yes |
| tax_class_id | Yes |
| url_key | Yes |
| weight | Yes |
