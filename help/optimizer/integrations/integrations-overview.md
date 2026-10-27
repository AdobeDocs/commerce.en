---
title: Commerce Optimizer Integrations
description: Learn about Adobe Commerce Optimizer integrations for catalog sync, asset management, storefront optimization, and Salesforce Commerce Cloud connectivity.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---

# [!DNL Adobe Commerce Optimizer] integrations

[!DNL Adobe Commerce Optimizer] includes integrations that let you sync data from Adobe Commerce on cloud or on-premises, manage assets, improve storefront experiences, and connect external systems. The sections below describe how each integration works with [!DNL Adobe Commerce Optimizer]. Follow the links for setup, configuration, and day-to-day use.

{{aco-integration-environment-alignment}}

## Product Visuals with AEM Assets {#product-visuals}

Product Visuals lets you manage product images through Adobe Experience Manager (AEM) Assets. Configure AEM Assets for Commerce Optimizer to enable Product Visuals. After you finish configuration, you use AEM Assets as the centralized digital asset management solution for your product images, with automated asset review and management workflows that keep images in sync with your Commerce Optimizer catalog. The integration matches assets to products by SKU. Updates flow through Adobe's integration services so storefronts reflect the latest media without manual re-uploads.

- [Product Visuals with AEM Assets](../setup/product-visuals.md)
- [Configure AEM Assets for Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer analyzes Commerce websites and improves performance by surfacing AI-driven **[!UICONTROL Opportunities]**—recommendations that help you improve discovery, engagement, and conversions.

>[!AVAILABILITY]
>
>This capability requires the **Ultima** Adobe Sites Optimizer license. You can request a license through your Adobe Customer Technical Advisor. Once your account is provisioned, the Opportunities feature is available in the [!DNL Adobe Commerce Optimizer] interface, and you can start using AI-driven insights to optimize your storefront and merchandising strategies.

- [Opportunities](../manage-results/opportunities.md)

## Adobe Commerce Optimizer Connector {#aco-connector}

The Adobe Commerce Optimizer Connector is the bridge that synchronizes catalog and pricing data between Adobe Commerce (cloud or on-premises) and [!DNL Adobe Commerce Optimizer]. When you enable the connector, Commerce remains the system of record for product data while [!DNL Adobe Commerce Optimizer] powers product discovery, recommendations, merchandising rules, analytics, and headless storefront experiences. To restrict who can query a synced catalog view, see [Private catalog views](../setup/private-catalog-view.md).

- [Adobe Commerce Optimizer Connector overview](../../aco-connector/overview.md){target="_blank"}
- [Get started with the connector](../../aco-connector/get-started.md){target="_blank"}

## Third-party cart and checkout integration

Adobe Commerce Optimizer can power product discovery and merchandising for a storefront that uses a separate commerce platform for transactions. The storefront uses Commerce Optimizer Merchandising Services APIs for product data, search, recommendations, and merchandising. The host commerce platform remains responsible for shopper accounts, cart, checkout, and order processing. Integration with the host platform is a custom implementation, using API Mesh, App Builder, direct APIs, or a combination of these tools.

For Salesforce Commerce Cloud (SFCC), the [Adobe Commerce Optimizer SFCC Checkout Starter Kit](https://github.com/adobe-commerce/aco-sfcc-checkout-starter-kit) provides example Edge Delivery Services blocks and scripts for connecting an Adobe Commerce Optimizer storefront to SFCC shopper, cart, and checkout functionality. Use it as a reference implementation and adapt it to your storefront; it is not a generic, out-of-the-box connector. A [headless storefront example for Next.js](https://github.com/adobe-commerce/aco-sfcc-storefront-next){target="_blank"} is also available.

The [Commerce Checkout Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/) is a separate App Builder starter kit for Adobe Commerce checkout extensions. It is not the ACO-to-SFCC storefront integration example.

## Commerce Salesforce Connector {#commerce-salesforce-connector}

The Commerce Salesforce Connector (built on Adobe App Builder) syncs catalog and price data from Salesforce Commerce Cloud B2C into [!DNL Adobe Commerce Optimizer] so you can use Adobe storefront and merchandising capabilities without replatforming your Salesforce commerce backend. You can schedule syncs, run on-demand updates, and extend the integration using Salesforce Commerce APIs.

- [Salesforce Commerce Connector](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Adobe Commerce Optimizer technical documentation](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Get started with Adobe Commerce Optimizer](../get-started.md)
