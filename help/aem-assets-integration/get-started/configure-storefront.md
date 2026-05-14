---
title: Configure your Storefront
description: Learn how to connect your Edge Delivery Services storefront to your AEM Assets integration.
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
---
# Configure your Storefront

The AEM Assets integration displays product images managed in AEM Assets instead of using images hosted in Adobe Commerce. The integration enables enhanced image management capabilities including advanced optimization, cropping, and delivery through Adobe’s Content Delivery Network (CDN).

To enable the integration in Commerce storefronts powered by Edge Delivery Services, update the storefront configuration file (`config.json`) to add the `"commerce-assets-enabled": true` parameter.

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

The Commerce drop-ins automatically detect the `commerce-assets-enabled` configuration and adjust image handling accordingly.

For more information on how to use AEM Assets with the Commerce Storefront powered by Edge Delivery Services, complete the storefront configuration described in the [AEM Assets integration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) topic in the *Adobe Commerce Storefront* documentation.
