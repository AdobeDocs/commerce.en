---
title: Migrate media files to AEM
description: Migrate the media files from Adobe Commerce or an external source into the AEM Assets DAM.
feature: CMS, Media, Integration
exl-id: ccb13e90-8b18-4f1e-94ce-f0dacea2f617
---
# Migrate media files to the AEM Assets DAM

 Both Adobe Commerce and Adobe Experience Manager (AEM) provide built-in features to streamline media file migration from Commerce to the AEM Assets **digital asset management system (DAM)**. You can also migrate media files from other sources.

## Prerequisites

| Category | Requirement |
|----------|-------------|
| **System requirements** | <ul><li>AEM as a Cloud Service environment provisioned with AEM Assets</li><li>Sufficient storage capacity</li><li>Network bandwidth for large file transfers</li></ul> |
| **Required access and permissions** | <ul><li>Administrator access to AEM Assets as a Cloud Service</li><li>Access to source system where media files are stored (Adobe Commerce or external system)</li><li>Appropriate permissions to access cloud storage services</li></ul> |
| **Cloud Storage Account** | <ul><li>AWS S3 or Azure Blob Storage account</li><li>Private container/bucket configuration</li><li>Authentication credentials</li></ul> |
| **Source Content** | <ul><li>Organized media files ready for migration</li><li>Image and video files in <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">formats supported by AEM Assets</a>.</li><li>Clean, duplicated assets</li></li> |
| **Metadata Preparation** | <ul><li><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">AEM Assets metadata profile configured for Commerce assets</a></li><li>Mapped metadata values for each asset</li><li>CSV file editor (e.g., Microsoft Excel)</li></ul> |

## Migration best practices

1. Curate assets before migration by removing unused and duplicate content.

1. Organize assets logically by size, format, or use case.

1. Consider breaking large migrations into smaller batches.

1. Schedule resource-intensive imports during off-peak hours.

1. Validate metadata mapping before full import.

## Migration workflow

Follow the migration workflow to export media files from Adobe Commerce or another external system and import them into the AEM Assets DAM.

### Step 1: Export content from the existing data source 

[!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}

For Adobe Commerce merchants, the **Remote Storage module** can facilitate media file imports and exports. This module allows businesses to store and manage media files using remote storage services like AWS S3. To set up remote storage for your Commerce instance, see [Configure Remote Storage](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3) in the **Commerce Configuration Guide**.

If you have media files stored outside of Adobe Commerce, upload them directly to one of the [data sources](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites) supported by AEM as a Cloud Service.

### Step 2: Build a CSV file for metadata mapping

Create a CSV file that maps each media file to its Commerce product data. Choose one of the following methods:

* **Adobe Commerce (PaaS)**: Use the CLI command to auto-generate the CSV from your catalog
* Manually create the CSV file

#### Export metadata using CLI

[!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}

Use the AEM Assets Integration CLI command to automatically generate a metadata CSV file that includes image URLs, positions, and roles from the product media files stored in your Commerce  project.

1. List available commands to verify the AEM Assets Integration module is installed:

   ```bash
   bin/magento list aem
   ```

   The custom extension commands appear under `aem` at the start of the command list.

1. Run the metadata export command with your AEM path prefix:

   ```bash
   bin/magento aem:assets:export:csv <AEM-path-prefix>
   ```

   The `<AEM-path-prefix>` is the base folder path where your assets will be stored in AEM Assets DAM (for example, `/content/dam/commerce/`).

   ```bash
   bin/magento aem:assets:export:csv /content/dam/commerce/
   ```

   This creates a `metadata.csv` file in the `var/export` directory containing image URLs, positions, and roles for each product asset in your Commerce catalog.

#### Create the CSV manually

For media files stored outside Adobe Commerce, manually create the CSV file. The column headers **must match** the field names configured in your [AEM Assets metadata profile](configure-aem.md). After creating the file, populate the rows with the metadata values for each media file.

| Metadata | Description | Value |
|-------|-------------|--------|
| assetPath | The full path where the asset will be stored in the AEM Assets repository.<br><br>Use the path to create sub-folders to organize Commerce assets, for example `content/dam/commerce/<brand>/<type>`. | `/content/dam/commerce/<sub-folder>/..<filename>` |
| commerce:positions | The position/order of the asset in product galleries | Multiple numeric values separated by pipe ("Number: multi") |
| commerce:isCommerce | Flag indicating if the asset is used in commerce | `Yes` |
| commerce:skus | Product SKUs associated with this asset | Multiple string values separated by pipe (String: multi) |
| commerce:roles | The roles or types of images for the asset (for example, `thumbnail`, `main image`, `swatch`) | Multiple values separated by semicolons (for example, "thumbnail; image; swatch_image; small_image") |

+++CSV code

Use this sample CSV code to create the file in a code editor or spreadsheet application like Microsoft Excel.

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### Step 3: Bulk Import Assets into AEM Assets

After creating the metadata mapping file, use the AEM Assets Bulk Import Tool to import your assets.

The following is a high-level overview for using the tool.

1. [Log in to your AEM Assets as a Cloud Service author environment](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem).

1. From the Experience Manager Tools view, select **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**.

   ![AEM Assets authoring](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. From the Bulk Import Configurations, select **[!UICONTROL Create]** to open the configuration form.

   ![AEM Assets authoring](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. Set up and save the configuration.

   You'll need:

   * Authentication credentials for your data source
   * The target folder in AEM Assets where imported files will be stored
   * Optional. Information about the MIME types, file size, and other parameters to customize the import configuration
   * The path to the metadata mapping CSV file you uploaded to the Cloud storage instance.

   For detailed steps, see [Configure the Bulk Import tool](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool) in the *AEM Assets as a Cloud Service User Guide*.

1. After saving the configuration, use the bulk import tools to test and run the import operation.

>[!MORELIKETHIS]
>
> [Bulk Import tool video demo](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> [Tips, best practices, and limitations](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> [Upload or ingest assets using APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)
