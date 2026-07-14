---
title: AEM Assets Integration for Commerce
description: Learn how to integrate Adobe Experience Manager Assets with your [!DNL Commerce] instance to create and manage the media files for your Commerce storefront.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
TQID: https://experienceleague.adobe.com/CTDmM7Ox2rQ-55F1BVTg-C8DPBEuEpzFxXGtWpnjXKs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
    internal-label: Categories
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# AEM Assets Integration for Commerce

The demand for personalized content is rapidly increasing while marketing budgets are under pressure. Retailers and brands are struggling to keep pace with the growing need for variations in product imagery, driven by regional, seasonal, and segment-specific requirements.

Consider a retailer with 1,000 products. Even before factoring in attribute variations, the number of required digital assets expands significantly when considering different regions, customer segments, and personalization efforts. This can lead to an overwhelming number of asset variations, reaching into the millions.

![overview](assets/product-visuals-example.png){width="700" zoomable="yes"}

The AEM Assets Integration addresses this challenge by automating asset management workflows. The integration ensures that digital assets, such as product images and marketing content, are dynamically linked to the appropriate merchandising entities, including products and categories in Adobe Commerce, based on SKU or other key attributes. This process streamlines operations and enhances efficiency by enabling:

* **Seamless Installation and Configuration**– Merchandising teams and developers can quickly set up the integration using familiar Adobe tools and workflows.

* **Dynamic Asset Updates**-Product images and marketing assets automatically reflect the latest changes in AEM Assets, keeping storefronts accurate and relevant.

* **Streamlined Catalog Management**-Automates asset refresh and cleanup, minimizing manual effort and ensuring a consistent, well-maintained product catalog.

## Requirements to use the integration

To leverage this integration either with [Product Visuals or AEM Assets](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets), businesses must meet the following requirements:

>[!BEGINTABS]

>[!TAB Product Visuals]

[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."}  Active licenses for Adobe Commerce, Product Visuals powered by AEM Assets, and [AEM Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) (These licenses are available out-of-the-box with [!DNL Adobe Commerce as a Cloud Service] and [!DNL Adobe Commerce Optimizer]).

>[!TAB AEM Assets]

[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."} Active licenses for Adobe Commerce, Adobe Experience Manager Assets, and [AEM Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media).

[!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} Adobe Commerce 2.4.5+

* PHP 8.1, 8.2, 8.3, and 8.4

* Composer 2.x

[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."} Adobe Experience Manager is provisioned with [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/overview)

>[!ENDTABS]

The Adobe Commerce user configuring the integration must have access to the [IMS Organization](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) where the AEM Assets project is provisioned.

>[!BEGINSHADEBOX]

## Key business benefits

![check](assets/icon-check.png) **No Additional Cost**-This integration is provided free of charge for merchants who meet the licensing requirements.

![check](assets/icon-check.png) **Official Adobe Solution**-Developed, maintained, and fully supported by Adobe, ensuring stability and alignment with future platform enhancements.

![check](assets/icon-check.png) **Adobe Managed Support Model**-Assistance and troubleshooting are handled directly by Adobe, providing peace of mind and streamlined issue resolution.

![check](assets/icon-check.png) **Adobe Storefront Builder capabilities**-The digital asset management (DAM) solution allows the use of assets like images, videos, and other media on the [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/#userlabs-commerce-genai-product-visuals).

>[!ENDSHADEBOX]

## Tutorial

Watch these videos to learn how to set up and use the AEM Assets integration with Adobe Commerce.

>[!BEGINTABS]

>[!TAB Adobe Commerce on Cloud or On-Premises Tutorial]

Watch this video to learn how Adobe Commerce and AEM Assets work together to streamline content workflows:

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

>[!TAB Adobe Commerce as a Cloud Service Tutorial]

Learn how to use Adobe Commerce as a Cloud Service with the AEM Assets integration.

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## Next steps

The process to install and configure the AEM Assets integration depends on your Adobe Commerce deployment. In all cases, you first configure AEM Assets, then connect Commerce to it.

Before you begin, review [Commerce metadata in AEM Assets](metadata.md) to understand the namespace, metadata schema, and **[!UICONTROL Commerce]** tab that the integration adds to your AEM Assets environment.

Select your deployment to follow the required steps in order:

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE SaaS only]{type=Positive tooltip="Applies to Adobe Commerce as a Cloud Service projects only (Adobe-managed SaaS infrastructure)."}

1. [Configure the AEM Assets project to support Commerce metadata](get-started/configure-aem.md). On AEM release `2026.5.26309` and later, use the [self-service onboarding](get-started/configure-aem.md#enable-aem-commerce-self-service); on earlier releases, install the `assets-commerce` package manually.

1. [Configure IMS user permissions](get-started/permissions.md) so the Asset Selector and the auto-populated **[!UICONTROL Program ID]** and **[!UICONTROL Environment ID]** fields are available.

1. [Configure the integration in the Commerce Admin](get-started/setup-synchronization.md).

1. Optional. [Enable product-image display](get-started/configure-storefront.md#enable-product-images) so a storefront powered by Edge Delivery Services renders AEM-managed product images.

>[!TAB Adobe Commerce on Cloud (PaaS)]

[!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}

1. [Configure the AEM Assets project to support Commerce metadata](get-started/configure-aem.md). On AEM release `2026.5.26309` and later, use the [self-service onboarding](get-started/configure-aem.md#enable-aem-commerce-self-service); on earlier releases, install the `assets-commerce` package manually.

1. [Install Adobe Commerce packages](get-started/configure-commerce.md) to add the extension and generate the required credentials and connections.

1. [Configure IMS user permissions](get-started/permissions.md) so the Asset Selector and the auto-populated **[!UICONTROL Program ID]** and **[!UICONTROL Environment ID]** fields are available.

1. [Configure the integration in the Commerce Admin](get-started/setup-synchronization.md).

1. Optional. [Enable product-image display](get-started/configure-storefront.md#enable-product-images) so a storefront powered by Edge Delivery Services renders AEM-managed product images.

>[!TAB Adobe Commerce Optimizer]

[!BADGE SaaS only]{type=Positive tooltip="Applies to Adobe Commerce Optimizer projects only."}

[!DNL Adobe Commerce Optimizer] has no Admin configuration UI. Adobe Support configures the integration from your onboarding ticket, so prepare AEM Assets first.

1. [Configure the AEM Assets project to support Commerce metadata](get-started/configure-aem.md). On AEM release `2026.5.26309` and later, use the [self-service onboarding](get-started/configure-aem.md#enable-aem-commerce-self-service); on earlier releases, install the `assets-commerce` package manually.

1. [Submit the onboarding support ticket](get-started/configure-aco.md#onboarding) with your tenant ID, AEM Program ID, AEM Environment ID, matching rule, layer, and locale.

1. [Configure your catalog view](get-started/configure-aco.md#onboarding) with the same locale and layer that you registered in the ticket.

1. Optional. [Enable product-image display](get-started/configure-storefront.md#enable-product-images) so a storefront powered by Edge Delivery Services renders AEM-managed product images.

   For the full procedure, limitations, and layer guidance, see [Configure AEM Assets for Commerce Optimizer](get-started/configure-aco.md).

>[!ENDTABS]

## Support

If you need information or have questions not covered in this guide, contact your AEM Assets Integration sales representative or create a [support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to receive additional help.
