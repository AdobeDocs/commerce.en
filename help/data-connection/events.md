---
title: Behavioral Events
description: Learn what data each behavioral event captures.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
---
# [!DNL Data Connection] Behavioral Events

The following lists the Commerce behavioral events available when you install the [!DNL Data Connection] extension. The data these events collect is sent to the Adobe Experience Platform. You can also create [custom events](custom-events.md) to collect additional data not provided out of the box.

In addition to the data the following events collect, you also get [other data](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) provided by the Adobe Experience Platform Web SDK.

The behavioral events collect anonymized behavioral data from your shoppers as they browse your site. You can use the data these events collect to create promotions and campaigns targeted to a specific set of shoppers.

>[!NOTE]
>
>All behavioral events include the [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) field, which includes the shopper's email address, when available, and ECID.

## Storefront events

Storefront events capture data from shoppers' interactions on the site and include events such as `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut`, and so on. Storefront events apply to simple and configurable products only.

See the [developer documentation](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) to learn more about storefront events. 

## Customer profile events

Profile events captured from the storefront include account information, such as `signIn`, `signOut`, `createAccount`, and `editAccount`. This data is used to help populate key customer details that are needed to better define segments or execute marketing campaigns, such as sending sign-up discount offers, account change confirmations, and so on.

See the [developer documentation](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) to learn more about customer profile events. 

## Search events

The search events provide data relevant to the shopper's intent. Insight into a shopper's intent helps merchants see how shoppers are searching for items, what they click, and ultimately purchase or abandon. An example of how you might use this data is if you want to target existing shoppers who search for your top product, but never purchase the product. You must install the [[!DNL Live Search]](../live-search/install.md) extension to access these events.

Use the `searchRequest.id` and `searchResponse.id` fields found in both the `searchRequestSent` and `searchResponseReceived` events to cross-reference a search request to the corresponding search response.

See the [developer documentation](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) to learn more about search events. 

## B2B events

![B2B for Adobe Commerce](../assets/b2b.svg) For B2B merchants, you must [install](install.md#install-the-b2b-extension) the `experience-platform-connector-b2b` extension to access these events.

The B2B events contain [requisition list](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html) information, such as if a requisition list was created, added to, or deleted from. By tracking events specific to requisition lists, you can see which products your customers purchase frequently and create campaigns based on that data.

See the [developer documentation](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) to learn more about B2B events.
