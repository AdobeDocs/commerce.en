---
title: Estimate data volume and sync time
description: Learn how to estimate data volume and synchronization time for [!DNL Adobe Commerce Optimizer Connector] feeds to plan catalog syncs and avoid disruptions.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---

# Estimate data volume and sync time

Adobe recommends estimating data volume and sync time before starting any feed synchronization to ensure smooth scheduling and avoid disruptions in site operations. This is especially important when planning initial syncs or large-scale catalog updates, such as mass price changes.

By default, the connector processes feeds in single-thread mode. There is no parallelization of the feed submission process. The ingestion API accepts up to 2 requests per second. However, the base allocation for the [!DNL Adobe Commerce Optimizer] ingestion rate limits throughput to the following:

- Up to 1,000 products per minute (a product is a SKU with attributes in a specific store view). See [Limits and boundaries](../../optimizer/boundaries-limits.md) for base allocation details.
- Up to 50,000 prices per minute

## Factors that affect sync time

The estimates below assume the following conditions:

- Thread count: 1 (default)
- Feed acceptance rate: 2 requests per second (0.5 seconds per request)
- All products are assigned to all existing websites

Actual transmission speed varies depending on request payload size and the current load on the Commerce application server.

## Calculate sync time per feed

Use the following table to estimate the number of records, requests, and sync time for each connector feed. Batch size values reflect the limits defined in the [supported feeds](connector-reference.md#supported-feeds) reference.

>[!NOTE]
>
>Product sync time is based on the base allocation limit of 1,000 products per minute. For other feeds, calculations are based on a transmission rate of 2 requests per second. Actual speed depends on payload size and server load.
>
>The prices estimate assumes all customer groups have unique prices.

| Feed | Data example | Formula | Predicted requests | Predicted sync time |
| ---- | ------------ | ------- | ------------------ | ------------------- |
| Products | Products (P): 10,000, Store Views (SV): 4 | P &times; SV = 40,000 records | 40,000 &divide; batch size (100) = 400 | 40,000 &divide; 1,000 records/min = **40 min** |
| Categories | Categories (C): 500, Store Views (SV): 4 | C &times; SV = 2,000 records | 2,000 &divide; batch size (100) = 20 | (20 &times; 0.5 s) &divide; 60 = **~10 s** |
| Product attributes | Attributes (A): 200, Store Views (SV): 4 | A &times; SV = 800 records | 800 &divide; batch size (100) = 8 | (8 &times; 0.5 s) &divide; 60 = **~4 s** |
| Prices | Products (P): 10,000, Websites (WS): 2, Customer Groups (CG): 6 | P &times; WS &times; CG = 120,000 records | 120,000 &divide; batch size (500) = 240 | (240 &times; 0.5 s) &divide; 60 = **2 min** |
| Price books | Websites (WS): 2, Customer Groups (CG): 6 | WS &times; CG = 12 records | 12 &divide; batch size (500) = 1 | (1 &times; 0.5 s) &divide; 60 = **< 1 s** |

>[!MORELIKETHIS]
>
> - [Connector modules and feed endpoints](connector-reference.md) - Review batch limits and supported feeds
> - [Manage synchronization](../data-sync-manage.md) - Monitor sync status and trigger manual resyncs
> - [Connector sync pipeline](../connector-sync-pipeline.md) - Understand how cron schedules and automated sync work
