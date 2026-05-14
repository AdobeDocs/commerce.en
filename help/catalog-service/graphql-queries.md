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

Use  GraphQL queries to retrieve product, price, and other data from the Adobe Commerce Catalog SaaS data space and use it to render Commerce experiences more quickly than the native Adobe Commerce GraphQL queries.

{{aco-merchandising-services}}

The Catalog Service provides the following queries:

| Query | Description | Usage |
|-------|-------------|-------|
| `categories` | Returns category data. If the subtree input object is specified, the query returns details about subcategories. | Useful to render storefront navigation and category pages. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | Returns details about the SKUs specified as input. | Used primarily to render content on product detail and product compare pages. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | Returns a list of products that match the search criteria. | Useful for rendering search results and product list pages based on search input. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | Narrows the results of a products query run against a complex product to return a specific information about a product variant. | Useful for rendering updated product detail pages when the shoppers select a product option. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | Returns details about all variations of a product. | Useful for showing variant images on product detail or listing pages without submitting multiple API requests. [See example.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

See [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) for more information about using these queries.
