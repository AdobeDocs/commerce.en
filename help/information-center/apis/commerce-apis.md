---
title: Commerce APIs
description: Compare Adobe Commerce API families, including Commerce Foundation, Storefront Services, Commerce Optimizer Merchandising Services, and Data Ingestion.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
---

# APIs

| API family | Primary purpose | Used by |
| --- | --- | --- |
| **Commerce Foundation GraphQL APIs** | Core commerce and transactional capabilities such as catalog operations, cart, checkout, customers, and orders | [!DNL Adobe Commerce] on Cloud, [!DNL Adobe Commerce] on premises, and [!DNL Adobe Commerce as a Cloud Service] |
| **Storefront Services GraphQL APIs** | Storefront-oriented catalog, search, and recommendation experiences through [!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations] | [!DNL Adobe Commerce] on Cloud or on premises with configured services, and [!DNL Adobe Commerce as a Cloud Service] |
| **Commerce Optimizer Merchandising Services GraphQL APIs** | Retrieve Optimizer-managed catalog, catalog views, price contexts, search, recommendations, and merchandising results | [!DNL Adobe Commerce] on Cloud or on premises with the Optimizer Connector, and stand-alone [!DNL Adobe Commerce Optimizer] |
| **Commerce Optimizer Data Ingestion REST API** | Add catalog and price data to a stand-alone [!DNL Adobe Commerce Optimizer] implementation | Stand-alone [!DNL Adobe Commerce Optimizer] connected to an external data source |

## Commerce Foundation GraphQL APIs

Core commerce and transactional capabilities such as catalog operations, cart, checkout, customers, and orders. Used by [!DNL Adobe Commerce] on Cloud, [!DNL Adobe Commerce] on premises, and [!DNL Adobe Commerce as a Cloud Service]. See the [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/).

## Storefront Services GraphQL APIs

Storefront-oriented catalog, search, and recommendation experiences through [!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations]. Used by [!DNL Adobe Commerce] on Cloud or on premises with configured services, and [!DNL Adobe Commerce as a Cloud Service]. See the [Storefront Services GraphQL schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## Commerce Optimizer Merchandising Services GraphQL APIs

Retrieve Optimizer-managed catalog, catalog views, price contexts, search, recommendations, and merchandising results. Used by [!DNL Adobe Commerce] on Cloud or on premises with the [!DNL Adobe Commerce Optimizer Connector], and stand-alone [!DNL Adobe Commerce Optimizer]. See [Commerce Optimizer Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/).

## Commerce Optimizer Data Ingestion REST APIs

Add catalog and price data to a stand-alone [!DNL Adobe Commerce Optimizer] implementation from an external data source. See [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).

## Commerce Optimizer integrations

[!DNL Adobe Commerce Optimizer] connects to other systems through several integration paths, depending on whether it's paired with [!DNL Adobe Commerce] or a third-party backend.

### Adobe Commerce Optimizer Connector

Synchronizes catalog and price data from [!DNL Adobe Commerce] on Cloud or on premises to [!DNL Adobe Commerce Optimizer], so [!DNL Adobe Commerce] remains the transaction system while Optimizer supplies discovery and merchandising experiences. See [Commerce Optimizer Integrations](/help/optimizer/integrations/integrations-overview.md).

### Third-party commerce integrations

Ingests catalog and price data from a third-party commerce platform, PIM, ERP, or other source into stand-alone [!DNL Adobe Commerce Optimizer] through the Data Ingestion REST API, while the third-party platform remains the transactional system of record.

### API Mesh and App Builder

Use API Mesh to orchestrate Adobe Commerce APIs with private or third-party APIs. Use Adobe Developer App Builder to build custom applications and integrations. For related Commerce extensibility guidance, see [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) and [Adobe Commerce extensibility](https://developer.adobe.com/commerce/extensibility/).

For event-driven integrations specifically, see [Adobe I/O Events for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events).


### Cart and checkout handoff

For stand-alone [!DNL Adobe Commerce Optimizer] with an external commerce backend, the storefront uses Merchandising Services GraphQL APIs for product and catalog experiences, then hands off cart, checkout, customer, order, payment, tax, shipping, and fulfillment operations to the third-party backend through API Mesh, App Builder, or a direct integration.

### AEM Assets

AEM Assets is an optional, cross-cutting digital asset management integration that can be added to any Commerce or Optimizer architecture rather than a separate integration path of its own. See [AEM Assets integration for Commerce](../aem-assets/aem-assets-integration.md).

## Related guidance

- [Architecture overview](../architecture-options/overview.md)
- [Storefronts](../storefronts/overview.md)
- [AEM Assets integration for Commerce](../aem-assets/aem-assets-integration.md)
