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

## Enable product-image display from AEM Assets {#enable-product-images}

The AEM Assets integration displays product images managed in AEM Assets instead of using images hosted in Adobe Commerce. The integration enables enhanced image management capabilities including advanced optimization, cropping, and delivery through Adobe's Content Delivery Network (CDN).

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

>[!TIP]
>
>To let authors browse and insert AEM assets into static content pages, see [Connect AEM Assets to Da.live for static content authoring](#connect-aem-assets-authoring).

## Connect AEM Assets to Da.live for static content authoring {#connect-aem-assets-authoring}

>[!NOTE]
>
>This setup is **separate from the AEM Assets Integration extension**. It is provided by [Da.live](https://da.live){target=_blank} out-of-the-box and applies only when authors need to browse and insert AEM assets into **static content pages** (for example, landing pages or content blocks) through the **[!UICONTROL Library]** panel and **[!UICONTROL Content Advisor]**. Product images synchronized through the AEM Assets Integration are configured separately using the `commerce-assets-enabled` setting described above.

Use the following steps to connect AEM Assets to a storefront authored in Document Authoring (Da.live). After you connect, authors can browse and insert AEM assets directly from the **[!UICONTROL Content Advisor]** when editing static content.

These steps summarize the [Da.live](https://da.live){target=_blank} setup. For the complete reference, see [Setup AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} in the Da.live documentation and [Integrate AEM Assets while authoring content for Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services){target=_blank} in the AEM Assets documentation.

### Step 1: Open your site config in Da.live

1. Go to [Da.live](https://da.live){target=_blank} and locate your storefront. Double-click it to open.

1. In the breadcrumb, click settings to open your site config spreadsheet.

### Step 2: Copy your AEM repository URL

1. In a new tab, go to [experience.adobe.com](https://experience.adobe.com){target=_blank} and navigate to **[!UICONTROL Experience Manager]**.

1. Scroll to the **[!UICONTROL My Authoring]** section and select **[!UICONTROL Assets]** next to your **[!UICONTROL Production]** environment to open Adobe Experience Manager Assets.

1. From the browser address bar, copy the segment that starts with `author` up to and including `.com`—for example, `author-p107634-e1009805.adobeaemcloud.com`.

### Step 3: Add the repository ID to your config

1. Return to Da.live and select **[!UICONTROL data]** in your site config.

1. Complete the spreadsheet as follows:

   | Cell | Value |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | The URL that you copied in Step 2 |

1. Select **[!UICONTROL Save]**, then select the back arrow next to your site name to return to the site root.

   >[!NOTE]
   >
   > The `author-` prefixed host browses assets from the author tier. To deliver assets through Dynamic Media instead, use a `delivery-` prefixed host. For all `aem.repositoryId` options, see [Setup AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}.

### Step 4: Connect AEM Assets through the Library

1. From the site root, select the **[!UICONTROL index]** folder to open it.

1. In the editor, open the **[!UICONTROL Library]** panel and select **[!UICONTROL AEM Assets]**.

   The **[!UICONTROL Content Advisor]** popover opens and shows your AEM Assets folders and files.

Your storefront is now connected to AEM Assets. You can browse and insert assets directly from the **[!UICONTROL Content Advisor]**.

## Related documentation

* [AEM Assets integration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/){target=_blank} in the *Adobe Commerce Storefront* documentation—storefront configuration and image-handling behavior.

* [Integrate AEM Assets while authoring content for Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services){target=_blank} in the *AEM Assets* documentation.

* [Setup AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} and [Working with media](https://docs.da.live/authors/guides/adding-media){target=_blank} in the Da.live documentation.
