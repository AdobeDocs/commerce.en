---
title: Configure AEM Assets for Commerce Optimizer
description: Learn how to configure AEM Assets Integration for [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
---

# Configure AEM Assets for [!DNL Adobe Commerce Optimizer]

[!BADGE SaaS only]{type=Positive tooltip="Applies to Adobe Commerce Optimizer projects only."}

The AEM Assets Integration for [!DNL Adobe Commerce Optimizer] enables merchants to use AEM Assets as the centralized digital asset management solution for product images. This guide covers the configuration specific to [!DNL Commerce Optimizer].

Unlike Adobe Commerce (PaaS) or [!DNL Adobe Commerce as a Cloud Service], [!DNL Commerce Optimizer] does not have an Admin configuration UI. To enable the integration, create a support ticket with your [!DNL Adobe Commerce Optimizer] and AEM Assets details. Adobe Support configures the integration and registers your tenant with the Assets Integration Service.

**Prepare AEM Assets before you submit the ticket.** Tenant registration assumes the AEM side is usable for Commerce. For example, after you deploy the AEM Commerce `assets-commerce` package so metadata and events work as explained. **Opening a ticket before AEM is configured can delay onboarding.**

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
* Dynamic Media with OpenAPI enabled on your AEM Assets environment (see [Configure the AEM Assets project](configure-aem.md#prerequisites) for enablement steps).

## Configure AEM Assets first

Complete the AEM Assets steps **before** you [open a support ticket](#onboarding) for tenant registration. The installation pattern matches Adobe Commerce as a Cloud Service—see [Configure the AEM Assets project to support Commerce metadata](configure-aem.md).

### Step 1: Deploy the AEM Commerce package

Install and deploy the `assets-commerce` package in your AEM project so Commerce metadata schemas, events, and UI are available.

Complete the full procedure in [Install the `assets-commerce` package](configure-aem.md#step-1-install-the-assets-commerce-package). Before you open a support ticket, follow these steps:

1. Clone the Cloud Manager Git repository and copy the [AEM Assets Commerce repository](https://github.com/ankumalh/assets-commerce) code into your project.

1. In all `filter.xml` and `pom.xml` files for your project, replace all occurrences of &lt;my-app&gt; with your app name.

1. Commit, push, run your deployment pipeline, and validate that the **[!UICONTROL Commerce]** tab appears on asset properties.

See [Install the `assets-commerce` package](configure-aem.md#step-1-install-the-assets-commerce-package) for Cloud Manager screenshots, pipeline steps, and troubleshooting if the **[!UICONTROL Commerce]** tab is missing.

### Step 2: Enable Dynamic Media with OpenAPI

Dynamic Media with OpenAPI capabilities must be enabled on your AEM Assets environment. Self-service paths (for example Cloud Manager for Product Visuals) and Adobe Support routes are described under [Configure the AEM Assets project](configure-aem.md#prerequisites).

### Step 3: Apply Commerce metadata and approve assets

Add Commerce metadata to your product images in AEM Assets—for field definitions see [AEM Commerce package contents](configure-aem.md#aem-commerce-assets-commerce-package-contents).

The asset must be in an **approved** status for the data sync to trigger. Saving metadata alone does not trigger the event.

### Step 4: Optional — configure a Commerce metadata profile

If you choose to use AEM metadata profiles to streamline authoring, configure them **after** the package is deployed and your team understands required Commerce fields—same optional pattern as **Configure the AEM Assets project**.

See [Configure a metadata profile](configure-aem.md#step-2-optional-configure-a-metadata-profile).

## Limitations

The [!DNL Commerce Optimizer] integration has the following limitations:

### Layer-related constraints

Read this section **before** you choose a catalog layer name in your support ticket. Choosing or sharing layers without this context is a frequent cause of preventable support cases.

**Use a dedicated layer for AEM Assets content.** Payloads sent from AEM Assets populate a Commerce Optimizer catalog **layer**. Values in that layer **overwrite** base catalog attributes where fields are supplied. When the integration omits a field in the payload, the corresponding values in that layer may be overwritten with empty values. Sharing a layer with unrelated Commerce workflows—or reusing a layer that already stores non–AEM-Assets product data—can cause **unintended data loss** or confusing overwrites. Plan the layer choice **before** you open your support ticket, and reserve that layer name (for example the default **`AEM-Assets`**) primarily for AEM-driven product image sync.

>[!IMPORTANT]
>
>The integration supports **one catalog source per tenant**: a single locale and **one named layer**. Configuring multiple AEM-Assets layers or multiple locales for the same tenant is not supported at this time.

### Other constraints

* **Images only**: The integration does not support video or other media types at this stage.
* **No category images**: Category image synchronization is not available. Category images from AEM Assets for the Assets Selector (UI insertion) are not supported.
* **No multi-site distinction**: The integration does not handle multi-site; an image associated with a product is shown the same across all channels and policies.
* **Image position / ordering**: Image position and ordering are not supported.
* **Product must exist**: If the product does not exist in [!DNL Commerce Optimizer], the layer is not created for that product-asset mapping.

## Onboarding

To onboard AEM Assets Integration with [!DNL Commerce Optimizer], you must [Create a support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

Adobe Support uses the information in your ticket to register your tenant with the Assets Integration Service, and configure the integration.

Ensure you finished [Configure AEM Assets first](#configure-aem-assets-first) before submitting the ticket.

Include the following information in your support ticket:

* **[!DNL Adobe Commerce Optimizer] Tenant ID** (Instance ID) found in your [!DNL Commerce Optimizer] URL or Commerce Cloud Manager UI.
* **AEM Program ID**.
* **AEM Environment ID**.
* **Matching rule**: Match by SKU or [external matcher (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Layer**: The catalog layer name to register the tenant with (see **Layer-related constraints**). Specify a custom name only if intentional; otherwise the default **`AEM-Assets`** is used.
* **Locale**: The catalog source locale to register the tenant with (for example, `en-US`). This must match the locale you use in your catalog view and product catalog data.

After Adobe Support processes your ticket, the integration is configured and your tenant is registered with Assets Integration Service.

Once onboarding is complete:

1. **Registration with Assets Integration Service**: Your [!DNL Commerce Optimizer] tenant is registered with the Assets Integration Service using your [!DNL Adobe Commerce Optimizer] Tenant ID, AEM Program ID, AEM Environment ID, matching rule, locale, and layer name supplied in the ticket.

1. **Event subscription**: Assets Integration Service subscribes to:

   * AEM Assets events (asset approved, updated, removed)
   * [!DNL Commerce Optimizer] catalog events (product created, updated)

Configure your [catalog view](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) so storefront and APIs surface AEM-driven image data:

* **Catalog source (locale)** — Select the same locale you specified in your support ticket (for example **`en-US`**). The integration registers one locale per tenant; a mismatch prevents synced images from appearing in the intended catalog view.
* **Catalog layer** — Assign the **`AEM-Assets`** layer (or your custom layer name from the ticket) to that catalog view.

If the locale or layer is not assigned correctly, image data may **not appear** or may behave unexpectedly—even though sync succeeded upstream.

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
