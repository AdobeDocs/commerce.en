---
title: Choose a Commerce Option
description: Compare Adobe Commerce architectures based on transaction ownership, deployment model, and merchandising needs.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
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
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
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
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---

# Choose a Commerce option

Start by identifying which system owns cart, checkout, orders, and other transactions. Then, choose the merchandising path that fits that backend.

## Questions to guide your decision

Use the following questions to identify which options to evaluate. Consider your existing commerce backend, how much infrastructure responsibility you want to retain, and whether you need to improve product discovery and merchandising. Adobe Commerce Optimizer provides discovery and merchandising capabilities. It does not replace the backend that handles transactions.

1. **Do you want Adobe to manage the Commerce platform as software as a service (SaaS)?**
   - Yes: Evaluate Adobe Commerce as a Cloud Service.
   - No: If you need Adobe Commerce and want to retain control over your cloud or on-premises infrastructure, evaluate Adobe Commerce on Cloud or on premises.
1. **Do you need Adobe Commerce to handle cart, checkout, orders, and other transactions?**
   - Yes: Evaluate Adobe Commerce on Cloud or on premises, or Adobe Commerce as a Cloud Service. These options use Commerce Foundation as the transactional backend.
   - No: Retain your existing or third-party transactional backend. If you also need Adobe discovery and merchandising capabilities, evaluate stand-alone Adobe Commerce Optimizer.
1. **Do you want to use Adobe Commerce Optimizer to improve product discovery and merchandising with your existing third-party commerce backend?**
   - Yes: Evaluate stand-alone Adobe Commerce Optimizer while retaining your third-party backend for transactions.
1. **Do you already operate Adobe Commerce on Cloud or on premises and want stronger discovery and merchandising?**
   - Yes: Evaluate the Adobe Commerce Optimizer Connector to synchronize catalog and pricing data while Adobe Commerce continues to handle transactions.

Use the comparison table below to match your answers to a starting point. For detailed system diagrams, see [Architecture options](../architecture-options/overview.md).

## Compare Commerce options

| Your requirement | Recommended starting point | System that owns transactions | Merchandising and discovery |
| --- | --- | --- | --- |
| Adobe manages the Commerce platform as SaaS. | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service Foundation | Use the Commerce services provisioned for Adobe Commerce as a Cloud Service. For Adobe Commerce Optimizer integration availability, see the note below this table. |
| Need Adobe Commerce and want to retain control over your cloud or on-premises infrastructure. | [Adobe Commerce on Cloud or on premises](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview) | Adobe Commerce Foundation | Use supported Commerce services as needed. |
| On Adobe Commerce on Cloud or on premises and want to adopt Adobe Commerce Optimizer for discovery and merchandising. | Adobe Commerce with the [Adobe Commerce Optimizer Connector](/help/aco-connector/overview.md) | Adobe Commerce remains the system of record for transactions. | The connector syncs catalog and pricing data to Adobe Commerce Optimizer which provides discovery and merchandising experiences. |
| Have a third-party commerce backend and want Adobe Commerce Optimizer discovery and merchandising without replacing that backend. | Stand-alone [Adobe Commerce Optimizer](/help/optimizer/overview.md) | Your third-party commerce backend | Send catalog and price data to Adobe Commerce Optimizer. Integrate cart, checkout, and other transactional operations with the backend through API Mesh, App Builder, or a direct integration. |

>[!NOTE]
>
>An integration between Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer is on the Commerce roadmap. If you need both platforms, plan to use them as separate architecture options for now. Contact your Adobe account manager to learn more about the timeline for the integration.

## Related guidance

- [Platforms and services](platform-and-services.md)
- [Architecture options](../architecture-options/overview.md)
- [Get started](../get-started/get-started-by-role.md)
