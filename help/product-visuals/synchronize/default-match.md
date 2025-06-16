---
title: Default automatic matching
description: Learn how the out-of-the-box automatic matching enables seamless synchronization between Adobe Commerce and Product Visuals, ensuring that assets are automatically linked to the correct merchandising entities.
feature: CMS, Media, Integration
---

# Default automatic matching

The [!DNL Product Visuals] integration provides a default automatic matching mechanism (**[!UICONTROL Match by product SKU]**) based on the **AEM Assets** metadata configuration. This rule enables seamless synchronization between **Adobe Commerce** and **AEM Assets**, ensuring that product visuals are automatically linked to the correct merchandising entities.

See [AEM Assets metadata](configure-aem.md#configure-a-metadata-profile) for more information.

## Configure the automatic matching mechanism

1. Navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Specify **[!UICONTROL Match by SKU]** as the matching rule.

    ![default automated matching rule](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. Enter the metadata field name used for asset identification in the AEM Assets.

    >[!NOTE]
    >
    > If the standard onboarding process was followed, this value should be set to `commerce:skus`.

## How the automatic matching mechanism works

When the **[!UICONTROL Match by product SKU]** matching rule is configured  in the Commerce Admin, Commerce assets files synchronize automatically from AEM Assets to your Commerce project based on the asset metadata configured for each file. You configure the metadata from the AEM **Commerce** tab in the **AEM Assets author** environment:

![Example metadata](../assets/example-metadata.png){width="600" zoomable="yes"}

1. In AEM Assets, update the image metadata to add the Adobe Commerce association, `Commerce=yes`.

1. Configure the metadata ([!UICONTROL SKU], [!UICONTROL position], and [!UICONTROL role]) that links the asset to the associated product SKU.

    >[!NOTE]
    >
    > If an asset is used for multiple products, configure the metadata for each associated SKU.  

This approach ensures that digital assets are properly linked and displayed in Adobe Commerce. It also empowers merchandisers and marketers to manage roles and asset positioning directly within AEM Assets, providing a consistent and centralized mechanism for image selection and ordering across all engagement channels.
