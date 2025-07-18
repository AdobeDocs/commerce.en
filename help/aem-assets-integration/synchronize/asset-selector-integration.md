---
title: Manual asset selection
description: Discover how the AEM Asset Selector integrated in the Commerce Admin helps marketers and merchandisers easily add images from AEM Assets to Adobe Commerce, streamlining asset management.
feature: CMS, Media, Integration
exl-id: 3c1f906f-3ec3-4eac-a47e-b21792767359
---
# Manual asset selection

The **AEM Asset Selector** enables marketers and merchandisers to easily add images from AEM Assets to Adobe Commerce, streamlining the asset management process. This method ensures brand consistency and compliance by limiting asset selection to those reviewed and approved in the [!DNL DAM (Digital Asset Management system)].

The **AEM Asset Selector** is available when the IMS client ID for the AEM Assets project has been configured in the Commerce Admin. See [Configure the AEM Asset Selector](#configure-the-aem-asset-selector-in-adobe-commerce).

When the **AEM Asset Selector** integration is configured, marketers and merchandisers can:

* Manage category images effortlessly, ensuring they align with brand and campaign guidelines.
* [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} Assign assets directly in Page Builder for visually rich content.
* [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."} Assign Assets directly in Commerce Storefront powered by Edge Delivery Services for visually enrich content.

>[!NOTE]
>
> The AEM Asset Selector is an AEM assets front-end component for integrating AEM Assets with authoring applications. For more information about this component, see the [Micro-Frontend Asset Selector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector){target=_blank} in the *AEM as a Cloud Service User Guide*.

## Key Benefits

Embedding AEM Asset Selector within the Adobe Commerce Admin Panel provides several key advantages:

* **Brand Consistency**–Displays only approved assets, minimizing the risk of outdated or non-compliant images on the storefront.

* **Efficiency**–Enables marketers and merchandisers to assign assets quickly without switching between different platforms.

* **Streamlined Collaboration**–Facilitates seamless teamwork by allowing direct image selection from the DAM, eliminating manual downloads and uploads.

* **Enhanced Content Quality**–Ensures the use of high-resolution, optimized images across product pages, categories, and Page Builder.

![Asset Selector](../assets/asset-selector.png){width="600" zoomable="yes"}

## Configure the AEM Asset Selector in Adobe Commerce

1. From the Commerce Admin, navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Fill in the **[!UICONTROL IMS Client ID]** field.

1. **Save** the configuration.

## Next steps

* [Manage Category Images with Asset Selector](../manage-assets.md#category-images)
* [Manage images in Page Builder content](../manage-assets.md#using-aem-asset-selector-in-page-builder)
