---
title: Reference Architectures
description: Learn about reference architecture patterns for common Adobe Commerce implementations, such as storefronts, services, and catalog synchronization pipelines.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
---

# Reference architectures

The following patterns illustrate how Adobe Commerce products and services fit together for common implementation scenarios.

- [Adobe Commerce as a Cloud Service architecture](/help/cloud-service/overview.md#architecture)
- [Adobe Commerce enterprise reference architecture](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/architecture/enterprise-blueprint){target="_blank"}
- [Adobe Commerce storefront architecture](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/){target="_blank"}
- [Adobe Commerce on cloud infrastructure architecture](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/cloud-architecture){target="_blank"}

## Storefront powered by Edge Delivery Services

A storefront built on the Adobe Commerce boilerplate, using drop-in components and content blocks, connected to Adobe Commerce or [!DNL Adobe Commerce Optimizer] as the backend. See the [Adobe Commerce Storefront overview](https://experienceleague.adobe.com/developer/commerce/storefront/).

- [Adobe Commerce storefront architecture](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)

## Catalog sync pipeline

Data flow for keeping catalog, price, and inventory data synchronized between Adobe Commerce and Adobe Commerce services (Commerce Optimizer,Live Search, Catalog Service, Product Recommendations, and other connected [Commerce Services](../../landing/home.md)).

- For Adobe Commerce as a Cloud Service, on cloud infrastructure, or on-premises deployments, see [Synchronize data with SaaS Data Export](/help/data-export/sync-overview.md)

- For Adobe Commerce on cloud infrastructure or on-premises configured with Adobe Commerce Optimizer Connector, see [Connector sync pipeline](/help/aco-connector/connector-sync-pipeline.md).


## Related guidance

- [Implementation architectures options](implementation-architectures.md)
