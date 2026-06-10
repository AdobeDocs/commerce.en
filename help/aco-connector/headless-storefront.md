---
title: '[!DNL Adobe Commerce Optimizer Connector] Headless Storefront Integration'
description: Learn how to integrate headless storefronts with the [!DNL Adobe Commerce Optimizer Connector] GraphQL API, price book IDs, and bundle add-to-cart encoding.
feature: Storefront, Integration, GraphQL
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Headless storefront integration

The `CommerceAdapter` module extends [!DNL Adobe Commerce] to bridge the gap between a headless storefront and [!DNL Adobe Commerce Optimizer]. It provides a GraphQL query for resolving the customer price book context, and enforces the bundle product encoding expected by the [!DNL Adobe Commerce Optimizer] GraphQL API.

For high-level storefront setup instructions, see [Configure merchandising and storefronts](./overview.md#merchandising-storefronts) in the [!DNL Adobe Commerce Optimizer Connector] overview.

## GraphQL: `commerceOptimizer` query {#graphql-commerceoptimizer-query}

Headless storefronts call the `commerceOptimizer` GraphQL query to retrieve the `priceBookId` for the current customer session. Pass this value to the [[!DNL Adobe Commerce Optimizer] GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"} when fetching prices.

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

Example response:

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

How `priceBookId` is resolved:

| Session state         | `priceBookId`                                                       |
|-----------------------|---------------------------------------------------------------------|
| Guest (not logged in) | `websiteCode::sha1(0)`, where `0` is the guest customer group ID    |
| Logged-in customer    | `websiteCode::sha1(customerGroupId)`                                |

The `Store` request header determines the website scope and therefore the `websiteCode` component. The `sha1(customerGroupId)` component matches the price book ID formula used during data sync. See [Price books](reference/field-mapping.md#price-books).

## Bundle products: add-to-cart format {#bundle-products-add-to-cart-format}

Allow shoppers to add bundle products to the cart from a headless storefront with only the `SKU` and `qty` for each selected bundle option.

Each selected or entered option value must be base64-encoded in the following format:

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

The same child SKU may appear only once across all options.

Example ([!DNL JavaScript]):

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
