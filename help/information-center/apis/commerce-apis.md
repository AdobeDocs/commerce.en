---
title: Commerce APIs
description: Compare Adobe Commerce API families, including Commerce Foundation, Storefront Services, Commerce Optimizer Merchandising Services, and Data Ingestion.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
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

Connect a storefront to third-party or custom systems—such as cart, checkout, customer, or order services—when the transactional backend isn't [!DNL Adobe Commerce] Commerce Foundation. See [Adobe I/O Events for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events).

### Cart and checkout handoff

For stand-alone [!DNL Adobe Commerce Optimizer] with an external commerce backend, the storefront uses Merchandising Services GraphQL APIs for product and catalog experiences, then hands off cart, checkout, customer, order, payment, tax, shipping, and fulfillment operations to the third-party backend through API Mesh, App Builder, or a direct integration.

### AEM Assets

AEM Assets is an optional, cross-cutting digital asset management integration that can be added to any Commerce or Optimizer architecture rather than a separate integration path of its own. See [AEM Assets integration for Commerce](../aem-assets/aem-assets-integration.md).

## Related guidance

- [Architecture options](../architecture-options/implementation-architectures.md)
- [Storefronts](../storefronts/storefronts.md)
- [AEM Assets integration for Commerce](../aem-assets/aem-assets-integration.md)
