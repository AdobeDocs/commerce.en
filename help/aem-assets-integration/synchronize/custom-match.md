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

### workspace.json

The **[!UICONTROL Adobe I/O Workspace Configuration]** field provides a streamlined way to configure your custom matcher by importing your App Builder `workspace.json` configuration file.

You can download the `workspace.json` file from the [Adobe Developer Console](https://developer.adobe.com/console). The file contains all the credentials and configuration details for your App Builder workspace.

+++Example `workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. Drag and drop your `workspace.json` file from your App Builder project into the **[!UICONTROL Adobe I/O Workspace Configuration]** field. Alternatively, you can click to browse and select the file.

![Workspace Configuration](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. The system automatically:

   * Validates the JSON structure
   * Extracts and populates OAuth credentials
   * Fetches available runtime actions for the workspace
   * Populates dropdown options for the **[!UICONTROL Product to Asset URL]** and **[!UICONTROL Asset to Product URL]** fields

1. Select the appropriate runtime actions from the dropdown menus for each flow.

1. Click **[!UICONTROL Save Config]**.

## Custom matcher API endpoints

When you build a custom matcher application using [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, the application must expose the following endpoints:

* **App Builder asset to product URL** endpoint
* **App Builder product to asset URL** endpoint

### App Builder asset to product URL endpoint

This endpoint retrieves the list of SKUs associated with a given asset:

#### Example usage

```javascript
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

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Request**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `assetId` | String | Represents the updated asset ID. |
| `eventData` | String | Returns the data payload associated with the asset ID. |

**Response**

```json
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail", "image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ],
  "skip": false
}
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `asset_id` | String | The asset ID being matched. |
| `product_matches` | Array | List of products associated with the asset. |
| `skip` | Boolean | (Optional) When `true`, the rule engine skips syncing for this asset (no product mapping update). When `false` or omitted, normal processing runs. See [Skip sync processing](#skip-sync-processing). |

### App Builder product to asset URL endpoint

This endpoint retrieves the list of assets associated with a given SKU:

#### Example usage

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Request**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `productSKU` | String | Represents the updated product SKU. |
| `eventData` | String | Returns the data payload associated with the Product SKU. |

**Response**

```json
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail", "image"],
      "asset_position": 1,
      "asset_format": "image"
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"],
      "asset_position": 2,
      "asset_format": "image"
    }
  ],
  "skip": false
}
```

| Parameter | Data Type | Description |
| --- | --- | --- |
| `product_sku` | String | The product SKU being matched. |
| `asset_matches` | Array | List of assets associated with the product. |
| `skip` | Boolean | (Optional) When `true`, the rule engine skips syncing for this product (no asset mapping update). When `false` or omitted, normal processing runs. See [Skip sync processing](#skip-sync-processing). |

The `asset_matches` parameter contains the following attributes:

| Attribute | Data Type | Description |
| --- | --- | --- |
| `asset_id` | String | The asset ID. |
| `asset_roles` | Array | Asset roles. Uses supported [Commerce asset roles](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) like `thumbnail`, `image`, `small_image`, and `swatch_image`. |
| `asset_format` | String | The asset format. Possible values are `image` and `video`. |
| `asset_position` | Number | The position of the asset in the product gallery. |

## Skip sync processing

The `skip` parameter allows your custom matcher to bypass sync processing for specific assets or products.

When your App Builder application returns `"skip": true` in the response, the rule engine does not send update or remove API requests to Commerce for that asset or product. This optimization reduces unnecessary API calls and improves performance.
