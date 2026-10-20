---
title: AEM Assets Integration for Commerce
description: Learn to integrate AEM Assets with Adobe Commerce, Adobe Commerce as a Cloud Service, and Adobe Commerce Optimizer to manage product images and media centrally.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---

# AEM Assets integration for Commerce

The AEM Assets integration enables Product Visuals capabilities in Adobe Commerce so you can manage product images, videos, and other media centrally in AEM Assets. It is an optional add-on that works with any Commerce architecture option, not a separate Commerce platform.

## Integration paths by architecture

There are two integration paths. The path depends on your Commerce architecture.

| Commerce architecture | AEM Assets integration path | Learn more |
| --- | --- | --- |
| [!DNL Adobe Commerce] on Cloud or on premises | [!DNL AEM Assets] Integration for Commerce. Uses the Commerce integration package to synchronize and manage product images, videos, and other media between [!DNL Adobe Commerce] and [!DNL AEM Assets]. | [AEM Assets Integration for Commerce](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL Product Visuals] powered by [!DNL AEM Assets] | [AEM Assets integration setup](/help/aem-assets-integration/overview.md#next-steps) |
| Stand-alone [!DNL Adobe Commerce Optimizer] | [!DNL Product Visuals] powered by [!DNL AEM Assets]. Base catalog and price data arrive through the [Optimizer Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/). | [Product Visuals with AEM Assets](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce] with the [!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals] powered by [!DNL AEM Assets]. Catalog and price data are synchronized from [!DNL Adobe Commerce] by the Connector. | [Commerce Optimizer Integrations](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals] is the integration path for Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer. It synchronizes AEM-managed product imagery to the Commerce catalog layer and delivers it to storefront experiences through storefront APIs.

## Before you choose

- Setup and licensing requirements differ between the Commerce on cloud or on-premises path and the Commerce as a Cloud Service or Adobe Optimizer [!DNL Product Visuals] path. Review the deployment-specific requirements first.
- [!DNL AEM Assets] manages digital assets. It doesn't replace the Commerce catalog, pricing, cart, checkout, or order system.
- Product assets are matched to Commerce products using SKU or other documented matching metadata.
- If marketing and merchandising teams need centralized product imagery and asset workflows, choose the path that matches your Commerce architecture.

## Related information

- [Adobe Experience Manager Assets documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/overview)
- [Architecture overview](../architecture-options/overview.md)
- [APIs](../apis/commerce-apis.md)
