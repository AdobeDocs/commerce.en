---
title: '[!DNL Page Builder] Integration'
description: Learn how to use [!DNL Product Recommendations] units in Page Builder.
feature: Services, Recommendations, Page Builder
exl-id: 001e8e1d-3590-4b44-b5f8-dd8b9b61f370
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# [!DNL Page Builder] Integration

Product Recommendations can be integrated within any Page Builder content that you deploy on your site.

>[!NOTE]
>
> You can have up to 25 recommendation units on a native Page Builder page. Non-native Page Builder pages can have up to 5 recommendation units. See [Create New Recommendation](create.md) for more information.

## Using Product Recommendations with Page Builder content

1. Create a Recommendation unit in the default store view of a website. They must be created in the default store view even if you plan to use them in different store views.

    >[!NOTE]
    >
    >Metrics for Page Builder recommendation units only appear on the default store view [!DNL Product Recommendations] workspace. Even if you place a Page Builder recommendation unit on a store view that is not the default store view, metrics related to those Page Builder recommendation units will not display on the non-default store view [!DNL Product Recommendations] workspace. To see Page Builder metrics on a non-default store view [!DNL Product Recommendations] workspace, open and [edit](edit.md) the Page Builder recommendation unit in the non-default store view, then click [!UICONTROL **Save**]. The Page Builder metrics now appear on the [!DNL Product Recommendations] workspace under the non-default storeview.

1. In Page Builder, select the Product Recommendations content widget and place on your site. 

![Insert Recommendation unit](assets/pb-insert.png)

1. Click **Edit Product Recommendation**
1. Click **Select**
1. Select your previously created Recommendation unit and click **Add Selected**

![Insert Recommendation unit](assets/pb-select.png)

1. Make any other edits to the Page Builder content and save your changes. 

At render time, the context and scope of the Page Builder content is respected by the Recommendation unit.
