---
title: AEM Assets Integration for Commerce
description: Learn how AEM Assets integrates with each Adobe Commerce architecture, including Adobe Commerce, Adobe Commerce as a Cloud Service, and Adobe Commerce Optimizer.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
---

# AEM Assets integration for Commerce

AEM Assets is an optional digital asset management integration that can be added to any [Commerce architecture option](../architecture-options/overview.md). Treat it as a cross-cutting capability, not as a separate Commerce platform option.

## AEM Assets with Adobe Commerce on Cloud or on premises

[!DNL AEM Assets] Integration for Commerce uses the Commerce integration package and the documented PaaS/on-premises setup path. It synchronizes and manages product images, videos, and other media between [!DNL Adobe Commerce] and [!DNL AEM Assets]. See [AEM Assets Integration for Commerce](/help/aem-assets-integration/overview.md).

## Product Visuals with AEM Assets

[!DNL Product Visuals] powered by [!DNL AEM Assets] is the SaaS integration path for AEM-managed product imagery. Before choosing an integration path, keep in mind:

- Setup and licensing requirements differ between the PaaS/on-premises integration path and the SaaS Product Visuals path.
- [!DNL AEM Assets] manages digital assets; it doesn't replace the Commerce catalog, pricing, cart, checkout, or order system.
- Product assets are matched to Commerce products using SKU or other documented matching metadata.
- For Optimizer architectures, imagery can be synchronized as a catalog layer and exposed through storefront APIs.

Review the deployment-specific requirements before choosing an integration path. See [Product Visuals with AEM Assets](/help/optimizer/setup/product-visuals.md).

## AEM Assets with Adobe Commerce as a Cloud Service

[!DNL Product Visuals] powered by [!DNL AEM Assets] synchronizes AEM-managed product imagery to the Commerce catalog layer, delivered through storefront experiences on [!DNL Adobe Commerce as a Cloud Service]. See [Product Visuals with AEM Assets](/help/optimizer/setup/product-visuals.md).

## AEM Assets with Adobe Commerce and the Optimizer Connector

[!DNL Product Visuals] with [!DNL AEM Assets] for [!DNL Adobe Commerce Optimizer] synchronizes product imagery to Optimizer and applies it as catalog-layer data for storefront experiences, alongside the catalog and price data synchronized by the [!DNL Adobe Commerce Optimizer Connector]. See [Commerce Optimizer Integrations](/help/optimizer/integrations/integrations-overview.md).

## AEM Assets with Commerce Optimizer

For stand-alone [!DNL Adobe Commerce Optimizer], [!DNL Product Visuals] with [!DNL AEM Assets] manages product imagery while the base catalog and price data arrive through the Optimizer Data Ingestion API. See [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).

## Choosing an integration path

If marketing and merchandising teams need centralized product imagery and asset workflows, evaluate the AEM Assets integration path that corresponds to your selected Commerce architecture.

| Customer situation | Starting point |
| --- | --- |
| Centralized product-media management across Commerce experiences | Architecture-specific AEM Assets integration |

## Documentation map

- [AEM Assets Integration for Commerce](/help/aem-assets-integration/overview.md)
- [Product Visuals with AEM Assets](/help/optimizer/setup/product-visuals.md)
- [Commerce Optimizer Integrations](/help/optimizer/integrations/integrations-overview.md)
- [Adobe Experience Manager Assets documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/overview)

## Related guidance

- [Architecture options](../architecture-options/overview.md)
- [APIs](../apis/overview.md)
