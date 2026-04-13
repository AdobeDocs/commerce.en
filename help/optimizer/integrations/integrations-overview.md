---
title: Commerce Optimizer Integrations
description: Learn about Adobe Commerce Optimizer integrations for catalog sync, asset management, storefront optimization, and Salesforce Commerce Cloud connectivity.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
---

# [!DNL Adobe Commerce Optimizer] integrations

[!DNL Adobe Commerce Optimizer] includes integrations that let you sync data from Adobe Commerce on cloud or on-premises, manage assets, improve storefront experiences, and connect external systems. The sections below describe how each integration works with [!DNL Adobe Commerce Optimizer]. Follow the links for setup, configuration, and day-to-day use.

## Adobe Commerce Optimizer Connector {#aco-connector}

The Adobe Commerce Optimizer Connector is the bridge that synchronizes catalog and pricing data between Adobe Commerce (cloud or on-premises) and [!DNL Adobe Commerce Optimizer]. When you enable the connector, Commerce remains the system of record for product data while [!DNL Adobe Commerce Optimizer] powers product discovery, recommendations, merchandising rules, analytics, and headless storefront experiences.

- [Adobe Commerce Optimizer Connector overview](../../aco-connector/overview.md){target="_blank"}
- [Get started with the connector](../../aco-connector/get-started.md){target="_blank"}

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

## Commerce Salesforce Connector {#commerce-salesforce-connector}

The Commerce Salesforce Connector (built on Adobe App Builder) syncs catalog and price data from Salesforce Commerce Cloud B2C into [!DNL Adobe Commerce Optimizer] so you can use Adobe storefront and merchandising capabilities without replatforming your Salesforce commerce backend. You can schedule syncs, run on-demand updates, and extend the integration using Salesforce Commerce APIs.

- [Salesforce Commerce Connector](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Adobe Commerce Optimizer technical documentation](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Get started with Adobe Commerce Optimizer](../get-started.md)
