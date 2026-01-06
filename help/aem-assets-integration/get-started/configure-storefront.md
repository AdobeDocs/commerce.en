---
title: Configure your Storefront
description: Learn how to connect your Edge Delivery Services storefront to your AEM Assets integration.
feature: CMS, Media, Integration
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
