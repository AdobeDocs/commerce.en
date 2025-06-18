---
title: Configure the integration
description: Learn how to connect your Adobe Commerce project and Experience Manager Assets projects to enable asset synchronization between these two systems.
feature: CMS, Media
---

# Configure the integration

Configure the integration by connecting Commerce to the AEM Assets instance and selecting the matching strategy for asset synchronization.

After identifying the AEM Assets project, select the matching rule for synchronizing assets between Adobe Commerce and AEM Assets.

* **[!UICONTROL Match by product SKU]**—Default rule that matches the SKU in the asset metadata with the [Commerce product SKU](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku) to ensure that assets are associated with the correct products.

* **[!UICONTROL Custom match]**—Matching rule for more complex scenarios or specific business requirements that require custom matching logic. Implementing custom matching requires developing custom code in Adobe Developer App Builder to define how assets are matched with products. More details coming soon...

For the initial setup, use the default *Match by product sku* rule.

## Prerequisites

* [Install AEM Assets package](configure-aem.md)

* [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} [Install Adobe Commerce packages](configure-commerce.md) to add the extension and generate the required credentials and connections to use the extension.

* Follow the steps described in the [enable Dynamic Media Open API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis) topic. Include the following information for the support team:

  * **[!UICONTROL AEM Program ID]**
  * **[!UICONTROL Adobe Commerce URL]**
  * **[!UICONTROL AEM Environment ID]**,
  * **[!UICONTROL IMS Org ID]** for the AEM Assets Authoring environment that you want to connect to Commerce.

## Configure the connection

1. Get the [AEM Assets Authoring Environment](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/quick-start) project and environment ID.

   1. Open the AEM Cloud Manager and select **[!UICONTROL Assets]**.

   1. Copy and save the project and environment IDs from the URL:<br>`https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`
   
1. From the Commerce Admin, open the AEM Assets Integration configuration.

   1. Go to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

      ![AEM Assets Integration enable the integration](../assets/aem-assets-integration-enable-config.png){width="600" zoomable="yes"}

1. Enter the AEM Assets environment **[!UICONTROL Program ID]** and **[!UICONTROL Environment ID]**.

   Edit the configuration values by removing the selection from *[!UICONTROL Use system value]*.

1. Enter the **[!UICONTROL Asset Selector IMS Client ID]**.

    For details about the Asset Selector, see [Manually selecting assets](../synchronize/asset-selector-integration.md)

1. [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}  Select the [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) for authenticating requests between Commerce and the asset matching service.

1. Set **[!UICONTROL Integration enabled]** to `Yes` to allow Commerce to accept incoming updates from AEM Assets.

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

### Optional. Configure the Custom Domain URL

If the AEM Assets as a Cloud Service project has been configured with a [Custom Domain Name](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, you must add the domain name to the Commerce store configuration so that the AEM Assets integration for Commerce can use it.

1. Navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![AEM Assets Integration enable the integration](../assets/aem-assets-view.png){width="600" zoomable="yes"}

1. Add the **Custom Domain URL** to the **[!UICONTROL Asset Custom Domain]** field.

1. Click **[!UICONTROL Save Config]** to apply updates and initiate asset synchronization.

## Next step

[Manage Commerce assets with Product Visuals](../manage-assets.md)
