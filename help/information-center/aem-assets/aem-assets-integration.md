---
title: AEM Assets Integration for Commerce
description: Learn how AEM Assets integrates with each Adobe Commerce architecture, including Adobe Commerce, Adobe Commerce as a Cloud Service, and Adobe Commerce Optimizer.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
---

# AEM Assets integration for Commerce

The AEM Assets integration enables Product Visuals capabilities in Adobe Commerce so you can manage product images, videos, and other media centrally in AEM Assets. It is an optional add-on that works with any Commerce architecture option, not a separate Commerce platform.

## Integration paths by architecture

There are two integration paths. The path depends on your Commerce architecture.

| Commerce architecture | AEM Assets integration path | Learn more |
| --- | --- | --- |
| [!DNL Adobe Commerce] on Cloud or on premises (PaaS) | [!DNL AEM Assets] Integration for Commerce. Uses the Commerce integration package to synchronize and manage product images, videos, and other media between [!DNL Adobe Commerce] and [!DNL AEM Assets]. | [AEM Assets Integration for Commerce](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL Product Visuals] powered by [!DNL AEM Assets] | [Product Visuals with AEM Assets](/help/optimizer/setup/product-visuals.md) |
| Stand-alone [!DNL Adobe Commerce Optimizer] | [!DNL Product Visuals] powered by [!DNL AEM Assets]. Base catalog and price data arrive through the [Optimizer Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/). | [Product Visuals with AEM Assets](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce] with the [!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals] powered by [!DNL AEM Assets]. Catalog and price data are synchronized from [!DNL Adobe Commerce] by the Connector. | [Commerce Optimizer Integrations](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals] is the SaaS integration path. It synchronizes AEM-managed product imagery to the Commerce catalog layer and delivers it to storefront experiences through storefront APIs.

## Before you choose

- Setup and licensing requirements differ between the PaaS/on-premises path and the SaaS [!DNL Product Visuals] path. Review the deployment-specific requirements first.
- [!DNL AEM Assets] manages digital assets. It doesn't replace the Commerce catalog, pricing, cart, checkout, or order system.
- Product assets are matched to Commerce products using SKU or other documented matching metadata.
- If marketing and merchandising teams need centralized product imagery and asset workflows, choose the path that matches your Commerce architecture.

## Related information

- [Adobe Experience Manager Assets documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/overview)
- [Architecture implementation options](../architecture-options/implementation-architectures.md)
- [APIs](../apis/commerce-apis.md)
