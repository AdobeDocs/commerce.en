---
title: Configure the AEM Assets Project to support Commerce metadata
description: Enable seamless asset synchronization between Adobe Commerce and AEM Assets by adding the required metadata for the integration.
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
---
# Configure the AEM Assets project to support Commerce metadata

When you use AEM Assets as a Digital Asset Management system (DAM) for Commerce, installing the `assets-commerce` package allows you to manage images and videos for Commerce products from the AEM authoring environment.

Complete the following steps to configure the AEM Assets project with the required package code and metadata to manage Commerce assets from the AEM authoring environment:

1. [Learn about the `assets-commerce` package contents](#aem-commerce-assets-commerce-package-contents)

1. [Complete the installation steps to configure the AEM Assets project to support Commerce metadata](#step-1-install-the-assets-commerce-package)

## AEM Commerce assets-commerce package contents

Adobe provides an AEM Commerce package code `assets-commerce` to add Commerce namespace and Metadata Schema resources to the Experience Manager Assets as a Cloud Service environment configuration.

This package code adds the following resources to the AEM Assets authoring environment:

* A [custom namespace](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` to identify Commerce-related properties.

  * A custom metadata type `commerce:isCommerce` with the label `Eligible for Commerce` to tag Commerce assets associated with an Adobe Commerce project.

  * A custom metadata type `commerce:skus` and a corresponding UI component to add a **[!UICONTROL Product Data]** property. Product Data includes the metadata properties to associate a Commerce asset with product SKUs.

      ![Custom Product Data UI Control](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

  * A custom metadata type `commerce:roles` and `commerce:positions`  attributes to show how the asset is visualized in Commerce.

* A metadata schema form with a Commerce tab that includes the `Eligible for Commerce` and `Product Data` fields for tagging Commerce assets. The form also provides options to show or hide the `roles` and `position` fields from the AEM Assets UI.

  ![Commerce tab for AEM Assets metadata schema form](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* A [sample tagged and approved Commerce asset](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` to support initial asset synchronization. Only approved Commerce assets can be synchronized from AEM Assets to Adobe Commerce.

>[!NOTE]
>
> See the [readme](https://github.com/ankumalh/assets-commerce) page for more information about the **AEM Commerce package code**.

## Prerequisites

You need the following resources and permissions to deploy the `assets-commerce` package code to the AEM Assets as a Cloud Service AEM  environment:

* [Access to the AEM Assets Cloud Manager Program and environments](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) with the Program and Deployment Manager roles.

* A [local AEM development environment](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) and familiarity with the AEM local development process.

* Understand [AEM project structure](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) and how to deploy custom content packages using Cloud Manager.

* The **IMS Org ID** configured for your Commerce instance.

## Step 1: Install the assets-commerce package

1. Navigate to the AEM Cloud Manager, select a program, and [create production and staging environments](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments) that you want to integrate with Adobe Commerce.

1. Configure a [deployment pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline), or verify that your pipeline can deploy changes to the selected environment.

1. [Clone the Adobe managed git repository](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access) for the selected program.

1. From GitHub, download the package code from the [AEM Assets Commerce repository](https://github.com/ankumalh/assets-commerce).

1. From your [local AEM development environment](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview), manually copy the downloaded code into the existing Adobe managed repository.

1.  In all `filter.xml` and `pom.xml files` for your project, replace all occurrences of `<my-app>` with your app name.

   >[!NOTE]
   >
   > Alternatively, you can install the custom code into your AEM Assets project configuration as a **Maven** package.

1. Commit the changes and push your local development branch to the Cloud Manager Git repository.

1. From AEM Cloud Manager, [update the AEM environment by using the pipeline to deploy your code](https://experienceleague.dobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager).

1. Go to any asset and edit its properties to validate the changes:

   * The default Metadata Schema includes the **Commerce** tab.

   * Product SKUs and the `Eligible for Commerce` fields are visible. 

### Commerce tab is not visible in properties

If the **Commerce** tab does not appear in properties, you must manually create one in the metadata schema editor.

1. Navigate to the metadata schema editor.

1. Click **Edit** to modify the default metadata schema form.

1. Create a **Commerce** tab, and select it.

1. Drag and drop the **Product** component into the **Commerce** tab, and map it to the property `commerce:skus`.

1. Select the checkbox for **show roles** and **show order**.

1. Drag and drop a **checkbox** component into the **Commerce** tab, and map it to the property `commerce:isCommerce`. Define **Yes** and **No** as the options.

If you encounter any other issues,  create a [support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) or contact your AEM Assets Integration sales representative for help.

## Step 2: Optional. Configure a metadata profile

In the AEM Assets author environment, set default values for Commerce asset metadata by creating a metadata profile. Then, apply the new profile to AEM Asset folders to automatically use these defaults. This configuration streamlines asset processing by reducing manual steps.

When you configure the metadata profile, you only have to configure the following components:

* Add a Commerce tab. This tab enables Commerce specific configuration settings added by the template.

* Add the `Eligible for Commerce` field to the Commerce tab.

The Product Data UI component is added automatically based on the template.

### Define the metadata profile

1. Log in to the Adobe Experience Manager author environment.

1. From the Adobe Experience Manager workspace, go to the Author Content Administration workspace for AEM Assets by clicking the Adobe Experience Manager icon.

   ![AEM Assets authoring](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. Open the Administrator tools by selecting the hammer icon.

   ![AEM Author Admin manage metadata profiles](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. Open the profile configuration page by clicking **[!UICONTROL Metadata Profiles]**.

1. **[!UICONTROL Create]** a metadata profile for the Commerce integration.

   ![AEM Author Admin add metadata profiles](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. Add a tab for Commerce metadata.

   1. On the left, click **[!UICONTROL Settings]**.

   1. Click  **[!UICONTROL +]** in the tab section, and then specify the **[!UICONTROL Tab Name]**, `Commerce`.

1. Add the `Eligible for Commerce` field to the form.

   ![AEM Author Admin add metadata fields to profile](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * Click **[!UICONTROL Build form]**.

   * Drag the `Single Line text` field to the form.

   * Add the `Eligible for Commerce` text for the label by clicking **[!UICONTROL Field Label]**.

   * On the Settings tab, add the label text to **Field Label**.

   * Set the placeholder text to `yes`.

   * In the **[!UICONTROL Map to Property]** field, copy and paste the following value

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. Optional. To automatically synchronize approved Commerce assets as they are uploaded to the AEM Assets environment, set the default value for the _[!UICONTROL Review Status]_ field on the `Basic` tab to `approved`.

1. Save the update.

### Apply the metadata profile to the Commerce assets source folder

   1. From the[!UICONTROL  Metadata Profiles] page, select the Commerce integration profile.

   1. From the action menu, select **[!UICONTROL Apply Metadata Profiles to Folders]**.

   1. Select the folder containing Commerce assets.

      Create a Commerce folder if it does not exist.

   1. Click **[!UICONTROL Apply]**.

## Next steps

* [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} [Install Adobe Commerce packages](configure-commerce.md).

* [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."} [Configure the integration from the Commerce Admin](setup-synchronization.md).
