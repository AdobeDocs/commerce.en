---
title: Storefronts
description: Learn about Adobe Commerce storefront options, including the Commerce Storefront powered by Edge Delivery Services and custom headless implementations.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---

# Storefronts

The storefront is separate from the Commerce backend and API layers. Depending on the selected architecture, a storefront can retrieve data from Commerce Foundation APIs, Storefront Services APIs, [!DNL Adobe Commerce Optimizer] Merchandising Services APIs, or connected systems through API Mesh, App Builder, or other integration mechanisms. See [Architecture options](../architecture-options/overview.md) for how each storefront pairs with a Commerce backend.

## Commerce Storefront powered by Edge Delivery Services

The Commerce Storefront powered by [!DNL Edge Delivery Services] is a customer-facing storefront option built on the Adobe Commerce boilerplate, using drop-in components and content blocks. It is compatible with any of the [architecture overview](../architecture-options/overview.md), connecting to Commerce Foundation, Storefront Services, or [!DNL Adobe Commerce Optimizer] Merchandising Services depending on the backend. See the [Adobe Commerce Storefront overview](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

## Storefront Services

[!DNL Storefront Services] are storefront-oriented services used with [!DNL Adobe Commerce]. The service APIs provide optimized access to capabilities such as:

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

Both [!DNL Adobe Commerce] on Cloud or on-premises (when configured) and [!DNL Adobe Commerce as a Cloud Service] use Storefront Services. They are not exclusive to [!DNL Adobe Commerce as a Cloud Service] and should not be used as the distinguishing label between the two [!DNL Adobe Commerce] platform options. See the [Storefront Services GraphQL schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## Custom headless storefronts

Storefront options beyond the Commerce Storefront powered by [!DNL Edge Delivery Services] include [!DNL Luma], [!DNL PWA Studio], or a custom headless storefront, depending on platform support and implementation requirements. A custom headless storefront connects to the same API families as any other storefront option—Commerce Foundation, Storefront Services, or Commerce Optimizer Merchandising Services—based on the selected [architecture option](../architecture-options/overview.md).

## Cart and checkout integration

Where cart and checkout transactions are handled depends on the Commerce backend, not the storefront technology:

- When [!DNL Adobe Commerce] Commerce Foundation is the backend, the storefront uses Commerce Foundation APIs for cart, checkout, customer, and order operations, along with configured payment, tax, shipping, and fulfillment integrations.
- When a third-party commerce platform is the backend—as with stand-alone [!DNL Adobe Commerce Optimizer]—the storefront connects to that platform's cart, checkout, customer, order, payment, tax, shipping, and fulfillment services through API Mesh, App Builder, or a direct integration.

## Related guidance

- [Architecture overview](../architecture-options/overview.md)
- [APIs](../apis/commerce-apis.md)
