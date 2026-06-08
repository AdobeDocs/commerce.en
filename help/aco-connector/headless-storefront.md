---
title: ACO Connector Headless Storefront Integration
description: Learn how to integrate a headless storefront with Adobe Commerce Optimizer using the ACO Connector's GraphQL API and bundle product add-to-cart format.
feature: Personalization, Integration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# Headless storefront integration

The `CommerceAdapter` module extends Adobe Commerce to bridge the gap between a headless storefront and Commerce Optimizer. It provides a GraphQL query for resolving the customer price book context, and enforces the bundle product encoding expected by the ACO API.

For high-level storefront setup instructions, see [Configure merchandising and storefronts](./overview.md#merchandising-storefronts) in the ACO Connector overview.

## GraphQL: `commerceOptimizer` query

Headless storefronts call the `commerceOptimizer` GraphQL query to retrieve the `priceBookId` for the current customer session. This value must then be passed to the ACO Catalog API when fetching prices.

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

**Example response:**

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

**How `priceBookId` is resolved:**

| Session state         | `priceBookId`                                                       |
|-----------------------|---------------------------------------------------------------------|
| Guest (not logged in) | `websiteCode::sha1(0)`, where `0` - not logged in customer group ID |
| Logged-in customer    | `websiteCode::sha1(customerGroupId)`                                |

The `Store` request header determines the website scope and therefore the `websiteCode` component. The `sha1(customerGroupId)` component matches the price book ID formula used during data sync - see [Price Books](reference/field-mappings.md#price-books).

## Bundle products: add-to-cart format

Allow shoppers add bundle product to te cart from a headless storefront with only `SKU` and `qty` values used for selected bundle option.

Each selected or entered option value must be base64-encoded in the following format:

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

The same child SKU may appear only once across all options. 

**Example (JavaScript):**

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
