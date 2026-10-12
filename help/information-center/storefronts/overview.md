---
title: Storefronts
description: Learn about Adobe Commerce storefront options, including the Commerce Storefront powered by Edge Delivery Services and custom headless implementations.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
---

# Storefronts

The storefront is separate from the Commerce backend and API layers. Depending on the selected architecture, a storefront can retrieve data from Commerce Foundation APIs, Storefront Services APIs, [!DNL Adobe Commerce Optimizer] Merchandising Services APIs, or connected systems through API Mesh, App Builder, or other integration mechanisms. See [Architecture options](../architecture-options/overview.md) for how each storefront pairs with a Commerce backend.

## Commerce Storefront powered by Edge Delivery Services

The Commerce Storefront powered by [!DNL Edge Delivery Services] is a customer-facing storefront option built on the Adobe Commerce boilerplate, using drop-in components and content blocks. It's compatible with any of the [architecture options](../architecture-options/overview.md), connecting to Commerce Foundation, Storefront Services, or [!DNL Adobe Commerce Optimizer] Merchandising Services depending on the backend. See the [Adobe Commerce Storefront overview](https://experienceleague.adobe.com/developer/commerce/storefront/).

## Storefront Services

[!DNL Storefront Services] are storefront-oriented services used with [!DNL Adobe Commerce]. The service APIs provide optimized access to capabilities such as:

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

Storefront Services are used by both [!DNL Adobe Commerce] on Cloud or on premises when the services are configured, and [!DNL Adobe Commerce as a Cloud Service]. They're not exclusive to [!DNL Adobe Commerce as a Cloud Service] and shouldn't be used as the distinguishing label between the two [!DNL Adobe Commerce] platform options. See the [Storefront Services GraphQL schema](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## Custom headless storefronts

Storefront options beyond the Commerce Storefront powered by [!DNL Edge Delivery Services] may include [!DNL Luma], [!DNL PWA Studio], or a custom headless storefront, depending on platform support and implementation requirements. A custom headless storefront connects to the same API families as any other storefront option—Commerce Foundation, Storefront Services, or Commerce Optimizer Merchandising Services—based on the selected [architecture option](../architecture-options/overview.md).

## Cart and checkout integration

Where cart and checkout transactions are handled depends on the Commerce backend, not the storefront technology:

- When [!DNL Adobe Commerce] Commerce Foundation is the backend, the storefront uses Commerce Foundation APIs for cart, checkout, customer, and order operations, along with configured payment, tax, shipping, and fulfillment integrations.
- When a third-party commerce platform is the backend—as with stand-alone [!DNL Adobe Commerce Optimizer]—the storefront connects to that platform's cart, checkout, customer, order, payment, tax, shipping, and fulfillment services through API Mesh, App Builder, or a direct integration.

## Related guidance

- [Architecture options](../architecture-options/overview.md)
- [APIs](../apis/overview.md)
