---
title: Configure AEM Assets for Commerce Optimizer
description: Learn how to configure AEM Assets Integration for [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
---

# Configure AEM Assets for [!DNL Adobe Commerce Optimizer]

[!BADGE SaaS only]{type=Positive tooltip="Applies to Adobe Commerce Optimizer projects only."}

The AEM Assets Integration for [!DNL Adobe Commerce Optimizer] enables merchants to use AEM Assets as the centralized digital asset management solution for product images. This guide covers the configuration specific to [!DNL Commerce Optimizer].

Unlike Adobe Commerce (PaaS) or Adobe Commerce as a Cloud Service (ACCS), [!DNL Commerce Optimizer] does not have an Admin configuration UI. To enable the integration, create a support ticket with your [!DNL Adobe Commerce Optimizer] and AEM Assets details. Adobe Support configures the integration and registers your tenant with the Assets Integration Service.

The following diagram is an overview of the product sync between [!DNL Adobe Commerce Optimizer] and the AEM Assets integration.

![AEM Assets to [!DNL Commerce Optimizer] flow](../assets/aco-asset-sync-architecture.png){width="700"}

This integration has two main flows:

* **From AEM Assets**: When an asset is approved, rejected, or removed, the event flows through the Adobe Pipeline to the Assets Integration Service. The service matches assets to products using `match-by-SKU` (metadata-driven) or a [custom matcher (App Builder)](../synchronize/custom-match.md){target=_blank}, then sends the `product-asset` mappings to the Commerce Optimizer, where they are stored as product layers.

* **From [!DNL Adobe Commerce Optimizer]**: When a product is updated in [!DNL Commerce Optimizer], the event flows through the Adobe Pipeline to the Assets Integration Service. The service syncs any matching asset mappings back to the [!DNL Adobe Commerce Optimizer].

## Prerequisites

Before configuring the integration, ensure you have:

* An active [!DNL Adobe Commerce Optimizer] instance with Product Visuals entitlement, or any AEM Assets license with Dynamic Media.
* Access to an AEM Assets as a Cloud Service environment.
* Both [!DNL Commerce Optimizer] and AEM Assets in the same Adobe IMS Organization.
* Dynamic Media with OpenAPI enabled on your AEM Assets environment.

## Onboarding

To onboard AEM Assets Integration with [!DNL Commerce Optimizer], you must [Create a support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

Adobe Support uses the information in your ticket to register your tenant with the Assets Integration Service, and configure the integration.

Include the following information in your support ticket:

* **[!DNL Adobe Commerce Optimizer] Tenant ID** (Instance ID) found in your [!DNL Commerce Optimizer] URL or Commerce Cloud Manager UI.
* **AEM Program ID**.
* **AEM Environment ID**.
* **Matching rule**: Match by SKU or [external matcher (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Layer**: The catalog layer name to register the tenant with. Specify a custom name if needed. Otherwise, the default `AEM-Assets` is used.
* **Locale**: The catalog source locale to register the tenant with (for example, `en-US`).

>[!IMPORTANT]
>
> The integration supports one source per tenant, which is the combination of one locale and one layer.

After Adobe Support processes your ticket, the integration is configured and your tenant is registered with Assets Integration Service.

Once onboarding is complete:

1. **Registration with Assets Integration Service**: Your [!DNL Commerce Optimizer] tenant is registered with Assets Integration Service using the [!DNL Adobe Commerce Optimizer] Tenant ID, AEM Program ID, AEM Environment ID, and  tenant.

1. **Authentication setup**: The IMS service token authentication is configured between [!DNL Commerce Optimizer] and the Assets Integration Service for a secure communication.

1. **Event subscription**: Assets Integration Service subscribes to:

   * AEM Assets events (asset approved, updated, removed)
   * [!DNL Commerce Optimizer] catalog events (product created, updated)

### Limitations

The [!DNL Commerce Optimizer] integration has the following limitations:

* **Single layer per merchant**—The AEM Assets Integration supports one AEM-Assets layer per merchant (one source per tenant). Configuring multiple layers per merchant is not supported at this time.
* **Images only**—The integration does not support video or other media types.
* **No category images**—Category image synchronization is not available. Category images from AEM Assets for the Assets Selector (UI insertion) are not supported.
* **No multi-site distinction**—The integration does not handle multi-site; an image associated with a product is shown the same across all channels and policies.
* **Image position/ordering**—Image position and ordering are not supported.
* **Product must exist**—If the product does not exist in [!DNL Commerce Optimizer], the layer will not be created for that product-asset mapping.
* **Layer field overwriting**—Values in a layer overwrite the base catalog. If a field is not sent in the layer payload, it can be overwritten with an empty value. Use a dedicated layer for AEM Assets content; reusing an existing layer for other purposes may result in unintended data loss.

### Configure your AEM Assets

The AEM Assets installation and configuration process for [!DNL Commerce Optimizer] is the same as for Adobe Commerce as a Cloud Service. See [Configure the AEM Assets project to support Commerce metadata](configure-aem.md) for the complete steps.

Ensure your AEM Assets environment is ready:

1. **AEM Assets configuration**: Configure the Commerce metadata profile. See [Configure a metadata profile](configure-aem.md#configure-a-metadata-profile).

1. **Dynamic Media enablement**: Verify Dynamic Media with OpenAPI capabilities is enabled on your AEM Assets environment.

## Configure AEM Assets

To enable product-asset synchronization, configure your AEM Assets environment.

### Step 1: Enable Dynamic Media with OpenAPI

Dynamic Media with OpenAPI must be enabled on your AEM Assets environment. Product Visuals and new AEM Assets licenses allow you to enable it in a self-service manner via Cloud Manager. Older AEM Assets licenses require Adobe Support to enable it. See [Configure the AEM Assets project](configure-aem.md#prerequisites) for enablement steps.

### Step 2: Optional. Configure Commerce metadata profile

Set up the metadata profile in AEM Assets to store Commerce-specific metadata.

See [Configure a metadata profile](configure-aem.md#step-2-optional-configure-a-metadata-profile) for detailed instructions.

### Step 3: Apply metadata to assets

Add Commerce metadata to your product images in AEM Assets.

See the [AEM Commerce package contents](configure-aem.md#aem-commerce-assets-commerce-package-contents) for field definitions and [Configure a metadata profile](configure-aem.md#step-2-optional-configure-a-metadata-profile) for the setup steps.

The asset must be in an **approved** status for the data sync to trigger. Saving metadata alone does not trigger the event.

>[!CAUTION]
>
> Assign the `AEM-Assets` layer to your [catalog view](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view). If the layer is not assigned, product image data may be overwritten unexpectedly.

## Synchronization

Once configured, the integration synchronizes `product-asset` mappings automatically.

See [Custom automatic matching](../synchronize/custom-match.md) for more information.

### Match by SKU workflow example

A typical flow when adding an existing asset to a new product:

1. Create the product in [!DNL Commerce Optimizer] (via API or data ingestion). The product can exist without images initially.

1. In AEM Assets, open the asset you want to map to the product.

1. Add the product SKU to the **commerce:skus** metadata and assign image roles (for example, `thumbnail`, `image`).

1. Approve the asset for delivery. This triggers the event that Assets Integration Service processes.

1. Assets Integration Service sends the product-image mapping to [!DNL Commerce Optimizer]. The product in [!DNL Commerce Optimizer] is updated with the images from the asset.

1. Verify the image is visible. Allow time for the sync to complete (typically within a few minutes), then check the product in the [!DNL Commerce Optimizer] UI (for example, Data Sync or catalog view), or query the storefront APIs (Catalog Service, Live Search, Storefront GraphQL API) to confirm the image is returned.

## Image role handling

When a product has multiple assets using the same image role (for example, two assets with the `thumbnail` role), the integration ensures only one asset retains that role to avoid duplicate roles in the [!DNL Commerce Optimizer] layer and unexpected storefront behavior.

**Behavior:** When an update is sent from AEM Assets, the most recently updated asset receives the image role (for example, `thumbnail`), and the role is removed from the previous asset that had it. This prevents duplicate image roles from appearing in the storefront.

## More like this

* [Product Visuals](../../optimizer/setup/product-visuals.md)
* [Configure the AEM Assets project](configure-aem.md)
* [Custom automatic matching](../synchronize/custom-match.md)
* [AEM Assets Integration overview](../overview.md)
