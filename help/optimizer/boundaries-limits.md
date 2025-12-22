---
title: Limits and boundaries
description: Understand [!DNL Adobe Commerce Optimizer] limits and boundaries to plan capacity and prevent performance issues.
role: Admin, Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
---
# Limits and boundaries

[!DNL Adobe Commerce Optimizer] has two types of limits:

- **License limits**—Based on your purchased capacity; can be expanded by purchasing additional packages.
- **System boundaries**—Fixed limits that protect system resources and ensure reliable performance for all users.

Your usage must stay within these limits. Exceeding them can cause:

- Degraded performance
- Increased latency
- Request throttling
- Service interruption

>[!TIP]
>
>**Need more capacity?** Contact your Adobe Account representative to purchase additional packages. For questions about system limits, contact [Adobe Support](https://experienceleague.adobe.com/home#support).

## How to prevent performance issues

Follow these best practices to stay within limits and avoid service disruptions:

- **Review your limits**—Understand your [capacity limits](#adobe-commerce-optimizer-limits) before launching new storefronts or campaigns.
* **Track your usage**: Use built-in metrics dashboards or CDN logs.
- **Plan for peak periods**—Before sales events, product launches, or seasonal promotions, verify you have sufficient capacity.
- **Provision environments early**—Add sandbox or production environments before development and testing workloads increase.

Follow these best practices to stay within limits and avoid service disruptions:

- **Review your limits**—Understand your [capacity limits](#adobe-commerce-optimizer-limits) before launching new storefronts or campaigns.
- **Monitor usage trends**—Check CDN logs and built-in metrics dashboards.
- **Plan for peak periods**—Before sales events, product launches, or seasonal promotions, verify you have sufficient capacity.
- **Provision environments early**—Add sandbox or production environments before development and testing workloads increase.

## Adobe Commerce Optimizer limits

The following tables summarize the limits by capability area and include information about whether the limit can be expanded by purchasing additional capacity.

>[!NOTE]
>
> For information about packages available for increasing capacity, see the [Adobe Commerce Optimizer product licensing description](https://helpx.adobe.com/legal/product-descriptions/adobe-commerce-optimizer.html).

### SaaS environment limits

| **Environment**              | **Description**                            | **Limit**      | **Expandable?** |
| ---------------------------- | -------------------------------------------| ---------------| ----------------|
| **Sandbox environment**      | Number of sandbox environments included    | 2 per instance | Yes |
| **Production environment**   | Number of production environments included | 1 per instance | Yes |

### Catalog

| **Capability**            | **Description**                               | **Limit**      | **Expandable?**   |
|---------------------------|---------------------------------------------------|----------------|---------------|
| Product ingestion rate    | Number of catalog updates allowed | 1K/minute (100K/day max) | Yes       |
| Catalog retrieval rate    | Monthly allowance for catalog retrieval API calls | 10M            | Yes           |
| Products in a single catalog source | Maximum number of SKUs supported in the catalog   | 250K SKUs      | Yes           |
| Catalog Variations                  | Number of catalog variations<br>(#Catalog Views × #PriceBooks) | 100 variations    |  Yes |
| Storefront Content Request | Monthly allowance for storefront content   | 2M requests/month         | Yes |
| Catalog sources            | Number of product data pools (locales) | 50  | No |
| Variants per product       | Number of product variants (size, color combinations) allowed per product | 10K  | No            |
| Catalog views | Number of configurable subsets of your master catalog | 30K per instance     | No |
| Policies per catalog view  | Number of data filters allowed  | 10  | No            |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100  | No |

### Assets and media

| **Capability**            | **Description**                                             | **Limit**            | **Expandable?** |
| ------------------------- | ----------------------------------------------------------- | -------------------- | --------------- |
| Dynamic Media operations  | Monthly allowance for dynamic media processing operations   | 5M operations/month  | Yes |
| GenAI variations          | Monthly allowance for generative AI content variations      | 1K variations/month  | Yes |


### Price books

| **Capability**             | **Description**                                      | **Limit** | **Expandable?** | **Notes** |
| -------------------------- | ---------------------------------------------------- | --------- | --------------- | --------- |
| Price books                | Number of price books allowed per instance           | 1,000     | Yes             | Divide the catalog variations by the catalog views to find the number of price books. See [Catalog Variations limit](#catalog). |
| Discounts per price record | Number of discounts that can be applied to a product | 10        | No              |           |

### Product discovery and storefront

| **Capability**  | **Description**       | **Limit**       | **Expandable?**  | **Notes**           |
|-----------------|-----------------------|------------------|------------|--------------------------|
| Products per search request | Maximum number of products returned per page in search results  | 100  | No         |                                      |
| Filterable attributes | Number of product characteristics (like color, size, brand, or material) that can be enabled for layered navigation and facets | 200 |      No |                                 |
| Searchable attributes | Number of product characteristics that can be configured for use with the product catalog search service | 200  | No            |                                        |
| Sortable attributes | Number of product characteristics that can be configured for determining the order of search result values | 50 |  No |   |
| Search pagination depth | Maximum number of products accessible through pagination (for example, page 100 × 100 products/page) | 10K |  No    |     |
| Facets | Number of filterable product attributes (like Brand, Color, Size, Price) that can be configured to help shoppers refine search results and browse categories | 100 | No | Must be filterable attributes          |
| Options per facet | The number of filterable product attribute values (like "Red," "Blue" for Color; "Small," "Medium" for Size) that shoppers can select from a list | 100              | Yes | Can increase via support request       |


### Recommendations

The following capabilities are available for product recommendations. Some features available in other Adobe Commerce products are not supported in [!DNL Adobe Commerce Optimizer].

| **Capability** | **Description** | **Limit**    | **Expandable?** | **Notes**                         |
|----------------|-----------------|--------------|-----------------|-----------------------------------|
| Active recommendation units | Number of live recommendation components on your storefront (like "Customers also viewed" or "You might also like") | 50 | No  |   |
| Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | — | No | Not supported |
| Preview recommendations | Preview how recommendations appear on the storefront before publishing | — | No | Not supported |

### Extensibility

| **Capability**  | **Description**     | **Limit** |  **Expandable?** |   **Notes**      |
| ---------------- | ------------------ | --------- | ------------ | ------------- |
| Adobe Developer App Builder | Capacity for building cloud-native extensions and integrations | 1 pack/year | Yes | See the [App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html) for limits defined per pack. |
| Adobe I/O Runtime | Capacity of the underlying serverless runtime (I/O Runtime) and eventing (I/O Events) services to support App Builder | — | — | See [System Settings](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) in the *App Builder Runtime Guides*.|

<!--## How to size your solution

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
   * Add-On: 10 × dynamic media packs (1M each) -->
