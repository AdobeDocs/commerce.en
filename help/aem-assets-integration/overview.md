---
title: AEM Assets Integration for Commerce
description: Learn how to integrate Adobe Experience Manager Assets with your [!DNL Commerce] instance to create and manage the media files for your Commerce storefront.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
---
# AEM Assets Integration for Commerce

The demand for personalized content is rapidly increasing while marketing budgets are under pressure. Retailers and brands are struggling to keep pace with the growing need for variations in product imagery, driven by regional, seasonal, and segment-specific requirements.

Consider a retailer with 1,000 products. Even before factoring in attribute variations, the number of required digital assets expands significantly when considering different regions, customer segments, and personalization efforts. This can lead to an overwhelming number of asset variations, reaching into the millions.

![check](assets/product-visuals-example.png)

The AEM Assets Integration addresses this challenge by automating asset management workflows. The integration ensures that digital assets, such as product images and marketing content, are dynamically linked to the appropriate merchandising entities, including products and categories in Adobe Commerce, based on SKU or other key attributes. This process streamlines operations and enhances efficiency by enabling:

* **Seamless Installation and Configuration**– Merchandising teams and developers can quickly set up the integration using familiar Adobe tools and workflows.

* **Dynamic Asset Updates**-Product images and marketing assets automatically reflect the latest changes in AEM Assets, keeping storefronts accurate and relevant.

* **Streamlined Catalog Management**-Automates asset refresh and cleanup, minimizing manual effort and ensuring a consistent, well-maintained product catalog.

## Requirements to use the integration

>[!BEGINTABS]

>[!TAB Product Visuals powered by AEM Assets]

[![learn more](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB AEM Assets]

[![learn more](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

To leverage this integration, businesses must meet the following requirements:

* Active licenses for Adobe Commerce, Adobe Experience Manager Assets, and [AEM Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media).

* Adobe Commerce 2.4.5+

    * PHP 8.1, 8.2, 8.3, and 8.4

    * Composer 2.x

* Adobe Experience Manager is provisioned with [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/overview)

* The Adobe Commerce user configuring the integration must have access to the [IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) where the AEM Assets project is provisioned.

>[!BEGINSHADEBOX]

## Key business benefits

![check](assets/icon-check.png) **No Additional Cost**-This integration is provided free of charge for merchants who meet the licensing requirements.

![check](assets/icon-check.png) **Official Adobe Solution**-Developed, maintained, and fully supported by Adobe, ensuring stability and alignment with future platform enhancements.

![check](assets/icon-check.png) **Adobe Managed Support Model**-Assistance and troubleshooting are handled directly by Adobe, providing peace of mind and streamlined issue resolution.

>[!ENDSHADEBOX]

Watch this video to learn how Adobe Commerce and AEM Assets work together to streamline content workflows:

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

## Next steps

Enabling the Commerce integration with Experience Manager Assets is a three step process:

1. [Configure your AEM Assets project to support Commerce metadata](get-started/configure-aem.md).

1. [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} [Install Adobe Commerce packages](get-started/configure-commerce.md).

1. [Configure the integration](get-started/setup-synchronization.md).

## Support

If you need information or have questions not covered in this guide, contact your AEM Assets Integration sales representative or create a [support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to receive additional help.
