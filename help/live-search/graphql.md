---
title: GraphQL
description: The [!DNL Live Search] GraphQL workspace lets you build queries with your live data.
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
---
# GraphQL

The *GraphQL* workspace allows administrators to build and test GraphQL queries using their own data.

This workspace supports the [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/product-search/) and [`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/attribute-metadata/) queries.

![GraphQL workspace](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
		name
      }
    }
    facets {
      title
    }
  }
}
```

Variables:

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```
