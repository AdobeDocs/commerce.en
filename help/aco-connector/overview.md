---
title: Adobe Commerce Optimizer Connector
description: Learn how to connect your data from your Commerce cloud or on-premises project to Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# Adobe Commerce Optimizer Connector

The Adobe Commerce Optimizer Connector is the integration bridge that synchronizes catalog and pricing data between an Adobe Commerce on cloud infrastructure or on-premises deployment and [!DNL Adobe Commerce Optimizer]. Syncing data to Adobe Commerce Optimizer enables features such as dynamic AI search, recommendations, fast-loading headless storefronts, including Adobe Commerce storefronts on Edge Delivery Services, and real-time performance analytics.

## Architecture and experience

The Adobe Commerce Optimizer Connector operates by mapping Commerce websites and store views to a Commerce Optimizer project as shown in the following figure:

![Mapping Commerce data to Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.svg){width="600" zoomable="yes"}

When data is exported from Commerce to Commerce Optimizer:

* Commerce store views are mapped to catalog sources
* Websites are mapped to price books

The associated catalog and price data is exported and later used to create catalog views and optionally define a policy to filter the catalog and price data for specific business use cases.

Instead of configuring and managing Commerce Services (Live Search and Product Recommendations) from the Commerce Admin, you use [[!DNL Adobe Commerce Optimizer] Merchandising tools](../optimizer/merchandising/overview.md) to manage product discovery (Live Search) and recommendations (Product Recommendations) rule configuration. The Adobe Commerce instance becomes the data source for catalog and price data. When the data is updated in Commerce, the updates are synced to the [!DNL Adobe Commerce Optimizer] instance.

## Workflows

The Connector enables several key workflows:

* **Export Commerce catalog data to [!DNL Adobe Commerce Optimizer]**—price and price book data is exported at the website and customer group level. Product and product attribute data is exported at the `store view` level. By default, catalog data sync is enabled for all Commerce scopes (websites and store views).

  To enable this workflow, install the `adobe-commerce/commerce-data-export-aco-adapter` PHP extension, review the exporter configuration, and then enable the integration between Commerce and Commerce Optimizer from the Commerce Admin. For detailed instructions, see [Get Started](#get-started).

* **Map the Commerce website and store view data to export to [!DNL Adobe Commerce Optimizer]**

  Optionally, customize the export settings to sync data only for specific websites or store views. For example, you can choose to export catalog data for only one store view to use for a specific use case, such as optimizing the search and discovery experience for a specific market or region.

* **Merchandising rule configuration and management**

  When the Connector is enabled, merchandising rules for product discovery and recommendations are defined and managed from the [!DNL Adobe Commerce Optimizer] UI, not from the [!UICONTROL Live Search] and [!UICONTROL Product Recommendations] pages in the Commerce Admin.

* **Deploy your Commerce Storefront on Edge Delivery Services**

  After setting up the integration with [!DNL Adobe Commerce Optimizer], you can set up and deploy a Commerce Storefront on Edge Delivery Services to deliver ultra-fast performance, scalability, seamless content authoring, integrated personalization, and reduced operational costs using the composable, API-driven architecture and modular components available with [!DNL Adobe Commerce Optimizer].

For details on how to set up the integration and enable these workflows, see [Get Started](get-started.md).
