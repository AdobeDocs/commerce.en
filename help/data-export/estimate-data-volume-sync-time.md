---
title: Estimate data volume and transmission time
description: Learn to estimate the data volume and transmission time required for the [!DNL data export] tool to synchronize feed data between Adobe Commerce and connected services.
role: Admin, Developer
exl-id: 787d05d6-fc2f-4f23-8ea7-ef54330e1f37
TQID: https://experienceleague.adobe.com/nhVfGHgrsvqIjUcWfsVDcriEFwUhRQa9D-4xAU-cAnU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Estimate data volume and transmission time for data sync

Adobe recommends estimating data volume and sync time before starting any data feed synchronization to ensure smooth scheduling and avoid disruptions in site operations. This estimation is important when planning for initial syncs or large scale catalog updates, such as mass price changes.

>[!NOTE]
>
>For [!DNL Adobe Commerce Optimizer Connector] deployments, review the connector-specific supported feeds and batch limits in [Connector modules and feed endpoints](../aco-connector/reference/connector-reference.md#supported-feeds).

By default the data export tool processes data in single-thread mode with a default batch size. With the default configuration, there is no parallelization of the feed submission process. Additionally, this component accepts requests per second (RPS) which translates to the following:

- Up to 10,000 products per minute where a product is a SKU with attributes in a specific storeview
- Up to 50,000 prices per minute

The following factors affect data transmission time during synchronization.

- Thread count is set to 1 (by default)
- Batch size is set to _100_ for all feeds except for the `prices` feed, where it is set to _500_.
- Feed acceptance rate is 2 request per seconds.
- All products are assigned to all existing websites
- For the price calculation scenarios, all products have special and grouped prices assigned to them


## Calculate data transmission per feed

Use the values and formulas in the following table to calculate the data volume and synchronization time for each data feed.

>[!NOTE]
>
>These calculations are based on a transmission rate of 2 requests per second. The speed is based on the time required for data collection and data submission. The actual transmission speed varies depending on the request payload size and the current load on the Commerce application server.

| Feed | Data Example | Formula to Calculate Records | Predicted Request Count | Predicted Resync Time |
| --- | --- | --- | --- | --- |
| Products | Products (P): 10000, Store Views (SV): 4 | P * SV = 40000 | 40000 / Batch Size (100) = 400 requests | (400 requests * 0.5 seconds per request) / 60 = 3.3 minutes |
| Categories | Categories &#40;C&#41;: 500, Store Views (SV): 4 | C * SV = 2000 | 2000 / Batch Size (100) = 20 requests | (20 requests * 0.5 seconds per request) / 60 = 0.1 minutes (4 seconds) |
| Prices | Products (P): 10000, Customer Groups (CG): 6 (for example, unique price in shared catalog), Websites (WS): 2 | P \* WS * CG = 120000 | 120000 / Batch Size (500) = 240 requests | (240 requests * 0.5 seconds per request) / 60 = 2 minutes |
| Product Overrides | Products with permissions or in shared catalog (P): 10000, Affected Customer Groups (CG): 5, Assigned Websites WS: 2 | P \* WS * CG  = 100000 | 100000 / Batch Size (100) = 1000 requests | (1000 requests * 0.5 seconds per request) / 60 = 8.3 minutes |
| Product Variants | Variants (child products) assigned to configurable products (PV): 100000 | PV = 100000 | 100000 / Batch Size (100) = 1000 requests | (1000 requests * 0.5 seconds per request) / 60 = 8.3 minutes |
| Category Permissions | Count of all Category Permissions + 4 fallback records (CP): 10000 | CP = 10000 | 10000 / Batch Size (100) = 100 requests | (100 requests * 0.5 seconds per request) / 60 = 0.8 minutes (50 seconds) |
| Inventory Stock Status | Products (P): 10000, Stocks products assigned to (S): 5 (assuming every product is assigned to every stock) | P * S = 50000 | 50000 / Batch Size (100) = 500 requests | (500 requests * 0.5 seconds per request) / 60 = 4.2 minutes |
| Sales Orders | All order records (including invoices, shipments, and so on) (SO): 10000 | SO = 10000 | 10000 / Batch Size (100) = 100 requests | (100 requests * 0.5 seconds per request) / 60 = 0.8 minutes (50 seconds) |

>[!MORELIKETHIS]
>
> - [Improve data export performance](customize-export-processing.md)
> - [Manage synchronization](data-sync-manage.md)
> - [How synchronization works](sync-overview.md)
