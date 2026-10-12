---
title: Architecture Options
description: Compare Adobe Commerce architecture options, including Commerce Foundation, Adobe Commerce as a Cloud Service, Optimizer Connector, and stand-alone Optimizer.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
---

# Architecture options

Adobe Commerce architectures generally combine three layers: a commerce backend ([!DNL Adobe Commerce] or [!DNL Adobe Commerce Optimizer]), a storefront, and a set of connected services and integrations. Compare the following options to identify which system owns catalog, pricing, cart, checkout, orders, and customer transactions in each architecture.

## Architecture options at a glance

| Option | Commerce platform and system of record | Storefront experience | Storefront data path | Transaction path | Best fit |
| --- | --- | --- | --- | --- | --- |
| **1. [!DNL Adobe Commerce] on Cloud or on premises with Commerce Foundation** | Commerce Foundation is the commerce and transaction system | Edge Delivery Services, Luma, PWA, or custom headless storefront | Storefront Services for Catalog Service, Live Search, and Product Recommendations; Commerce Foundation APIs for core platform data | Commerce Foundation APIs and configured payment, tax, shipping, inventory, and fulfillment integrations | Customers that need the full [!DNL Adobe Commerce] platform with deployment control over cloud or on-premises infrastructure |
| **2. [!DNL Adobe Commerce as a Cloud Service] with Commerce Foundation** | Adobe-managed Commerce Foundation is the commerce and transaction system | Commerce Storefront powered by Edge Delivery Services or another supported headless experience | Storefront Services for Catalog Service, Live Search, and Product Recommendations; Commerce Foundation APIs for core platform data | Managed Commerce Foundation and connected Commerce services | Customers that want Adobe-managed SaaS Commerce with reduced infrastructure ownership |
| **3. [!DNL Adobe Commerce] on Cloud or on premises with the [!DNL Adobe Commerce Optimizer Connector]** | Existing Commerce Foundation remains the system of record for Commerce data and transactions | Edge Delivery Services, Luma, PWA, or custom headless storefront using Optimizer experiences | Commerce Optimizer Merchandising Services GraphQL APIs retrieve Optimizer-managed catalog and merchandising data | Existing Commerce Foundation APIs and connected transaction services | Customers that want to add Optimizer discovery and merchandising capabilities to an existing [!DNL Adobe Commerce] deployment |
| **4. Stand-alone [!DNL Adobe Commerce Optimizer] with an external commerce backend** | Existing or third-party commerce platform owns transactions; catalog and price data are added to Optimizer from an external source | Commerce Storefront powered by Edge Delivery Services or a custom headless storefront | Commerce Optimizer Merchandising Services GraphQL APIs retrieve catalog and merchandising data | API Mesh, App Builder, or direct integrations connect the storefront to third-party cart, checkout, customer, order, payment, tax, shipping, and fulfillment services | Customers that want Optimizer capabilities while retaining an existing or third-party transactional commerce platform |

## Adobe Commerce with Commerce Foundation

![Architecture diagram of Adobe Commerce on Cloud or on premises with Storefront Services and Commerce Foundation APIs feeding a Commerce Storefront](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="800" zoomable="yes"}

**Key boundary:** Commerce Foundation owns the Commerce platform and transaction flows. [!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations] provide optimized storefront access to catalog, search, and recommendations when configured. AEM Assets integration is optional. See [AEM Assets integration for Commerce](../aem-assets/overview.md).

**References:**

- [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)
- [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Storefront Services GraphQL schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe Commerce as a Cloud Service

![Architecture diagram of Adobe Commerce as a Cloud Service with managed Commerce Foundation and Storefront Services feeding a Commerce Storefront](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="800" zoomable="yes"}

**Key boundary:** Adobe manages the Commerce Foundation platform. The architecture uses Storefront Services, including [!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations], for storefront experiences. [!DNL Product Visuals] powered by AEM Assets is an optional SaaS integration. See [AEM Assets integration for Commerce](../aem-assets/overview.md).

**References:**

- [[!DNL Adobe Commerce as a Cloud Service] overview](/help/cloud-service/overview.md)
- [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)
- [Storefront Services GraphQL schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe Commerce with the Optimizer Connector

![Architecture diagram of the Adobe Commerce Optimizer Connector synchronizing catalog and price data from Adobe Commerce to Adobe Commerce Optimizer, feeding a Commerce Storefront through Merchandising Services APIs](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="800" zoomable="yes"}

**Key boundary:** The Connector synchronizes catalog and price data from [!DNL Adobe Commerce] to [!DNL Adobe Commerce Optimizer]. [!DNL Adobe Commerce] remains the transaction system, while Optimizer supplies discovery and merchandising experiences through its Merchandising Services APIs.

**References:**

- [Commerce Optimizer Integrations](/help/optimizer/integrations/integrations-overview.md)
- [Commerce Optimizer Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)

## Stand-alone Commerce Optimizer with a third-party backend

![Architecture diagram of customer-owned source systems sending catalog and price data through Data Ingestion to a stand-alone Adobe Commerce Optimizer, feeding a Commerce Storefront connected to a third-party commerce backend](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**Key boundary:** Stand-alone [!DNL Adobe Commerce Optimizer] owns catalog discovery and merchandising experiences, but not the transactional Commerce backend. Catalog and price data enter through the Data Ingestion REST API. The Edge Delivery Services storefront uses Merchandising Services GraphQL APIs for product experiences and connects to the third-party backend for cart and checkout.

**References:**

- [What is Adobe Commerce Optimizer?](/help/optimizer/overview.md)
- [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Commerce Optimizer Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)

## Related guidance

- [Choose a Commerce option](../choose-commerce-option/overview.md)
- [Storefronts](../storefronts/overview.md)
- [APIs](../apis/overview.md)
