---
title: Headless
description: Learn how to integrate [!DNL Product Recommendations] in a headless storefront.
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
TQID: https://experienceleague.adobe.com/J3qXs-SWuDCz7pQwzGm0VcOOFoU1QM2M4qwsTxxPwE8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Headless

You can integrate [!DNL Product Recommendations] in a headless storefront using either [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) or a custom frontend technology, such as React or Vue JS.

Custom and headless integrators should refer to these Luma and PWA instructions as a suggested implementation. There are many ways of implementing Product Recommendations into headless solutions and this documentation does not cover all scenarios. Integrators must cover eventing, design, and testing for their implementations.

[!DNL Product Recommendations] require [behavioral and catalog data](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html) to operate. The catalog data sync process remains unchanged in a headless implementation, but changes are needed for behavioral data collection.

 >[!NOTE]
 >
 >Headless instances must implement eventing to power the Product Recommendations dashboard.
 
To integrate [!DNL Product Recommendations] in a headless storefront, you must:

1. Send behavioral data to Adobe AI to analyze and compute Product Recommendation results. You can also send additional data to enable product recommendation [metrics reporting](workspace.md).

1. Fetch product recommendation results and render those results on the page.

You can perform both of these actions using the available SDKs as described in the following workflow.

1. [Install](install-configure.md) the [!DNL Product Recommendations] module.

1. Install and use the [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) to fire the [behavioral events](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

    The minimum required events to return [!DNL Product Recommendations] results:

    | Event | Category |
    |--- | ---|
    |`view` | product|
    |`add-to-cart` | product|
    |`place-order` | checkout|

    To enable [metrics reporting](workspace.md), the following additional events are required:

    |Event | Category|
    |--- | ---|
    |`impression-render` | recommendation-unit|
    |`view` | recommendation-unit|
    |`rec-click` | recommendation-unit|
    |`rec-add-to-cart-click` | recommendation-unit (if an "Add to cart" button is present in the recommendations template)|

1. When the events are fired, use the [Adobe Commerce Storefront Event Collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) to handle the events and send them to Adobe AI.

1. After the behavioral data is collected, you can [create](create.md) [!DNL Product Recommendations] in the Admin.

1. Use the [Recommendations SDK](https://developer.adobe.com/commerce/services/product-recommendations/) to fetch the recommendation units on the storefront. The SDK returns necessary product data to render recommendation units on a page.

1. Learn how to use the [`recommendations` GraphQL query](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) to return information about product recommendation blocks for a given SKU and more.
