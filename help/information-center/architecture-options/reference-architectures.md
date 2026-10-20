---
title: Reference Architectures
description: Learn about reference architecture patterns for common Adobe Commerce implementations, such as storefronts, services, and catalog synchronization pipelines.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T11:42:09.021Z'
TQID: 'https://experienceleague.adobe.com/GVbGyRZz8llMWcUykcXXZwWnTaAomHVCTcV3ft49IEc'
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
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
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

# Reference architectures

The following documentation provides reference architecture patterns for Adobe Commerce platforms and services across different deployment models and use cases.

- [Adobe Commerce as a Cloud Service architecture](/help/cloud-service/overview.md#architecture)
- [Adobe Commerce enterprise reference architecture](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/architecture/enterprise-blueprint){target="_blank"}
- [Adobe Commerce storefront architecture](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/){target="_blank"}
- [Adobe Commerce on cloud infrastructure architecture](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/cloud-architecture){target="_blank"}

## Storefront powered by Edge Delivery Services

A storefront built on the Adobe Commerce boilerplate, using drop-in components and content blocks, connected to Adobe Commerce or [!DNL Adobe Commerce Optimizer] as the backend. See the [Adobe Commerce Storefront overview](https://experienceleague.adobe.com/developer/commerce/storefront/).

- [Adobe Commerce storefront architecture](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)

## Catalog sync pipeline

Data flow for keeping catalog, price, and inventory data synchronized between Adobe Commerce and Adobe Commerce services (Commerce Optimizer, Live Search, Catalog Service, Product Recommendations, and other connected [Commerce Services](../../landing/home.md)).

- For Adobe Commerce as a Cloud Service, on cloud infrastructure, or on-premises deployments, see [Synchronize data with SaaS Data Export](/help/data-export/sync-overview.md)

- For Adobe Commerce on cloud infrastructure or on-premises configured with Adobe Commerce Optimizer Connector, see [Connector sync pipeline](/help/aco-connector/connector-sync-pipeline.md).


## Related guidance

- [Implementation architectures](implementation-architectures.md)
