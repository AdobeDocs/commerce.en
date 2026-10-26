---
title: Commerce Architecture Overview
description: Learn about the Adobe Commerce product model and where to find detailed architecture options, storefront, and API guidance.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
---

# Commerce architecture overview

Adobe Commerce architectures generally combine three layers: a commerce backend ([!DNL Adobe Commerce] or [!DNL Adobe Commerce Optimizer]), a storefront, and a set of connected services and integrations. This section orients you to the product model and points you to the detailed comparisons, diagrams, and API references maintained in each dedicated page.

## Getting started

| Section | Use it to |
| ------- | --------- |
| [Platforms and services](../portfolio/platform-and-services.md) | Understand what each Commerce product is—Adobe Commerce, Commerce Foundation, Adobe Commerce Optimizer, and Adobe Commerce as a Cloud Service. |
| [Choose a Commerce option](../portfolio/choose-commerce-option.md) | Compare Commerce options based on transaction ownership, deployment model, and merchandising needs. |
| [Architecture options](../architecture-options/implementation-architectures.md) | Compare all four supported architectures in detail, including system diagrams and reference links. |
| [Storefronts](../storefronts/overview.md) | Understand storefront options and how they connect to each architecture. |
| [APIs](../apis/commerce-apis.md) | Compare the API families used across Commerce Foundation, Storefront Services, and Commerce Optimizer. |
| [AEM Assets integration for Commerce](../aem-assets/aem-assets-integration.md) | Add centralized digital asset management to any Commerce or Optimizer architecture. |
| [Migration and adoption](../migration-adoption/overview.md) | Plan a move between architectures or a phased adoption of Adobe Commerce Optimizer. |

## Terminology quick reference

| Preferred term | Meaning | Avoid using as a current architecture label |
| --- | --- | --- |
| **Commerce Foundation** | Base commerce and transactional capabilities | Core Commerce and PHP Foundational Layer |
| **Storefront Services** | Storefront-oriented APIs for Catalog Service, Live Search, and Product Recommendations | A label limited to only one Commerce platform |
| **Commerce Optimizer Merchandising Services** | Optimizer APIs for catalog discovery and merchandising experiences | Commerce Foundation APIs |
| **Commerce Storefront powered by Edge Delivery Services** | Customer-facing storefront implementation | An API family |

## Related guidance

- [Implementation architectures](implementation-architectures.md)
- [Reference architectures](reference-architectures.md)
- [Build a new storefront](../implementation-guides/build-new-storefront.md)
