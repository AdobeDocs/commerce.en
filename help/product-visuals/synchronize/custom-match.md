---
title: Custom automatic matching
description:  Learn how the custom automatic matching is particularly useful for merchants with complex matching logic or those relying on a third-party system that cannot populate product visuals metadata into the AEM Assets.
feature: CMS, Media, Integration
---

# Custom automatic matching

If the default automatic matching strategy (**OOTB automatic matching**) is not aligned with your specific business requirements, you can select the custom match option. This option supports the use of Adobe Developer App Builder to develop a Custom matcher application that handles complex matching logic, or assets coming from a third-party system that cannot populate product visuals metadata into AEM Assets.

## Configure custom automatic matching

1. Navigate to **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Select **[!UICONTROL Custom Matcher]** as the matching rule.

1. When you select this matching rule, Admin displays additional fields to configure the **endpoints** and the necessary **authentication parameters** for the custom matching logic.

## Custom matcher API endpoints

When you build a Custom matcher application using [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, the application should expose the following main endpoints:

* **App Builder asset to product URL** endpoint
* **App Builder product to asset URL** endpoint

### App Builder asset to product URL endpoint

This endpoint retrieves the list of SKUs associated with a given asset:

#### Example usage

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**Request**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `assetId` | String | Represents the updated asset ID |

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
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**Request**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `productSKU` | String | Represents the updated product SKU |

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

>[!TIP]
>
> Supported Asset Roles like `thumbnail`, `image`, `small_image`, and `swatch_image`.
