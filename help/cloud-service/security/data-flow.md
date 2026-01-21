---
title: Security architecture and data flow
description: Learn about the security architecture and data flow for Adobe Commerce as a Cloud Service.
role: Admin, Architect, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---

# Security architecture and data flow

The following example illustrates how data typically flows in [!DNL Adobe Commerce as a Cloud Service]:

![Adobe Commerce as a Cloud Service data flow diagram](../assets/data-flow-1.png)

## Data flow narrative

**Step 1**: The shopper types in the URL of the merchant's storefront in their browser, which sends the URL to the Commerce Storefront's Content Delivery Network (External CDN).

**Step 2**: If the site URL is cached, the Storefront CDN returns it to the shopper. If it is not already cached, which could occur if this is the first request for a resource, the external CDN forwards the shopper's request to the internal CDN and caches the response for subsequent requests.

**Step 2a**: If the request is for images or videos, it is sent to [!DNL Product Visuals] for fulfillment and returned to the storefront.

**Step 3**: If the site URL is cached on the internal CDN, it is returned from that cache. If not, it is sent to [!DNL API Mesh] and the response is cached for subsequent requests.

**Step 4**: [!DNL API Mesh] acts as the orchestration layer and determines whether to send the request to [!DNL Adobe Commerce as a Cloud Service] or a third-party system to fulfill the request.

>[!NOTE]
>
>[!DNL API Mesh] will only send requests to third-party systems if you have customized your mesh configuration to do so.

**Step 5**: Requests sent to [!DNL Adobe Commerce as a Cloud Service] pass through a Web Application Firewall (WAF) that blocks suspicious or malicious requests. If the requested URL is cached at the [!DNL Commerce] CDN, it is delivered from that cache. If it is not cached, it is returned from one or more [!DNL Adobe Commerce as a Cloud Service] microservices (for example, foundation, search, and recommendations) and then cached for future requests.

**Step 5a**: If the request is sent to a third-party system, the response will be returned to [!DNL API Mesh].

**Step 5b**: If the request is for payment processing, the payment provider will render an iframe into the storefront for the shopper to securely enter the credit card information and complete the payment transaction.

**Step 6**: Once responses from [!DNL Adobe Commerce as a Cloud Service] or third-party services are received by [!DNL API Mesh], they are stitched together into a unified graph and returned to [!DNL Commerce Storefront] to serve the shopper's request.
