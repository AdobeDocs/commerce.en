---
title: Private Catalog Views
description: Learn how to create a private catalog view by enabling Catalog Protection so only requests with a valid signed token can retrieve its product and pricing data.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Private catalog views

By default, a [catalog view](catalog-view.md) is public—anyone who can reach the Merchandising API can retrieve its product and pricing data. Enable **[!UICONTROL Catalog Protection]** on a catalog view so that only requests carrying a valid signed token can retrieve its data.

See [Restricted access key use cases](restricted-access-keys.md#restricted-access-key-use-cases) for examples of when to protect a catalog view.

>[!IMPORTANT]
>
>Automatic key creation and management through Adobe Commerce and the Adobe Commerce Optimizer Connector are not yet available.

## Protect a catalog view

Before you begin, [create a restricted access key](restricted-access-keys.md) from the public key your client application generates.

1. On the catalog view create or edit form, toggle **[!UICONTROL Catalog Protection]** to **[!UICONTROL Enabled]**.

1. Under **[!UICONTROL Restricted Access Keys]**, select up to three [restricted access keys](restricted-access-keys.md) to assign to this catalog view.

   ![Catalog Protection enabled on the catalog view edit form, with a restricted access key assigned](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. Click **[!UICONTROL Save catalog view]**.

   The catalog view is now protected. Only requests carrying a valid signed token from an assigned key can retrieve its data.

   >[!NOTE]
   >
   >Allow up to five minutes for Catalog Protection configuration changes to take effect.

>[!NOTE]
>
>If [!UICONTROL Catalog Protection] is enabled and all assigned keys expire, the catalog view becomes inaccessible—storefronts that rely on this catalog view will not be able to serve data from it. Assign a new, unexpired key to restore access.

## Verify access is enforced

To confirm that a private catalog view rejects unauthorized requests, call its [GraphQL endpoint](../get-started.md#get-instance-details) with and without a signed token, using these headers:

| Header | Purpose |
| --- | --- |
| `AC-View-ID` | The catalog view to query. |
| `AC-Price-Book-ID` | The price book to apply. |
| `AC-Catalog-View-Access-Token` | The signed JWT proving authorization for the catalog view. |

A request without a valid token returns a GraphQL error instead of catalog data, for example:

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

A request carrying a token signed by an assigned, unexpired key returns the catalog data as expected. For details on signing a JWT and calling the Merchandising API, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication).

## More like this

- [Catalog views](catalog-view.md)—Learn how catalog views organize your product catalog by business structure, policies, and pricing.
- [Restricted access keys](restricted-access-keys.md)—Create, assign, and rotate the keys used to sign tokens for Catalog Protection.
