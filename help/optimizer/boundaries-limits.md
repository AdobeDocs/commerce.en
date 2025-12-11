---
title: Limits and sizing guide
description: Learn about the boundaries and limits for [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
---
# Limits and sizing guide

Adobe Commerce Optimizer packages include predefined limits for various capabilities, each measured by specific metrics. Limits can be categorized by type:

* **Base limits** can be upgraded by purchasing add-on packages
* **Hard limits** reflect maximum system capacity and cannot be exceeded
* **Soft limits** reflect the defined service-level capacity and can potentially be increased by contacting Adobe Support.

The base limits for your Adobe Commerce Optimizer implementation are established in your license agreement based on your project's initial design and requirements. If your business needs additional capacity, you can extend base limits by purchasing add-on packages tailored to your resource needs.

Your product usage must remain within the defined boundaries. If your usage approaches these limits, it may affect system performance.

* For base limits, contact your Adobe Account representative to purchase additional capacity.
* For hard and soft limits, contact Adobe Support to discuss potential solutions.

## How to size your solution

Adobe Commerce Optimizer packages are sized by GMV (Gross Merchandise Value) tiers, each with specific base limits for various metrics. Ask your Adobe representative for a list of available packages and their corresponding limits.

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your current GMV.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each)

## Add-on options table

The following table provides the base limits for [!DNL Adobe Commerce Optimizer]. You can purchase add-on packages to extend base limits as needed.


| **Metric**                            | **Description**                                             | **Base Limits** | **Add-On Unit**                                                               |
| ------------------------------------- | ----------------------------------------------------------- | ------------------------- | ----------------------------------------------------------------------------- |
| **B2C Orders per year** | Annual B2C order volume threshold | varies by GMV tier | Request higher GMV tier for increased order volume |
| **B2B Order per year** | Annual B2B order volume threshold | varies by GMV tier | Request higher GMV tier for increased order volume |
| **Sandbox environment**               | Number of sandbox environments included                     |   2  | Per instance |
| **Production environment**            | Number of production environments included | 1 | Per instance |
| **Catalog Ingestion Rate**            | Number of catalog updates allowed per minute                | 1K updates/min            | +5K updates/min per pack per year OR +10K updates/min per pack per year       |
| **Catalog Retrieval Rate**            | Monthly allowance for catalog retrieval API calls           | 10M calls/month           | +1M API calls/month per pack                                                  |
| **Catalog SKU Count**                 | Maximum number of SKUs supported in the catalog             | 250K SKUs                 | +10K SKUs per pack                                                            |
| **Catalog Variations**                | Number of catalog variations (#Catalog Views × #PriceBooks) | 100 variations            | +100 variations per pack per year                                             |
| **Storefront Content Requests**       | Monthly allowance for storefront content or API requests    | 3M requests/month         | +1M requests/month per pack                                                   |
| **Dynamic Media Operations**          | Monthly allowance for dynamic media processing operations   | 5M operations/month       | +1M operations/month per pack                                                 |
| **Environments (Production)**         | Additional production environment instances                 | 1 Production              | +1 Production environment instance                                            |
| **Environments (Sandbox)**            | Additional sandbox environment instances                    | 2 Sandboxes               | +1 Sandbox instance                                                           |
| **Adobe Developer App Builder Packs** | Additional capacity for App Builder development             | 1 pack/year               | +1 pack/year                                                                  |
| **GenAI Variations**                  | Monthly allowance for generative AI content variations      | 1K variations/month       | +1K variations per pack (or as defined in SKU)                                |

## How to choose add-on packages

* **Track your usage**: Use built-in metrics dashboards or CDN logs.
* **Align with future growth**: Consider upcoming events, new storefronts, or promotional cycles.
* **Plan for environments**: Add environments proactively—do not wait until development or testing workloads peak.
* **Bundle efficiently**: Buying multi-unit packs can simplify contracts and lower administrative overhead.

## Adobe Commerce Optimizer limits

In addition to the limits defined in your license agreement and any purchased add-on packages, Adobe Commerce Optimizer has hard and soft system-defined limits for various capabilities.

The following tables summarize these limits by capability area, including all base, hard, and soft limits.

>[!NOTE]
>
>In the following tables, "—" indicates that no limit applies or the capability is not applicable for that category.

### Catalog

| Capability                             | Volume         | Max Limit        | Limit Type |
|----------------------------------------|----------------|------------------|------------|
| Product ingestion rate (records/min)   | 1K             | 100K             | Base       |
| Product updates per day                | 100K           | —                | Base       |
| Catalog retrieval rate (calls/month)   | 10M            | —                | Base       |
| Products in a single catalog source    | 250K SKUs      | 100M             | Base       |
| Catalog sources                        | —              | 50               | Soft       |
| Variants per product                   | —              | 10K              | Hard       |

### Price books

| Capability                             | Base Limit       | Max Limit       | Limit Type | Notes |
|----------------------------------------|------------------|-----------------|------------|-------|
| Price books per instance               | 1,000            | —               | Hard       | Limit defined by available catalog variations, calculated as #catalog variations=(#pricebooks * #catalog views) |
| Detached price books                   | —               | 30K              | Soft       |       |
| Embedded price books                   | —               | 5K               | Soft       |       |
| Discounts per price record             | —               | 10               | Hard       |       |

### Product discovery and storefront

| Capability                             | Max Limit        | Limit Type | Notes                                  |
|----------------------------------------|------------------|------------|----------------------------------------|
| Products per search request            | 100              | Hard       |                                        |
| Filtrable attributes                   | 200              | Hard       |                                        |
| Searchable attributes                  | 200              | Hard       |                                        |
| Sortable attributes                    | 50               | Hard       |                                        |
| Search offset                          | 10K              | Hard       |                                        |
| Facets                                 | 100              | Hard       | Must be filterable attributes          |
| Options per facet                      | 100              | Soft       | Can increase via support request       |

### Catalog views and policies

| Capability                            | Max Limit       | Limit Type |
|---------------------------------------|-----------------|------------|
| Catalog views per tenant              | 30K             | Soft       |
| Policies per catalog view             | 10              | Soft       |
| Attribute values in a policy          | 100             | Soft       |

### Recommendations

| Capability                             | Max Limit        | Limit Type | Notes                                           |
|----------------------------------------|------------------|------------|-------------------------------------------------|
| Active recommendation units            | 50               | Hard       |                                                 |
| Category or attribute inclusions/exclusions | —           | —          | Not supported                                   |
| Preview recommendations                | —                | —          | Not available in [!DNL Adobe Commerce Optimizer] |
