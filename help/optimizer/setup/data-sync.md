---
title: Data sync
description: Review the catalog data that is being synchronized from your Commerce data source into [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
---
# Data Sync

The **Data Sync** page displays an overview of the synchronization status for product data transferred from your data source (your existing Commerce catalog, Product Information Management (PIM) system, Enterprise Resource Planning (ERP) system, and so on) into [!DNL Adobe Commerce Optimizer].

The **Data Sync** page provides valuable insights into the availability of product data for your storefront, ensuring that it can be promptly displayed to your shoppers.

The **Data Sync** page is located at *Setup* > **Data sync**.

![Data Sync](../assets/data-sync.png)

The **Data Sync** page contains the following fields:

|Field|Description|
|--- |--- |
| Catalog source | Specific locale for the synced data.|
|[!DNL Catalog Service]|Displays the latest sync update, the total products received, a search field, and a table of the synced products for [!DNL Catalog Service].|
|Product Discovery|Displays the latest sync update, the total products received, a search field, and a table of the synced products for Search.|
|Recommendations|Displays the latest sync update, the total products received, a search field, and a table of the synced products for Recommendations.|
|Products received in the last 3 hours|Displays the number of products that have been transferred from the catalog source to Adobe Commerce Optimizer within the last three hours. If you make infrequent updates to your catalog, this value is frequently zero.|
|Total products in catalog|Reflects the total number of catalog products available to Adobe Commerce Optimizer.|
|Synced products|Provides details about the products synced to Adobe Commerce Optimizer. By default, this table is sorted by 'Last Updated'. To find a specific product, use the **[!UICONTROL Search by Name or SKU]** field.|

## List of synced products

To see the details of a synced product in JSON format, click on the code icon ![Code link](../assets/data-sync-details.png) on the row of the product from the synced products table.

![Syncd Product Details](../assets/synced-products.png)

## Resync catalog data

If you do not see specific products on the **Data Sync** page, you need to initiate a resync from your upstream system. However, keep in mind that a resync can increase the load on hardware resources. Nevertheless, resyncing your catalog might be necessary in the following scenarios:

- When significant changes are made to your product catalog, such as adding new products, updating product details, or modifying categories

- If you notice any discrepancies or performance issues in displaying product data on your storefronts

>[!IMPORTANT]
>
>The time it takes to complete the sync varies based on your catalog size and the volume of data updated.
