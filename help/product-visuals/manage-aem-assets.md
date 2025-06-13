---
title: Manage Product Visuals powered by AEM Assets
description: Use Product Visuals with AEM Assets to manage media assets for your storefront.
feature: CMS, Media
---

# Manage Commerce media assets with Product Visuals powered by AEM Assets

<!--In ACAP-844, this topic was linked to from the Commerce Admin products images and videos when the Assets integration is enabled. If the URL to the topic changes, be sure to add a redirect.-->

Adobe Commerce allows merchants to associate images with product categories, helping create a visually engaging storefront. Our integration leverages AEM Asset Selector, enabling marketers to seamlessly select images directly from the AEM Assets digital asset management system (DAM). This ensures that only approved images are used and eliminates the need to store them in Adobe Commerce, maintaining consistency and efficiency across all engagement channels.

## Update an asset

After you edit an asset in AEM Assets, send the updates to Commerce by approving and reprocessing the asset. Only approved assets are sent to your Commerce instance. Reprocessing the asset ensures that any final changes or metadata updates are captured before the asset is sent to Adobe Commerce.

For details, see the following AEM Assets documentation.

- [Reprocessing digital assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing)

- [Approve an asset](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/approve-assets)

## Using AEM Asset Selector for Category Images

To update a category image using AEM Asset Selector:

After you have enabled and configured the AEM Assets integration, you can  add assets into your catalog categories content by using the AEM assets selector now available in the Commerce Admin.

1. On the _Admin_ sidebar, navigate to **[!UICONTROL Catalog]** > **[!UICONTROL Categories]**.

1. Select a category you want to update.

1. Expand the ![Expansion selector](../assets/icon-display-expand.png) in the **[!UICONTROL Content]** section.

1. In the **[!UICONTROL Content]** section, locate the *Image field* associated with the category.

   ![Category content](./assets/category-asset.png){width="600" zoomable="yes"}

1. Click **[!UICONTROL Select from Assets]** to change the category image.

   ![Category content](./assets/asset-view.png){width="600" zoomable="yes"}

1. Choose an image from the AEM Asset Selector.

   ![Category content](./assets/select-image.png){width="600" zoomable="yes"}

1. Click **[!UICONTROL Save]** and continue.

   For more information about creating a category, see [Complete the category content](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/create/category-create#step-3-complete-the-category-content).
