---
title: Automatic Matching
description: Learn how the out-of-the-box automatic matching enables seamless synchronization between Adobe Commerce and Product Visuals, ensuring that assets are automatically linked to the correct merchandising entities.
feature: CMS, Media, Integration
---
# Out-of-the-box automatic matching

The [!DNL Product Visuals] integration provides an out-of-the-box (OOTB) automatic matching mechanism based on the **AEM Assets** metadata configuration. This enables seamless synchronization between **Adobe Commerce** and **AEM Assets**, ensuring that product visuals are automatically linked to the correct merchandising entities.

See [AEM Assets metadata](configure-aem.md#configure-a-metadata-profile) for more information.

## Configure the OOTB automatic matching mechanism

1. Navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Specify **[!UICONTROL Match by SKU]** as the matching rule.

    ![ootb matching rule](./assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. Enter the metadata field name used for asset identification in the AEM Assets.

    >[!NOTE]
    >
    > If the standard onboarding process was followed, this value should be set to `commerce:skus`.

## How the OOTB automatic matching mechanism works

When this mechanism is configured, it automatically synchronizes Commerce asset files from AEM Assets to your Commerce project based on the asset metadata configured for each file. You configure the metadata from the AEM **Commerce** tab in the **AEM Assets author** environment:

![Example metadata](./assets/example-metadata.png){width="600" zoomable="yes"}

1. Define that the image is associated with `Commerce=yes`.

1. Associate assets with all products that share the same SKU.

1. Define the role and position for each asset as described in the metadata.

This approach ensures that digital assets are properly linked and displayed in Adobe Commerce. Also enables merchandisers and marketers to manage roles, as well as position directly in the AEM Assets, giving them a mechanism to maintain consistency in image selection and ordering across all engagement channels.
