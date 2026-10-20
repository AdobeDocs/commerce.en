---
title: Modernize an Existing Storefront
description: Learn how to plan an incremental migration from a legacy Adobe Commerce storefront to a storefront built on Edge Delivery Services and drop-in components.
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T11:09:14.812Z'
TQID: 'https://experienceleague.adobe.com/1OR7uwncjLw-NpwMMuwKjDjpASdh74sfu6s5rNClqxg'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---

# Modernize an existing storefront

If you're running a legacy storefront—such as a Luma theme or an older PWA Studio implementation—you can migrate incrementally to a storefront built on Edge Delivery Services and Commerce drop-in components, rather than rebuilding everything at once.

>[!NOTE]
>
>This guide applies to Adobe Commerce as a Cloud Service and Adobe Commerce on cloud infrastructure or on premises using either Storefront Services or the Adobe Commerce Optimizer Connector. It also applies to stand-alone Adobe Commerce Optimizer with an existing or third-party backend. See [Implementation architecture options](../architecture-options/implementation-architectures.md) to confirm which option applies to your project.

## Where to start

1. Review the [Adobe Commerce Storefront overview](https://experienceleague.adobe.com/developer/commerce/storefront/) to understand what a storefront built on Edge Delivery Services looks like compared to your current implementation.

1. Use the [Storefront Developer Guide](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) to scope which pages or flows to migrate first.

1. For Adobe Commerce as a Cloud Service, keep your existing Commerce services connections ([!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations], [!DNL Payment Services]) in place—see [Set up Commerce services](set-up-commerce-services.md).

## Related guidance

- [Build a new storefront](build-new-storefront.md)
- [Architecture options](../architecture-options/overview.md)
