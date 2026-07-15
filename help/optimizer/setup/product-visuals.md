---
title: Product Visuals with AEM Assets
description: Learn how to use AEM Assets for product images in [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
---

# Product Visuals with AEM Assets

Product Visuals enables [!DNL Adobe Commerce Optimizer] merchants to manage product images through Adobe Experience Manager (AEM) Assets. This integration provides a seamless workflow for syncing high-quality product imagery from AEM Assets to your [!DNL Commerce Optimizer] catalog using catalog layers.

>[!NOTE]
>
>**Product Visuals** is the name of the bundle provided with [!DNL Adobe Commerce as a Cloud Service] and [!DNL Adobe Commerce Optimizer]. It combines [Dynamic Media with OpenAPI capabilities](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) and [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime).
>
>Customers with a different AEM Assets license (for example, **AEM Assets Ultimate**) can use the same integration; only the AEM release affects the onboarding steps, not the license type.

## Key benefits

* **Centralized asset management**: Manage all product images in AEM Assets, the enterprise-grade digital asset management solution.
* **Automatic synchronization**: Product images automatically sync when assets are approved or updated in AEM Assets.
* **Dynamic Media delivery**: Leverage Dynamic Media with OpenAPI capabilities for optimized image delivery.
* **Catalog layers**: Product images are applied as a catalog layer, allowing you to overlay AEM Assets imagery on your base catalog.

## How it works

The integration has two independent event flows. Both use [Adobe I/O Events](https://developer.adobe.com/events/docs/) to transfer events to the Assets integration service, but each direction uses its own event provider:

* **From AEM Assets to the Assets integration service**: When an asset is approved, rejected, or removed, the event is delivered to the Assets integration service. The service matches assets to products using a `match-by-SKU` or a custom matcher strategy, then sends the `product-asset` mappings to [!DNL Commerce Optimizer], where they are stored as product layers.

* **From [!DNL Commerce Optimizer] to the Assets Integration Service**: When a product is updated in [!DNL Commerce Optimizer], the event is delivered to the Assets Integration Service. The service syncs any matching asset mappings back to [!DNL Commerce Optimizer].

The updated images are available through storefront APIs (Catalog Service, Live Search, Product Recommendations).

### Source and layer configuration

Images from AEM Assets are ingested as a catalog layer with the following source configuration:

> Example of a source configuration

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

This configuration ensures that AEM Assets images are applied as an overlay on your base product catalog.

## Prerequisites

Before enabling Product Visuals, ensure you meet the [prerequisites for Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md#prerequisites).

## Setup

To enable the integration, [create a support ticket](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket) with your [!DNL Commerce Optimizer] and AEM Assets details. Adobe Support configures the integration and registers your tenant with the Assets Integration Service.

See [Configure AEM Assets for Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) for onboarding information.

### Configure AEM Assets metadata

To enable automatic product matching, configure your assets in AEM Assets with Commerce metadata.

See [Configure AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first) for the required metadata fields and steps.

## Limitations

Before using Product Visuals, review the [integration limitations](../../aem-assets-integration/get-started/configure-aco.md#limitations) — the layer-related constraints that affect how AEM Assets data merges with your base catalog.

For capacity and usage allocations (asset storage, Dynamic Media operations, user licenses), see [Product Visuals limits](../boundaries-limits.md#product-visuals-limits) in the _Boundaries and Limits guide_.

## Using Product Visuals

After the integration is configured, manage your product images through AEM Assets.

### Add images to products

1. Upload images to your AEM Assets repository.

1. Add Commerce metadata to the asset.

   See [Default automatic matching](../../aem-assets-integration/synchronize/default-match.md) and [Custom automatic matching](../../aem-assets-integration/synchronize/custom-match.md).

1. Approve the asset for delivery. The asset must be in **approved** status to trigger synchronization.

1. The image automatically syncs to [!DNL Commerce Optimizer].

### Apply the AEM-Assets layer

To display AEM Assets images on your storefront, [assign the `AEM-Assets` layer to your catalog view](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## More like this

* [Catalog layers](catalog-layer.md)
* [Catalog views](catalog-view.md)
* [AEM Assets Integration Guide](../../aem-assets-integration/overview.md)
