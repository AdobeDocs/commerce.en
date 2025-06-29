---
title: What is Adobe Commerce Optimizer?
description: Learn about [!DNL Adobe Commerce Optimizer] and its key features.
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: f9516d4c-fbae-4db2-a1a9-cda3684a8122
---
# What is [!DNL Adobe Commerce Optimizer]?

[!DNL Adobe Commerce Optimizer] enhances your e-commerce experience with a high-performance storefront, boosting organic traffic, customer engagement, and revenue.

With [!DNL Adobe Commerce Optimizer], you can:

- Grow and scale your catalog without re-platforming your entire commerce stack.
- Ingest catalog data from any source.
- Define business catalog views and policies.
- Create personalized search and recommendations using AI and ML.
- View crucial product data availability, including synchronization status and storefront eventing data for accurate implementation and troubleshooting.

Watch the following video for a high-level overview of [!DNL Adobe Commerce Optimizer]:

>[!VIDEO](https://video.tv.adobe.com/v/3450226)

## Who benefits the most from [!DNL Adobe Commerce Optimizer]?

[!DNL Adobe Commerce Optimizer] is for:

- Merchants who want to maintain their existing backend commerce system and only transform storefront experiences.
- Businesses where a third-party system manages the cart and checkout lifecycle.
- AEM customers seeking a simple way to manage their product catalog from a third-party commerce engine.

## Quick tour

When you first launch [!DNL Adobe Commerce Optimizer], you see the following:

![[!DNL Adobe Commerce Optimizer] UI](./assets/user-interface.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Home]

Preview key metrics and activities for your store. The home page also includes quick links to configure search and recommendations.

>[!TAB Success metrics report]

This page provides an overview of the key performance metrics for your store. The goal is for you to quickly understand the results of implementing [!DNL Adobe Commerce Optimizer] then help you and your team identify opportunities for growth, and highlight areas for optimization.

>[!TAB Search performance]

The *Search performance* page provides insight into the search terms that shoppers use. The information can be used to identify trends, increase click-through, and improve the conversion rate.

>[!TAB Merchandising]

Create personalized experiences for your shoppers through product discovery and product recommendations.

- **Recommendations** - Uses artificial intelligence and machine-learning algorithms to perform a deep analysis of aggregated visitor data. This data, when combined with your catalog, results in a highly engaging, relevant, and personalized experience. Recommendations are surfaced on the storefront as units with labels, such as "Customers who viewed this product also viewed". You can create, manage, and deploy recommendations directly from [!DNL Adobe Commerce Optimizer].
- **Merchandising rules** - Enhances your site search functionality, ensuring a seamless and efficient shopper experience that maximizes conversion rates. It enables merchandisers to ensure that shoppers get the right products at the right time.  
- **Facets** - Enhances your site search functionality, ensuring a seamless and efficient shopper experience that maximizes conversion rates. It enables merchandisers to ensure that shoppers get the right products at the right time.  
- **Synonyms** - Enhances your site search functionality, ensuring a seamless and efficient shopper experience that maximizes conversion rates. It enables merchandisers to ensure that shoppers get the right products at the right time.  

>[!TAB Store Setup]

Define your catalog views and policies. The catalog not only contains your product data, but it also helps you define your business structure. Also, you can view valuable insights into the availability of product data for your storefront, ensuring it can be promptly displayed to your shoppers.

- **Catalog views** - Help you define your retail structure into meaningful business groups. For example, dealers for the automobile industry, subsidiaries for multi brand conglomerates, or manufacturing locations for suppliers.
- **Policies** - Data access filters that are housed within catalog views. Policies help to ensure that the right content is sent to the right destination. For example, point of sale physical stores, marketplaces, advertisement pipelines (Google, Facebook, Instagram). 
- **Data Sync** - Displays an overview of the synchronization status for product data transferred from their data source (PIM, ERP, and so on) into [!DNL Adobe Commerce Optimizer]. That product data is displayed within the **[!UICONTROL Catalog Service]**, **[!UICONTROL Search]**, and **[!UICONTROL Recommendations]** tabs.
- **Events** - Displays storefront event data which powers Product Discovery and Recommendations. The **Events** page lets the merchant verify that they have implemented storefront eventing correctly and that events are being successfully captured. Merchants can use this page to identify potential problems and take steps to resolve any eventing issues.

>[!ENDTABS]

## Key Capabilities

Key capabilities include:

- **Third-party catalog ingestion** - Ingest catalog data from any third-party source (your existing Commerce catalog, PIM, ERP, and so on). Your catalog data is directly ingested into the merchandising services layer, which is a SaaS component called Merchandising Services powered by Catalog views and Policies (Catalog views and Policies).
- **Merchandising Services powered by Catalog views and Policies** - This solution is the foundational piece of [!DNL Adobe Commerce Optimizer]. Merchandising Services powered by Catalog views and Policies is a highly scalable, flexible catalog data model which unlocks multi-brand, multi-business unit, and multi-language use cases. These merchandising services provide building blocks that merchants can use to create and manage catalogs at scale. Within [!DNL Adobe Commerce Optimizer], you can manage your catalog by creating catalog views and policies that best define your business goals. In addition, the merchandiser can provide personalized experiences to drive traffic and engagement using product discovery, recommendations​, and intelligent merchandising.
- **Before and After metrics** - Provides real-time insights into the performance of your commerce initiatives. You can view before and after results of specific KPIs and evaluate the impact of changes and optimize for better results. You can export the results in a PDF.
- **Commerce storefront powered by Edge Delivery** - With Edge delivery, you can launch your site quickly using prebuilt storefront components with integrated commerce functionality — including product listing pages, product detail pages, cart, and checkout.
- **Third-party cart and checkout** - Use API mesh and App builder to integrate with third-party cart and checkout systems.

## Architecture

The following diagram describes the basic architecture of [!DNL Adobe Commerce Optimizer], from catalog data ingestion to the relationship between merchandising services, your storefront, and the integration with a third-party cart and checkout process.

![[!DNL Adobe Commerce Optimizer] Architecture](./assets/architecture.png)
