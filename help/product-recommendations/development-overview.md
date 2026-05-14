---
title: Product Recommendations Administrator Development
description: An overview of Product Recommendations architecture and development features.
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
TQID: https://experienceleague.adobe.com/DtPYY7DaB-A7-VyTeXkjL9Y2My-WOQx-9CD-TgrcTmk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
---
# Product Recommendations Administrator Development

Product Recommendations are a powerful marketing tool you can use to increase conversions, boost revenue, and stimulate shopper engagement. Product Recommendations are surfaced on the storefront in the form of units such as "Customers who viewed this product also viewed", "Customers who bought this product also bought", "Recommended for you", and so on. Adobe Commerce Product Recommendations are powered by [Adobe AI](https://business.adobe.com/ai.html), which uses artificial intelligence and machine-learning algorithms to perform a deep analysis of aggregated shopper data. This data, when combined with your Commerce catalog, results in highly engaging, relevant, and personalized experiences for the shopper.

>[!NOTE]
>
>If your storefront is implemented using PWA Studio, refer to the [PWA documentation](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). If you use a custom frontend technology such as React or Vue JS, refer to the user guide to learn how to integrate Product Recommendations in a [headless](headless.md) environment. Headless instances must implement eventing to power the Product Recommendation workspace.

## Architectural overview

At a high level, Commerce Product Recommendations are deployed as SaaS. The Commerce side includes the storefront, which contains the event collector and recommendations layout template, and the backend, which includes the Data Services, SaaS Export module, and the Admin UI. Adobe AI intelligence services are leveraged on the SaaS side.

  ![Product recommendations architecture diagram](assets/arch-diag-sensei.svg)

Once the recommendation modules are installed and configured, your storefront will begin collecting behavioral data. Adobe AI processes this behavioral data along with your catalog data and calculates product associations that are leveraged by the recommendations service. At this point, the merchant can create, manage, and deploy product recommendation units to their storefront directly from the Admin UI.

## Next steps

Read the following topics to get started with Product Recommendations:

- [How to Implement Product Recommendations](implementation-workflow.md)

- [Install and configure Product Recommendations](install-configure.md)

- [Create Product Recommendations](create.md)
