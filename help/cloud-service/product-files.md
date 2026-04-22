---
title: Add files to products
description: Learn how to attach files such as PDFs, manuals, and data sheets to products using file-type product attributes in [!DNL Adobe Commerce as a Cloud Service].
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Add files to products

[!DNL Adobe Commerce as a Cloud Service] supports a "File" [product attribute input type](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"} that allows merchants to attach files—such as PDFs, manuals, certificates, and data sheets directly to products. Files are stored in Amazon S3 media storage and can be accessed through the storefront using GraphQL or through integrations using the REST API.

There are three ways to upload files to product file attributes:

* [Admin UI](#upload-files-through-the-admin) - Upload files manually on the product edit page.
* [REST API](#upload-through-the-rest-api) - Upload files through the REST API using S3 presigned URLs.
* [Product import](#upload-through-product-import) - Import files in bulk by providing external URLs in CSV.

## Prerequisites

Before uploading files, you must create a file attribute and assign it to an attribute set.

* [Create a file attribute](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - Set **[!UICONTROL Catalog Input Type for Store Owner]** to **[!UICONTROL File]**.

* [Assign the attribute to an attribute set](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} - Drag the new file attribute into the desired group.

* Configure allowed file types and size in the [Product File Attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes) configuration.

## Upload files through the Admin

After you [create a file attribute](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} and assign it to an attribute set, you can upload files directly from the product edit page.

1. On the _Admin_ sidebar, go to **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Open the product you want to edit.

1. Locate the file attribute field and click **[!UICONTROL Upload]** to select a file.

  ![Upload file button in the Admin](./assets/upload-file.png){width="600" zoomable="yes"}

1. Click **[!UICONTROL Save]**.

To replace a file, delete the existing file and upload a new one. The uploaded file is stored in Amazon S3 media storage.

## Upload through the REST API

Use the [S3 presigned URL flow](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"} to upload files programmatically through the REST API. This process works the same way for product file attributes as it does for other media types such as category images and customer attribute files.

The process has four steps:

1. Call `POST V1/media/initiate-upload` with the file name and the `media_resource_type` for product file attributes.
1. Use the returned presigned URL to `PUT` the file directly to Amazon S3.
1. Call `POST V1/media/finish-upload` to confirm the upload.
1. Assign the returned key to the product's file attribute through `PUT /V1/products/{sku}`, passing the key as the [custom attribute](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/) value.

## Upload through product import

You can attach files to products in bulk using the [import API](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} or the Admin import UI. Product file attributes support import from external URLs only, which follows the same approach as [Method 2 for product image import](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}. Commerce downloads the file from the provided URL and saves it to S3 media storage.

>[!NOTE]
>
>Importing files from a local server path (Method 1) is not supported in [!DNL Adobe Commerce as a Cloud Service] because there is no direct filesystem access. 

### Provide the URL in a dedicated column

Use the attribute code as the CSV column header and the full URL as the value. For example, if the attribute code is `file_upload`, the CSV would look like this:

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### Provide the URL in `additional_attributes`

Alternatively, include the file attribute in the `additional_attributes` column:

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

In both cases, the URL must be publicly accessible, and the file extension and size must comply with the [configured limitations](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}.

## Retrieve files through GraphQL

In [!DNL Adobe Commerce as a Cloud Service], the [Catalog Service GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} endpoint serves product data. File attributes appear in the `attributes` field on `ProductView`, with the `value` containing the full public URL to the file:

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

The response includes the file attribute with its public URL:

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>This query requires the `Magento-Website-Code` and `Magento-Store-View-Code` headers. For more information, see the [Catalog Service products query](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}.

## Retrieve files through the REST API

When retrieving a product through the [REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"} (`GET /V1/products/{sku}`), file attributes appear in the `custom_attributes` array with the filename as the value:

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
