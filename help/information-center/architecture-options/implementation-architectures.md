---
title: Implementation Architecture Options
description: Compare Adobe Commerce architectures, including Commerce Foundation, Adobe Commerce as a Cloud Service, Optimizer Connector, and stand-alone Optimizer.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:39:51.406Z'
TQID: 'https://experienceleague.adobe.com/tYkxRAfJWOY7C0OEqYxEb4onwvnnL9wEofEG2e6qnKA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
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
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---

# Implementation architecture options

Adobe Commerce implementation architectures combine three layers: a commerce backend ([!DNL Adobe Commerce] or [!DNL Adobe Commerce Optimizer]), a storefront, and a set of connected services and integrations. Compare the following options to identify which system owns catalog, pricing, cart, checkout, orders, and customer transactions in each architecture.

## Architecture options summary

Compare the options by transaction ownership and by storefront experience.

### Commerce platform and transactions

| Option | System of record | Transaction path | Best fit |
| --- | --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service] with Commerce Foundation** | Adobe-managed Commerce Foundation | Managed Commerce Foundation and connected Commerce services | Customers that want Adobe-managed software as a service (SaaS) Commerce with reduced infrastructure ownership |
| **[!DNL Adobe Commerce] on Cloud or on premises with the [!DNL Adobe Commerce Optimizer Connector]** | Existing Commerce Foundation, for Commerce data and transactions | Existing Commerce Foundation APIs and connected transaction services | Customers that want to add Optimizer discovery and merchandising capabilities to an existing [!DNL Adobe Commerce] deployment |
| **Stand-alone [!DNL Adobe Commerce Optimizer] with an external commerce backend** | Existing or third-party commerce platform. Catalog and price data are added to Optimizer from an external source | API Mesh, App Builder, or direct integrations connect the storefront to third-party cart, checkout, customer, order, payment, tax, shipping, and fulfillment services | Customers that want Optimizer capabilities while retaining an existing or third-party transactional commerce platform |
| **[!DNL Adobe Commerce] on Cloud or on premises with Commerce Foundation** | Commerce Foundation | Commerce Foundation APIs and configured payment, tax, shipping, inventory, and fulfillment integrations | Customers that need the full [!DNL Adobe Commerce] platform with deployment control over cloud or on-premises infrastructure |

### Storefront experience

Storefronts connect to Commerce Foundation APIs, Storefront Services ([!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations]), or [!DNL Adobe Commerce Optimizer] Merchandising Services.

| Option | Storefront experience | Storefront data path |
| --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service] with Commerce Foundation** | Commerce Storefront powered by Edge Delivery Services or another supported headless experience | Storefront Services, plus Commerce Foundation APIs for core platform data |
| **[!DNL Adobe Commerce] on Cloud or on premises with the [!DNL Adobe Commerce Optimizer Connector]** | Edge Delivery Services or custom headless storefront using Optimizer experiences | Commerce Optimizer Merchandising Services GraphQL APIs for Optimizer-managed catalog and merchandising data |
| **Stand-alone [!DNL Adobe Commerce Optimizer] with an external commerce backend** | Commerce Storefront powered by Edge Delivery Services or a custom headless storefront | Commerce Optimizer Merchandising Services GraphQL APIs for catalog and merchandising data |
| **[!DNL Adobe Commerce] on Cloud or on premises with Commerce Foundation** | Edge Delivery Services, Luma, PWA, or custom headless storefront | Commerce Foundation APIs, plus Storefront Services when configured |

## Adobe Commerce as a Cloud Service

![Architecture diagram of Adobe Commerce as a Cloud Service with managed Commerce Foundation and Storefront Services feeding a Commerce Storefront](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Key boundary**—Adobe manages the Commerce Foundation platform. The architecture uses Storefront Services, including [!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations], for storefront experiences. [!DNL Product Visuals] powered by AEM Assets is an optional SaaS integration. See [AEM Assets integration for Commerce](../aem-assets/aem-assets-integration.md).

**References:**

- [[!DNL Adobe Commerce as a Cloud Service] overview](/help/cloud-service/overview.md)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Storefront Services GraphQL schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe Commerce with Commerce Foundation

![Architecture diagram of Adobe Commerce on Cloud or on premises with Storefront Services and Commerce Foundation APIs feeding a Commerce Storefront](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Key boundary**—Commerce Foundation owns the Commerce platform and transaction flows. [!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations] provide optimized storefront access to catalog, search, and recommendations when configured. AEM Assets integration is optional. See [AEM Assets integration for Commerce](../aem-assets/aem-assets-integration.md).

**References:**

- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Storefront Services GraphQL schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)


## Adobe Commerce with the Optimizer Connector

![Architecture diagram of the Adobe Commerce Optimizer Connector synchronizing catalog and price data from Adobe Commerce to Adobe Commerce Optimizer, feeding a Commerce Storefront through Merchandising Services APIs](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="600" zoomable="yes"}

**Key boundary**—The Connector synchronizes catalog and price data from [!DNL Adobe Commerce] to [!DNL Adobe Commerce Optimizer]. [!DNL Adobe Commerce] remains the transaction system, while Optimizer supplies discovery and merchandising experiences through its Merchandising Services APIs.

**References:**

- [Commerce Optimizer Integrations](/help/optimizer/integrations/integrations-overview.md)
- [Commerce Optimizer Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Stand-alone Commerce Optimizer with a third-party backend

![Architecture diagram of customer-owned source systems sending catalog and price data through Data Ingestion to a stand-alone Adobe Commerce Optimizer, feeding a Commerce Storefront connected to a third-party commerce backend](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**Key boundary**—Stand-alone [!DNL Adobe Commerce Optimizer] owns catalog discovery and merchandising experiences, but not the transactional Commerce backend. Catalog and price data enter through the Data Ingestion REST API. The Edge Delivery Services storefront uses Merchandising Services GraphQL APIs for product experiences and connects to the third-party backend for cart and checkout.

**References:**

- [What is Adobe Commerce Optimizer?](/help/optimizer/overview.md)
- [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Commerce Optimizer Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Terminology quick reference

| Preferred term | Meaning | Avoid using as a current architecture label |
| --- | --- | --- |
| **Commerce Foundation** | Base commerce and transactional capabilities | Core Commerce, PHP Foundational Layer |
| **Storefront Services** | Storefront-oriented APIs for Catalog Service, Live Search, and Product Recommendations | A label limited to only one Commerce platform |
| **Commerce Optimizer Merchandising Services** | Optimizer APIs for catalog discovery and merchandising experiences | Commerce Foundation APIs |
| **Commerce Storefront powered by Edge Delivery Services** | Customer-facing storefront implementation | An API family |

## Related guidance

- [Reference architectures](reference-architectures.md)
- [Choose a Commerce option](../portfolio/choose-commerce-option.md)
- [Storefronts](../storefronts/overview.md)
- [APIs](../apis/commerce-apis.md)
