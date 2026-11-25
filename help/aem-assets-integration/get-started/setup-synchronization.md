---
title: Configure the integration
description: Learn how to connect your Adobe Commerce project and Experience Manager Assets projects to enable asset synchronization between these two systems.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
TQID: 'https://experienceleague.adobe.com/MM-neGrH-N8xBcCwLgnsaIrIjhbX6uYL5kS41QdV79I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Configure the integration

Configure the integration by connecting Commerce to the AEM Assets instance and selecting the matching strategy for asset synchronization.

After identifying the AEM Assets project, select the matching rule for synchronizing assets between Adobe Commerce and AEM Assets.

* **[!UICONTROL Match by product SKU]**—Default rule that matches the SKU in the asset metadata with the [Commerce product SKU](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku) to ensure that assets are associated with the correct products.

* **[!UICONTROL Custom match]**—Matching rule for more complex scenarios or specific business requirements that require custom matching logic. Implementing custom matching requires developing custom code in Adobe Developer App Builder to define how assets are matched with products. See [Custom automatic matching](../synchronize/custom-match.md).

For the initial setup, use the default **[!UICONTROL Match by product SKU]** rule.

## Requirements

Before configuring the AEM Assets Integration, verify that you have completed the following steps:

* [Configure the AEM Assets project](configure-aem.md)

* [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} [Install Adobe Commerce packages](configure-commerce.md) to add the extension and generate the required credentials and connections to use the extension.

* [User permissions and IMS](permissions.md)—Configure the required permissions for the Asset Selector, AEM environment selection, and domain mapping.

## Configure the connection

![AEM Assets Integration configuration with example environment and domain values](../assets/aem-assets-view.png){width="900" zoomable="yes"}

1. From the Commerce Admin, go to **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

>[!INFO]
>
> The AEM Assets integration only supports configuration at the global (default) scope. Website-level configuration is not supported. When you attempt to configure the integration at the Website level, the system ignores website-level settings and uses the global configuration values instead.

1. [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} Enter the **[!UICONTROL Asset Selector IMS Client ID]**.

    This ID is required to enable the Asset Selector. See [User permissions and IMS](permissions.md) to obtain this ID. For details about the Asset Selector, see [Manually selecting assets](../synchronize/asset-selector-integration.md).

1. From **[!UICONTROL AEM Environment]**, select the environment configured in [Configure the AEM Assets project](configure-aem.md).

    The list includes AEM environments for which your user has an Author or Delivery product profile. If the expected environment is missing, review [User permissions and IMS](permissions.md).

    If your configuration displays separate **[!UICONTROL Program ID]** and **[!UICONTROL Environment ID]** fields instead, specify the identifiers for that environment. For manual entry, copy them from AEM Cloud Manager, or derive them from your author URL: `https://author-p<ProgramID>-e<EnvironmentID>.adobeaemcloud.com/`. Enter only the numeric identifiers, without the `p` and `e` prefixes.

    For fields with a **[!UICONTROL Use system value]** checkbox, clear it before overriding the default value.

1. Check **[!UICONTROL AEM Domain Mapping]**. Available domains are loaded automatically based on the selected AEM environment. If your project uses a custom asset-delivery domain, follow [Configure the Custom Domain URL](#optional-configure-the-custom-domain-url).

1. [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}  Select the [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) for authenticating requests between Commerce and the asset matching service.

1. Set **[!UICONTROL Synchronization enabled]** to `Yes` to allow Commerce to accept incoming updates from AEM Assets.

   After enabling the integration, additional configuration options are available to specify asset matching criteria.

1. Select one of the asset matching rules for asset synchronization from the **[!UICONTROL Asset matching rule]**  dropdown.

    * Select **[!UICONTROL Match by product SKU]** for [default automatic matching](../synchronize/default-match.md).
    * Select **[!UICONTROL Custom match]** for [custom automatic matching](../synchronize/custom-match.md). This option requires [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder).

1. For **[!UICONTROL Match by product SKU]**, enter the [AEM Assets metadata property name](../metadata.md) in the **[!UICONTROL Match by product SKU attribute name]** field. The default is `commerce:skus`.

    Enter the property name, not a product SKU value. Add the actual product SKUs to each asset's **[!UICONTROL Product Data]** metadata in AEM Assets, as described in [Default automatic matching](../synchronize/default-match.md).

1. Review the [Visualization Owner](#configure-the-visualization-owner) setting. During migration, retain **Adobe Commerce** ownership until asset synchronization completes.

1. Select **[!UICONTROL Save Config]** to apply updates and initiate asset synchronization.

   The configuration update triggers the initial synchronization process, allowing Commerce to accept incoming updates from AEM Assets. The time required for synchronization depends on the volume of assets and specific configurations. The integration leverages automated processes to minimize the time required for synchronization.

### Synchronization SLA

The service level agreement (SLA) for the integration guarantees the following synchronization performance levels:

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

This level of service ensures that product pages always display the most up-to-date images, keeping storefront content accurate and visually appealing.

## Synchronize localized alt text

Localized alt text uses the existing asset synchronization process. You do not need a new event type or a separate synchronization configuration.

1. Add one or more store-view alt-text rows in the AEM asset's **[!UICONTROL Commerce]** tab.

1. Associate the asset with the Commerce product SKU.

1. Approve the asset in AEM Assets.

1. Wait for the asset event and synchronization process to complete.

1. Verify the localized value in Commerce Admin and in the storefront response.

For the field names, validation rules, and Commerce result, see [Commerce metadata in AEM Assets](../metadata.md).

## Configure the Visualization Owner

The **Visualization Owner** setting determines which system serves product images in the integration:

* Adobe Commerce – Uses images hosted in Commerce.

* AEM Assets – Uses images synchronized from AEM.

The Admin displays the available images for that owner, while the rest of the images are grayed out and displayed with a **hidden** label.

See the [set image details](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} topic for details on image display behavior.

>[!TIP]
>
> During a migration from Commerce to AEM Assets, set the **Visualization Owner** to Commerce to avoid broken image links. After all the products have been successfully synchronized with AEM Assets, switch to the AEM Assets owner to complete the transition. This ensures continuous image availability throughout the process.

1. Navigate to **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

    ![Visualization Owner set to AEM Assets](../assets/visualization-owner-detail.png){width="700" zoomable="yes"}

1. Select the **Visualization Owner** source to display the images.

1. Click **[!UICONTROL Save Config]** to apply updates.

    Before switching to **AEM Assets**, [verify that the assets are associated with the expected products](#verify-the-integration). Then [configure your storefront](configure-storefront.md) to display AEM Assets product images.

## Optional. Configure the Custom Domain URL

If the AEM Assets as a Cloud Service project has been configured with a [Custom Domain Name](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, you must add the domain name to the Commerce store configuration so that the AEM Assets integration for Commerce can use it.

Obtain the configured asset-delivery custom domain URL from your AEM administrator. This setting replaces the AEM delivery URL; it is not the AEM author URL used to identify the Program ID and Environment ID. If your project does not use a custom domain, leave the domain mapping unchanged.

>[!NOTE]
>
>Configuring a custom domain URL does not update the URLs of previously synchronized assets. These assets retain their previous URLs until they are [reprocessed in AEM Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing){target=_blank}. After saving the custom domain configuration, reprocess these assets to update their URLs to use the custom domain.

1. Navigate to **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Confirm the selected **[!UICONTROL AEM Environment]**, then select the configured custom domain from **[!UICONTROL AEM Domain Mapping]**. Available domains are loaded automatically for the selected environment.

  ![AEM environment and domain selectors with example values](../assets/aem-assets-environment-domain.png){width="700" zoomable="yes"}

    For configurations that display an **[!UICONTROL Asset Custom Domain]** text field instead, enter the custom domain URL in that field.

1. Click **[!UICONTROL Save Config]** to apply updates.

## Verify the integration

>[!NOTE]
>
>Sync Status is not available for Adobe Commerce Optimizer. Follow the [Commerce Optimizer verification workflow](configure-aco.md#match-by-sku-workflow-example) instead of the Commerce Admin checks below.

1. Choose an existing Commerce product and note its SKU.

1. In AEM Assets, mark a test asset as **[!UICONTROL Eligible for Commerce]**, associate it with that product SKU, and set its role and position. Approve the asset. See [Default automatic matching](../synchronize/default-match.md), or use your configured [custom matching rule](../synchronize/custom-match.md).

1. After synchronization completes, open the product in Commerce Admin and check its **[!UICONTROL Images And Videos]** section for the associated asset, role, and position. See [Manage assets](../manage-assets.md).

1. Review [Sync Status](sync-status.md) for the asset's synchronization result. If synchronization fails, review the **[!UICONTROL Error]** column.

1. After selecting **AEM Assets** as the Visualization Owner and completing the [storefront configuration](configure-storefront.md), open the product on the storefront and confirm that the expected image appears.

[!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} For additional synchronization troubleshooting, review the [integration logs](logs.md).

## Next step

* [Configure your Commerce Storefront](configure-storefront.md) to display product images from AEM Assets with Edge Delivery Services.

* Set up [matching rules](../synchronize/default-match.md) between Adobe Commerce and the AEM Assets integration.

* [Manage Commerce assets](../manage-assets.md).
