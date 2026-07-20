---
title: Security architecture and data flow
description: Learn about the security architecture and data flow for Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
autotag-review: '2026-06-18T16:16:18.600Z'
TQID: 'https://experienceleague.adobe.com/2yK-VVec98nFH9LPpfSe4kQ2YvQr2yy3G0Rym5-HCbI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
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

**Step 5b**: If the request is for payment processing, the payment provider renders an iframe into the storefront for the shopper to securely enter the credit card information and complete the payment transaction.

**Step 6**: Once responses from [!DNL Adobe Commerce as a Cloud Service] or third-party services are received by [!DNL API Mesh], they are stitched together into a unified graph and returned to [!DNL Commerce Storefront] to serve the shopper's request.
