---
title: Custom automatic matching
description: Learn how custom automatic matching is particularly useful for merchants with complex matching logic or those relying on a third-party system that cannot populate metadata into AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
---
# Custom automatic matching

If the default automatic matching strategy (**OOTB automatic matching**) is not aligned with your specific business requirements, select the custom match option. This option supports the use of [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) to develop a custom matcher application that handles complex matching logic, or assets coming from a third-party system that cannot populate metadata into AEM Assets.

## Configure custom automatic matching

1. From the Commerce Admin, navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Select **[!UICONTROL Custom Matcher]** as the matching rule.

1. When you select this matching rule, Admin displays additional fields to configure the **endpoints** and the necessary **authentication parameters** for the custom matching logic.

## Custom matcher API endpoints

When you build a custom matcher application using [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, the application must expose the following endpoints:

* **App Builder asset to product URL** endpoint
* **App Builder product to asset URL** endpoint

### App Builder asset to product URL endpoint

This endpoint retrieves the list of SKUs associated with a given asset:

#### Example usage

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Request**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `assetId` | String | Represents the updated asset ID |
| `eventData` | String | Returns the data payload associated with the `assetId` |

**Response**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### App Builder product to asset URL endpoint

This endpoint retrieves the list of assets associated with a given SKU:

#### Example usage

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Request**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `productSKU` | String | Represents the updated product SKU. |
| `asset_matches` | String | Returns all assets associated with a specific `productSku`. |

The `asset_matches` parameter contains the following attributes:

| Attribute | Data Type | Description |
| --- | --- | --- |
| `asset_id` | String | Represents the updated asset ID. |
| `asset_roles` | String | Returns all available asset roles. Uses supported [Commerce asset roles](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) like `thumbnail`, `image`, `small_image`, and `swatch_image`. |
| `asset_format` | String | Provides the available formats for the asset. Possible values are `image` and `video`. |
| `asset_position` | String | Shows the position of the asset. |

**Response**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```
