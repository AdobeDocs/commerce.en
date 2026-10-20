---
title: B2B Shared Catalog Projection
description: Learn how B2B connector projects Adobe Commerce B2B shared catalogs into protected Commerce Optimizer catalog views, and how storefronts resolve and authorize buyer access.
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# B2B shared catalog projection

The [!DNL Adobe Commerce Optimizer Connector for B2B] projects [!DNL Adobe Commerce] shared catalogs and company assignments into protected [!DNL Adobe Commerce Optimizer] catalog views.

## Base synchronization and B2B projection

The base [!DNL Adobe Commerce Optimizer Connector] synchronizes catalog and pricing feeds, mapping store views to catalog sources, websites to price books, and customer groups to price books.

The [!DNL Adobe Commerce Optimizer Connector for B2B] projects each custom shared catalog's assortment and prices into a protected view. Adobe Commerce selects the view using the buyer's company assignment. The restricted access key verifies signed requests but does not determine catalog access. Adobe Commerce is the system of record for connector-managed catalog, pricing, and B2B projection data. Manage product discovery and recommendations in the [!DNL Adobe Commerce Optimizer] configuration.

## Data mapping

The B2B projection combines synchronized catalog content and pricing with Shared Catalog assortment and company assignment context.

![Diagram mapping [!DNL Adobe Commerce] store views, pricing, shared catalogs, and company assignments to projected private catalog views in [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}

| [!DNL Adobe Commerce] data | [!DNL Adobe Commerce Optimizer] result | Purpose |
| --- | --- | --- |
| Enabled store view and product data | Catalog source | Supplies localized product content. |
| Website and customer group pricing | Price book | Supplies the applicable prices but does not authorize access |
| Custom shared catalog assortment | Policy | Filters the catalog view to the shared catalog assortment. |
| Custom shared catalog and enabled store view | Private catalog view | Creates one protected view for each combination, with the applicable catalog source, policy, and price book. |
| Company assignment to a shared catalog | Resolved buyer context | Lets the authenticated backend resolve the catalog view associated with the buyer's company. |
| Restricted access key assigned to a protected view | Catalog Protection | Authorizes requests to the protected catalog view but does not select pricing. |

Each private catalog view can reference only one price book. Store views with the same website and customer-group pricing context can share a price book while using different localized catalog sources. The connector does not create a price book per shared catalog.

The default shared catalog is not projected as a B2B private catalog view.

## Runtime authorization

After a buyer signs in, the Commerce backend authenticates the session and uses the buyer's company assignment and store view to resolve the appropriate catalog view and price book.

The storefront sends the catalog view ID, price book ID, and signed token with each Merchandising API request. [!DNL Adobe Commerce Optimizer] verifies the RS256 signature for the JWT against the restricted access keys assigned to the catalog view. It returns catalog data only when the token and key are valid and unexpired.

![Runtime authorization flow for B2B catalog requests from a shopper through a storefront and Commerce backend to [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}

For private catalog requests, send these headers:

| Header | Purpose |
| --- | --- |
| `AC-View-ID` | Identifies the catalog view. |
| `AC-Price-Book-ID` | Identifies the price book to use. |
| `AC-Catalog-View-Access-Token` | Carries the signed JWT that authorizes access to the protected catalog view. |

For the full request and token requirements, see [Merchandising API authentication](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication) and [Verify access to a private catalog view](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced).

## Protection boundary

Catalog protection covers catalog and search requests only. It does not secure cart, checkout, or order operations. Enforce purchase eligibility in Adobe Commerce or the connected transaction system.

## Projection setup and monitoring

The B2B connector projects private catalog views, policies, price book references, and restricted access key configuration from [!DNL Adobe Commerce]. You do not need to create those connector-managed projection objects manually. For setup instructions, see [Get started with the B2B connector](get-started-b2b-shared-catalogs.md).

To monitor projected catalog views and reconcile configuration drift, see [Monitor catalog view synchronization](catalog-view-sync-status.md). To manage the assigned keys, see [Manage restricted access keys for B2B shared catalogs](restricted-access-keys.md).
