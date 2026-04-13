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

[!DNL Adobe Commerce Optimizer] provides several integrations that allow you to sync data from an Adobe Commerce on cloud or on-premises environment, manage assets, improve storefront experiences, and connect external systems. Use the sections below to understand how each integration works with [!DNL Adobe Commerce Optimizer] and follow the links for setup, configuration, and day-to-day use.

## Adobe Commerce Optimizer Connector

The Adobe Commerce Optimizer Connector is the bridge that synchronizes catalog and pricing data between Adobe Commerce (cloud or on-premises) and [!DNL Adobe Commerce Optimizer]. When you enable the connector, Commerce remains the system of record for product data while [!DNL Adobe Commerce Optimizer] powers product discovery, recommendations, merchandising rules, analytics, and headless storefront experiences.

- [Adobe Commerce Optimizer Connector overview](../../aco-connector/overview.md)
- [Get started with the connector](../../aco-connector/get-started.md)

## Product Visuals with AEM Assets

Product Visuals enables Adobe Commerce Optimizer merchants to manage product images through Adobe Experience Manager (AEM) Assets. This capability is enabled by configuring AEM Assets for Commerce Optimizer. Once the configuration is complete, you can use AEM Assets as the centralized digital asset management solution for product images with access to automated asset review and management workflows to keep images in sync with your Commerce Optimizer catalog. The integration matches assets to products by SKU, and updates flow through Adobe's integration services so that storefronts reflect the latest media without manual re-uploads.

- [Product Visuals with AEM Assets](../setup/product-visuals.md)
- [Configure AEM Assets for Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md)

## Adobe Experience Manager Sites Optimizer

Adobe Experience Manager Sites Optimizer analyzes Commerce websites and improves performance by surfacing AI-driven **[!UICONTROL Opportunities]**—recommendations that help you improve discovery, engagement, and conversions.

>[!AVAILABILITY]
>
>This capability requires the **Ultima** Adobe Sites Optimizer license. When Adobe provisions your account with this license, Adobe coordinates enablement through your customer success manager. Once your account is provisioned, the Opportunities feature is available in the [!DNL Adobe Commerce Optimizer] interface, and you can start using AI-driven insights to optimize your storefront and merchandising strategies.

- [Opportunities](../manage-results/opportunities.md)

## Commerce Salesforce Connector

The Commerce Salesforce Connector (built on Adobe App Builder) syncs catalog and price data from Salesforce Commerce Cloud B2C into [!DNL Adobe Commerce Optimizer] so that you can use Adobe storefront and merchandising capabilities without replatforming your Salesforce commerce backend. You can schedule syncs, run on-demand updates, and extend the integration using Salesforce Commerce APIs.

- [Salesforce Commerce Connector](../developer/salesforce-connector.md)
