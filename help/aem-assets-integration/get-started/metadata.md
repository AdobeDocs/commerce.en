---
title: Commerce metadata in AEM Assets
description: Learn about the Commerce namespace, metadata schema, and alternative text that the AEM Assets integration adds to your AEM Assets authoring environment.
feature: CMS, Media, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
---
# Commerce metadata in AEM Assets

When you use AEM Assets as a Digital Asset Management system (DAM) for Commerce, the AEM environment exposes a Commerce namespace, metadata schema, and a **[!UICONTROL Commerce]** tab so you can manage images and videos for Commerce products from the AEM authoring environment.

This topic describes the Commerce metadata resources that the integration adds. To configure them in your AEM project, see [Configure the AEM Assets project to support Commerce metadata](configure-aem.md).

## AEM Commerce assets-commerce package contents

Adobe provides an AEM Commerce package code `assets-commerce` to add Commerce namespace and Metadata Schema resources to the Experience Manager Assets as a Cloud Service environment configuration.

This package code adds the following resources to the AEM Assets authoring environment:

* A [custom namespace](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` to identify Commerce-related properties.

  * A custom metadata type `commerce:isCommerce` with the label `Eligible for Commerce` to tag Commerce assets associated with an Adobe Commerce project.

  * A custom metadata type `commerce:skus` and a corresponding UI component to add a **[!UICONTROL Product Data]** property. Product Data includes the metadata properties to associate a Commerce asset with product SKUs.

      ![Custom Product Data UI Control](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

  * A custom metadata type `commerce:roles` and `commerce:positions`  attributes to show how the asset is visualized in Commerce.

  * Alternative text multifield (_[!UICONTROL Alt texts]_) metadata so editors can enter alternative text keyed by Commerce store view code. This does not change how product images are assigned or scoped in the catalog. See [Localized alt text in AEM Assets metadata](#localized-alt-text-in-aem-assets-metadata).

* A metadata schema form with a Commerce tab that includes the `Eligible for Commerce` and `Product Data` fields for tagging Commerce assets. The form also provides options to show or hide the `roles` and `position` fields from the AEM Assets UI.

  ![Commerce tab for AEM Assets metadata schema form](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* A [sample tagged and approved Commerce asset](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` to support initial asset synchronization. Only approved Commerce assets can be synchronized from AEM Assets to Adobe Commerce.

>[!NOTE]
>
> See the [readme](https://github.com/ankumalh/assets-commerce) page on GitHub for more information about the **AEM Commerce package code**.

## Localized alt text in AEM Assets metadata

The _[!UICONTROL Alt texts]_ multifield is available in the AEM Assets asset metadata editor on the **[!UICONTROL Commerce]** tab when you edit an eligible image.

>[!IMPORTANT]
>
> Per-store view behavior applies to alternative text only. The AEM Assets integration does not synchronize different product images per Adobe Commerce store view. Product images from AEM continue to sync into Commerce with the same gallery assignment behavior as before this release.

The multifield contains one row per Commerce store view. Each row has two inputs:

* **[!UICONTROL Store View Code]** — The store view identifier (for example `default` or `en_US`).

* **[!UICONTROL Alt Text]** — Alternative text for that store view, limited to 255 characters.

Select **[!UICONTROL Add]** to add more rows for additional store views. To remove a row, select the **[!UICONTROL Delete]** icon on that row to remove it.

![Alt texts multifield with Store View Code and Alt Text inputs](../assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

When you save, client-side validation blocks submission if any row has an empty _[!UICONTROL Store View Code]_ or if two rows use the same store view code (case-insensitive).

Alternative text entries are persisted in JCR asset metadata as two index-aligned `String[]` properties:

* `commerce:altTextStoreViews`: Store view code for each row.
* `commerce:altTextValues`: Matching alt text at the same index as each entry in `commerce:altTextStoreViews`.

When these assets synchronize to Adobe Commerce, per-store view alt text is written to the product media gallery for the matching store view codes. The underlying image mapping is unchanged.
