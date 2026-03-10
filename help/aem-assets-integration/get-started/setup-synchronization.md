---
title: Configure the integration
description: Learn how to connect your Adobe Commerce project and Experience Manager Assets projects to enable asset synchronization between these two systems.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
---
# Configure the integration

Configure the integration by connecting Commerce to the AEM Assets instance and selecting the matching strategy for asset synchronization.

After identifying the AEM Assets project, select the matching rule for synchronizing assets between Adobe Commerce and AEM Assets.

* **[!UICONTROL Match by product SKU]**—Default rule that matches the SKU in the asset metadata with the [Commerce product SKU](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku) to ensure that assets are associated with the correct products.

* **[!UICONTROL Custom match]**—Matching rule for more complex scenarios or specific business requirements that require custom matching logic. Implementing custom matching requires developing custom code in Adobe Developer App Builder to define how assets are matched with products. More details coming soon...

For the initial setup, use the default *Match by product sku* rule.

## Requirements

Before configuring the AEM Assets Integration, verify that you have completed the following steps:

* [Configure the AEM Assets project](configure-aem.md)

* [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} [Install Adobe Commerce packages](configure-commerce.md) to add the extension and generate the required credentials and connections to use the extension.

### IMS and user permissions

To use the Asset Selector and provide a smoother setup in Commerce, the following permissions are required:

>[!BEGINTABS]

>[!TAB ACCS]

[!BADGE SaaS only]{type=Positive tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."}

IMS authentication is enabled by default. Add the user to the **AEM Assets DM OpenAPI Users - delivery** product profile in the [Adobe Admin Console](https://adminconsole.adobe.com/) to grant access to the AEM Assets delivery layer.

![Admin Console product profile for AEM Assets delivery](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB PaaS]

[!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}

1. [Enable Adobe IMS for Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} by following the instructions in the *Commerce Admin Guide*.

1. [Open a Support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) to request a custom IMS Client ID for the Asset Selector.

1. Add the user to the **AEM Assets DM OpenAPI Users - delivery** product profile in the [Adobe Admin Console](https://adminconsole.adobe.com/) to grant access to the AEM Assets delivery layer.

>[!ENDTABS]

## Configure the connection

1. From the Commerce Admin, open the AEM Assets Integration configuration.

   1. Go to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

      ![AEM Assets Integration enable the integration](../assets/aem-assets-view.png){width="600" zoomable="yes"}

>[!INFO]
>
> The AEM Assets integration only supports configuration at the global (default) scope. Website-level configuration is not supported. When you attempt to configure the integration at the Website level, the system ignores website-level settings and uses the global configuration values instead.

1. [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} Enter the **[!UICONTROL Asset Selector IMS Client ID]**.

    This ID is required to enable the Asset Selector and auto-populate feature for the Program ID and Environment ID fields. See [IMS and user permissions](#ims-and-user-permissions) to obtain this ID. For details about the Asset Selector, see [Manually selecting assets](../synchronize/asset-selector-integration.md).

1. Select the AEM Assets environment **[!UICONTROL Program ID]** and **[!UICONTROL Environment ID]** from the dropdown menus.

   The dropdowns auto-populate based on the user's IMS session. To use this feature, ensure you have the right [IMS and user permissions](#ims-and-user-permissions).

   If the dropdowns are not available, you can manually enter the IDs from the AEM Cloud Manager URL: `https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

   Edit the configuration values by removing the selection from *[!UICONTROL Use system value]*.

1. [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}  Select the [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) for authenticating requests between Commerce and the asset matching service.

1. Set **[!UICONTROL Synchronization enabled]** to `Yes` to allow Commerce to accept incoming updates from AEM Assets.

   After enabling the integration, additional configuration options are available to specify asset matching criteria.

1. Select one of the asset matching rules for asset synchronization from the **[!UICONTROL Asset matching rule]**  dropdown.

   * Select **[!UICONTROL Match by SKU]** for [default automatic matching](../synchronize/default-match.md),
   * Select **[!UICONTROL Custom match]** for [custom automatic matching](../synchronize/custom-match.md) (requires [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder).)

1. Add the [AEM Assets metadata field name](configure-aem.md#configure-metadata) defined for Commerce product SKUs in the **[!UICONTROL Match by product SKU attribute name]** field, `commerce:skus` by default.

1. Select **[!UICONTROL Save Config]** to apply updates and initiate asset synchronization.

   The configuration update triggers the initial synchronization process, allowing Commerce to accept incoming updates from AEM Assets. The time required for synchronization depends on the volume of assets and specific configurations. The integration leverages automated processes to minimize the time required for synchronization.

### Synchronization SLA

The integration guarantees the following synchronization performance levels:

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

This ensures that product pages always display the most up-to-date images, keeping storefront content accurate and visually appealing.

### Configure the Visualization Owner

The **Visualization Owner** setting determines which system serves product images in the integration:

* Adobe Commerce – Uses images hosted in Commerce.

* AEM Assets – Uses images synchronized from AEM.

The Admin displays the available images for that owner, while the rest of the images are grayed out and displayed with a **hidden** label.

See the [set image details](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} topic for details on image display behavior.

>[!TIP]
>
> During a migration from Commerce to AEM Assets, set the **Visualization Owner** to Commerce to avoid broken image links. After all the products have been successfully synchronized with AEM Assets, switch to the AEM Assets owner to complete the transition. This ensures continuous image availability throughout the process.

1. Navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![AEM Assets Integration visualization owner feature](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. Select the **Visualization Owner** source to display the images.

1. Click **[!UICONTROL Save Config]** to apply updates and initiate asset synchronization.

### Optional. Configure the Custom Domain URL

If the AEM Assets as a Cloud Service project has been configured with a [Custom Domain Name](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, you must add the domain name to the Commerce store configuration so that the AEM Assets integration for Commerce can use it.

1. Navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![AEM Assets Integration enable the integration](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. Add the **Custom Domain URL** to the **[!UICONTROL Asset Custom Domain]** field.

1. Click **[!UICONTROL Save Config]** to apply updates and initiate asset synchronization.

## Next step

* **Configure your Commerce Storefront**---To use AEM Assets with the Commerce Storefront powered by Edge Delivery Services, complete the storefront configuration described in the [AEM Assets integration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) topic in the *Adobe Commerce Storefront documentation*.

* Set up [matching rules](../synchronize/default-match.md) between Adobe Commerce and the AEM Assets integration.

* [Manage Commerce assets](../manage-assets.md).
