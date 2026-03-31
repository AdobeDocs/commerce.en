---
title: Adding files to products
description: Learn how to attach files such as PDFs, manuals, and data sheets to products using file-type product attributes in [!DNL Adobe Commerce as a Cloud Service].
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Adding files to products

[!DNL Adobe Commerce as a Cloud Service] supports a "File" [product attribute input type](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"} that allows merchants to attach files—such as PDFs, manuals, certificates, and data sheets directly to products. Files are stored in Amazon S3 media storage and can be accessed through the storefront using GraphQL or through integrations using the REST API.

There are three ways to upload files to product file attributes:

* [Admin UI](#upload-through-the-admin) - Upload files manually on the product edit page.
* [REST API](#upload-through-the-rest-api) - Upload files through the REST API using S3 presigned URLs.
* [Product import](#upload-through-product-import) - Import files in bulk by providing external URLs in CSV.

## Prerequisites

Before uploading files, you must create a file attribute and assign it to an attribute set.

* [Create a file attribute](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - Set **[!UICONTROL Catalog Input Type for Store Owner]** to **[!UICONTROL File]**.

* [Assign the attribute to an attribute set](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} - Drag the new file attribute into the desired group.

* Configure allowed file types and size - Navigate to **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Product File Attributes]** and set the allowed file types and size.

  * Set **[!UICONTROL Allowed File Extensions]** to a comma-separated list of permitted file types, such as `pdf,doc,docx,txt`. Leave blank to use the defaults (pdf, doc, docx, xls, xlsx).

  * Set **[!UICONTROL Maximum File Size]** in MB, such as `20.0`. The default limit is 16 MB.
   
## Upload files through the Admin

After you [create a file attribute](#prerequisites) and assign it to an attribute set, you can upload files directly from the product edit page.

1. On the _Admin_ sidebar, go to **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Open the product you want to edit, or [create a new product](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/product-create){target="_blank"}.

1. Locate the file attribute field and click **[!UICONTROL Upload]** to select a file.

1. Click **[!UICONTROL Save]**.

To replace a file, delete the existing file and upload a new one. The uploaded file is stored in Amazon S3 media storage. <!-- ACCS-535, ACCS-565 -->

## Upload through the REST API

Use the S3 presigned URL flow to upload files programmatically through the REST API. This process works the same way for product file attributes as it does for other media types such as category images and customer attribute files.

The process has four steps:

1. Call `POST V1/media/initiate-upload` with the file name and the `media_resource_type` for product file attributes. <!-- This value needs confirmation from engineering. -->
1. Use the returned presigned URL to `PUT` the file directly to Amazon S3.
1. Call `POST V1/media/finish-upload` to confirm the upload.
1. Assign the returned key to the product's file attribute through `PUT /V1/products/{sku}`, passing the key as the [custom attribute](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/) value.

For the complete API reference, request and response examples, and curl commands, see [Upload files to Amazon S3](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"}. <!-- ACCS-565 -->

## Upload through product import

You can attach files to products in bulk using the [import API](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} or the Admin import UI. Product file attributes support import from external URLs only, which follows the same approach as [Method 2 for product image import](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}. Commerce downloads the file from the provided URL and saves it to S3 media storage.

>[!NOTE]
>
>Importing files from a local server path (Method 1) is not supported in [!DNL Adobe Commerce as a Cloud Service] because there is no direct filesystem access. <!-- ACCS-535 -->

### Provide the URL in a dedicated column

Use the attribute code as the CSV column header and the full URL as the value:

```csv
sku,name,test_file
ADB112,"My Product",https://example.com/files/manual.pdf
```

### Provide the URL in `additional_attributes`

Alternatively, include the file attribute in the `additional_attributes` column:

```csv
sku,name,additional_attributes
ADB112,"My Product",test_file=https://example.com/files/manual.pdf
```

In both cases, the URL must be publicly accessible, and the file extension and size must comply with the [configured limits](#configure-allowed-file-types-and-size).

For the full import API specification including JSON format and validation strategies, see [Import data](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}.

## Retrieve files through GraphQL

File attributes resolve to the `AttributeFile` type, which is a SaaS-only implementation of `AttributeValueInterface`. Query product file attributes through `custom_attributesV2`:

```graphql
{
  products(filter: { sku: { eq: "ADB112" } }) {
    items {
      sku
      name
      custom_attributesV2 {
        items {
          code
          ... on AttributeFile {
            url
            value
          }
        }
      }
    }
  }
}
```

The `url` field returns the full public URL to the file. The `value` field returns the relative path in media storage.

For more information about the `AttributeFile` and `AttributeImage` types, see [Attribute interfaces and implementations](https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/interfaces/){target="_blank"}.

## Retrieve files through the REST API

When retrieving a product through the REST API (`GET /V1/products/{sku}`), file attributes appear in the `custom_attributes` array with the filename as the value:

```json
{
  "custom_attributes": [
    {
      "attribute_code": "test_file",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```

For the complete product REST API reference, see the [SaaS REST API reference](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"}.
