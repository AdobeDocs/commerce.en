---
title: "[!DNL Retrieve catalog data with GraphQL]"
description: Use GraphQL queries to retrieve the catalog data to power Commerce experiences.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Retrieve catalog data with GraphQL {#graphql-queries}

Use GraphQL queries to retrieve product, price, and other catalog data from the [!DNL Catalog Service] data space and render [!DNL Adobe Commerce] storefront experiences faster than native product queries.

{{aco-merchandising-services}}

The [!DNL Catalog Service] provides the following queries:

| Query | Description | Usage | Limits |
| --- | --- | --- | --- |
| `categories` | Returns category data. If the `subtree` input object is specified, the query returns details about subcategories. | Useful for rendering storefront navigation and category pages. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/){target="_blank"} | — |
| `products` | Returns details about the SKUs specified as input. | Used primarily to render content on product detail and product compare pages. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} | 100 SKUs per request |
| `productSearch` | Returns a list of products that match the search criteria. | Useful for rendering search results and product list pages based on search input. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/){target="_blank"} | 100 SKUs per request |
| `refineProduct` | Narrows the results of the `products` query for a complex product to return specific information about a product variant. | Useful for rendering updated product detail pages when shoppers select a product option. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/){target="_blank"} | 100 SKUs per request |
| `variants` | Returns details about all variations of a product. | Useful for showing variant images on product detail or listing pages without submitting multiple API requests. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/){target="_blank"} | 100 SKUs per request |

{style="table-layout:auto"}

See [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/){target="_blank"} for more information about using these queries.
