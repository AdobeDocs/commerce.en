---
title: Headless
description: Learn how to integrate [!DNL Product Recommendations] in a headless storefront.
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
---
# Headless

You can integrate [!DNL Product Recommendations] in a headless storefront using either [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) or a custom frontend technology, such as React or Vue JS.

Custom and headless integrators should refer to these Luma and PWA instructions as a suggested implementation. There are many ways of implementing Product Recommendations into headless solutions and this documentation does not cover all scenarios. Integrators must cover eventing, design, and testing for their implementations.

[!DNL Product Recommendations] require [behavioral and catalog data](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html) to operate. The catalog data sync process remains unchanged in a headless implementation, but changes are needed for behavioral data collection.

 >[!NOTE]
 >
 >Headless instances must implement eventing to power the Product Recommendations dashboard.
 
To integrate [!DNL Product Recommendations] in a headless storefront, you must:

1. Send behavioral data to Adobe Sensei to analyze and compute Product Recommendation results. You can also send additional data to enable product recommendation [metrics reporting](workspace.md).

1. Fetch product recommendation results and render those results on the page.

You can perform both of these actions using the available SDKs as described in the following workflow.

1. [Install](install-configure.md) the [!DNL Product Recommendations] module.

1. Install and use the [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) to fire the [behavioral events](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html).

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

1. When the events are fired, use the [Adobe Commerce Storefront Event Collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) to handle the events and send them to Adobe Sensei.

1. After the behavioral data is collected, you can [create](create.md) [!DNL Product Recommendations] in the Admin.

1. Use the [Recommendations SDK](https://developer.adobe.com/commerce/services/product-recommendations/) to fetch the recommendation units on the storefront. The SDK returns necessary product data to render recommendation units on a page.

1. Learn how to use the [`recommendations` GraphQL query](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) to return information about product recommendation blocks for a given SKU and more.
