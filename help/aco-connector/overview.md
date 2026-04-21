---
title: Adobe Commerce Optimizer Connector
description: Learn how to connect your data from your Commerce cloud or on-premises project to Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# Adobe Commerce Optimizer Connector

The Adobe Commerce Optimizer Connector is a native, first‑party integration between Adobe Commerce (cloud or on‑premises) and Adobe Commerce Optimizer. It synchronizes catalog and pricing data from your Adobe Commerce stores into Commerce Optimizer so you can:

- Power **AI‑driven product discovery and recommendations**
- Run **high‑performance headless storefronts** (including Commerce storefronts powered by Edge Delivery)
- Analyze **before-and-after** KPIs and data‑sync health in a single place

Commerce remains your system of record for products, prices, and catalog structure. Commerce Optimizer becomes your experience and merchandising layer, serving fast, relevant results to any connected storefront or channel.

## Key benefits

| Benefit | What it means for you |
|--------|------------------------|
| **No custom connector to build** | Use a supported, first‑party integration instead of writing and maintaining bespoke feeds and scripts. |
| **Faster time‑to‑value with Commerce Optimizer** | Turn on AI search, recommendations, and headless storefronts on top of your existing Adobe Commerce deployment. |
| **Aligned with Commerce scopes** | Automatically maps Websites, Store Views, and customer groups into Commerce Optimizer catalog constructs (Catalog Sources and Price Books). |
| **Operational visibility** | Monitor feed health, last sync times, and per‑SKU status from a dedicated Data Feed Sync Status view. |
| **Future‑ready path toward SaaS** | Provides a low‑risk modernization path from PaaS towards Adobe Commerce as a Cloud Service + Optimizer, without a re‑platform. |

The Adobe Commerce Optimizer Connector is the integration bridge that synchronizes catalog and pricing data between an Adobe Commerce on cloud infrastructure or on-premises deployment and [!DNL Adobe Commerce Optimizer]. Syncing data to Adobe Commerce Optimizer enables features such as dynamic AI search, recommendations, site optimization, and fast-loading headless storefronts, including Adobe Commerce storefronts on Edge Delivery Services, and real-time performance analytics.

## Architecture and experience

The Adobe Commerce Optimizer Connector operates by mapping Commerce websites and store views to a Commerce Optimizer project as shown in the following figure:

![Mapping Commerce data to Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="700" zoomable="yes"}

When data is exported from Commerce to Commerce Optimizer:

* Commerce store views are mapped to catalog sources
* Websites are mapped to price books

The associated catalog and price data is exported and later used to create catalog views and optionally define policies to filter the catalog and price data for specific business use cases.

When the connector is enabled, you can also configure and manage merchandising rules for product discovery and rules for recommendations using [[!DNL Adobe Commerce Optimizer] Merchandising tools](../optimizer/overview.md#quick-tour) The Adobe Commerce instance becomes the data source for catalog and price data. When the data is updated in Commerce, the updates are synced to the [!DNL Adobe Commerce Optimizer] instance.

## Workflows

The Connector enables several key workflows:

* **Export Commerce catalog data to [!DNL Adobe Commerce Optimizer]**—price and price book data is exported at the website and customer group level. Product and product attribute data is exported at the `store view` level. By default, catalog data sync is enabled for all Commerce scopes (websites and store views).

  To enable this workflow, install the `adobe-commerce/commerce-data-export-aco-adapter` PHP extension, review the exporter configuration, and then enable the integration between Commerce and Commerce Optimizer from the Commerce Admin. For detailed instructions, see [Get Started](get-started.md).

* **Map the Commerce website and store view data to export to [!DNL Adobe Commerce Optimizer]**

  Optionally, customize the export settings to sync data only for specific websites or store views. For example, you can choose to export catalog data for only one store view to use for a specific use case, such as optimizing the search and discovery experience for a specific market or region.

* **Merchandising rule configuration and management**

  When the Connector is enabled, merchandising rules for product discovery and recommendations are defined and managed from the [!DNL Adobe Commerce Optimizer] UI, not from the [!UICONTROL Live Search] and [!UICONTROL Product Recommendations] pages in the Commerce Admin.

* **Deploy your Commerce Storefront on Edge Delivery Services**

  After setting up the integration with [!DNL Adobe Commerce Optimizer], you can deploy a Commerce Storefront on Edge Delivery Services. This delivers ultra-fast performance, scalability, seamless content authoring, and integrated personalization using a composable, API-driven architecture.

For details on how to set up the integration and enable these workflows, see [Get Started](get-started.md).
