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

Your usage must stay within these limits. Exceeding them can cause increased latency and request throttling.

>[!TIP]
>
>**Need more capacity?** Contact your Adobe Account representative to purchase additional packages. For questions about system limits, contact [Adobe Support](https://experienceleague.adobe.com/home#support).

## How to prevent performance issues

Follow these best practices to stay within limits and avoid service disruptions:

- **Review your limits**—Understand your [capacity limits](#adobe-commerce-optimizer-limits) before launching new storefronts or campaigns.
- **Track your usage**—Use built-in metrics dashboards or CDN logs.
- **Plan for peak periods**—Before sales events, product launches, or seasonal promotions, verify you have sufficient capacity.
- **Provision environments early**—Add sandbox or production environments before development and testing workloads increase.

## Adobe Commerce Optimizer limits

The following tables summarize the limits by capability area and include information about whether the limit can be expanded by purchasing additional capacity.

>[!NOTE]
>
> For information about packages available for increasing capacity, see the [Adobe Commerce Optimizer product licensing description](https://helpx.adobe.com/legal/product-descriptions/adobe-commerce-optimizer.html).

### Environment limits

| **Environment**              | **Description**                            | **Limit**      | **Expandable?** |
| ---------------------------- | -------------------------------------------| ---------------| ----------------|
| **Sandbox environment**      | Number of sandbox environments included    | 2 per instance | Yes<br>License additional environments per instance |
| **Production environment**   | Number of production environments included | 1 per instance | Yes<br>License additional environments per instance|

{style="table-layout:auto"}

### Catalog

| **Capability**            | **Description**                               | **Limit**      | **Expandable?**   |
|---------------------------|---------------------------------------------------|----------------|---------------|
| Product ingestion rate    | Number of products created or updated | 1K/minute (100K/day) | Yes<br>Add 5K/minute or 10K/minute data ingestion license packs |
| Product payload size | Maximum amount of data allowed when creating, updating, or ingesting product information using the API | 200 KB | No |
| Catalog Variations                  | Number of catalog variations<br>(*Number of Catalog Views × Number of Price Books*) | 100 variations per year    |  Yes<br>Add 100 catalog variations per year license pack |
| Products in a single catalog source | SKUs supported in the catalog | 250K SKUs      | Yes<br>Add 10K SKU license packs |
| Variants per product       | Number of product variants (size, color combinations) allowed per product | 10K  | No |
| Catalog sources            | Number of catalog data contexts (for example, locales or data sources like PIMs and ERPs) | 50  | No |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>If your Adobe Commerce Optimizer implementation exceeds the licensed quantities for Catalog Ingestion Rate, Catalog Variations, or SKU Count, at any time, you must license additional quantities sufficient to cover its excess usage.

### Price books

| **Capability**             | **Description**                                      | **Limit** | **Expandable?** |
| -------------------------- | ---------------------------------------------------- | --------- | --------------- |
| Price books | Number of price books allowed per instance           | 1,000     | No       |
| Discounts per price record | Number of discounts that can be applied to a product price within a single price book | 10        | No              |

{style="table-layout:auto"}

### Product Visuals powered by AEM Assets

| **Capability**            | **Description**                                             | **Limit**            | **Expandable?** |
| ------------------------- | ----------------------------------------------------------- | -------------------- | --------------- |
| Product Visuals Power users | Licensed user with full digital asset management capabilities, including AI tools, Adobe Express/Firefly integrations, and Content Hub sharing, handling core DAM tasks and advanced cloud-native features for optimal efficiency. | 2 | Yes<br>Upgrade to AEM Assets license |
| Product Visuals Collaborator users | Access and work with assets through the AEM Commerce integration, create and edit content using Adobe Express and Firefly, and—if enabled—leverage approved assets via the Content Hub portal. | 2 | Yes<br>Upgrade to AEM Assets license |
| Product Visuals storage | Allocated storage space for assets | 1 TB storage | No |
| Dynamic Media operations  | Allowance for dynamic media processing operations   | 5M operations/month  | Yes<br>Purchase license for additional operations|
| Video delivery | Allowance for video delivery. A single delivery or download of a video or transformed variant of a video consumes 20 Dynamic Media Operations.  | 300 videos/minute | No |
| Adobe Express | Access to Adobe Express generative AI for creating images | Power and Collaborator users | No |

{style="table-layout:auto"}

>[!NOTE]
>
>**Power Users** can access Adobe Express directly or within Adobe Commerce Optimizer. **Collaborator Users** can access the Adobe Express application directly. Usage is governed by the [Adobe Express with Firefly Product Specific Licensing Terms](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


### Catalog views and policies

| **Capability**            | **Description**                               | **Limit**      | **Expandable?**   |
|---------------------------|---------------------------------------------------|----------------|---------------|
| Catalog views | Number of configurable subsets of your master catalog | 30K per instance     | No |
| Policies per catalog view  | Number of data filters allowed  | 10  | No            |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100  | No |

{style="table-layout:auto"}

### Catalog storefront

| **Capability**            | **Description**                               | **Limit**      | **Expandable?**   |
|---------------------------|---------------------------------------------------|----------------|---------------|
| Catalog retrieval rate    | Number of times a catalog API is called per month by a system (for example, commerce backend, storefront, or other service) to retrieve data from the catalog | 10M/month          | Yes<br>Add 1M requests per month license packs |
| Content requests  | Requests to Commerce Storefront for HTML page views or JSON API calls. Counted as 1 page view or 5 API calls. | 2M/month          | Yes<br>Add 1M per month license pack |
| GenAI variations          | Allowance for text-based content generation in any environment | 1K variations/month  | Yes |

{style="table-layout:auto"}

>[!NOTE]
>
>Image generation requires an Adobe Firefly license provisioned to the same IMS org as Adobe Commerce Optimizer.


### Product discovery

| **Capability**  | **Description**       | **Limit**       | **Expandable?**  | **Notes**           |
|-----------------|-----------------------|------------------|------------|--------------------------|
| Products per search request | Maximum number of products returned per page in search results  | 100  | No         |                                      |
| Filterable attributes | Number of product characteristics (like color, size, brand, or material) that can be enabled for layered navigation and facets | 200 |      No |                                 |
| Searchable attributes | Number of product characteristics that can be configured for use with the product catalog search service | 200  | No            |                                        |
| Sortable attributes | Number of product characteristics that can be configured for determining the order of search result values | 50 |  No |   |
| Search pagination depth | Maximum number of products accessible through pagination (for example, page 100 × 100 products/page) | 10K |  No    |     |
| Facets | Number of filterable product attributes (like Brand, Color, Size, Price) that can be configured to help shoppers refine search results and browse categories | 100 | No | Must be filterable attributes          |
| Options per facet | The number of filterable product attribute values (like "Red," "Blue" for Color; "Small," "Medium" for Size) that shoppers can select from a list | 100              | Yes | Can increase via support request       |

{style="table-layout:auto"}


### Recommendations

The following capabilities are available for product recommendations. Some features available in other Adobe Commerce products are not supported in [!DNL Adobe Commerce Optimizer].

| **Capability** | **Description** | **Limit**    | **Expandable?** | **Notes**                         |
|----------------|-----------------|--------------|-----------------|-----------------------------------|
| Active recommendation units | Number of live recommendation components on your storefront (like "Customers also viewed" or "You might also like") | 50 | No  |   |
| Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | |  | Not supported |
| Preview recommendations | Preview how recommendations appear on the storefront before publishing | | | Not supported |

{style="table-layout:auto"}

### Extensibility

| **Capability**  | **Description**     | **Limit** |  **Expandable?** |   **Notes**      |
| ---------------- | ------------------ | --------- | ------------ | ------------- |
| Adobe Developer App Builder | Capacity for building cloud-native extensions and integrations | 1 pack/year | Yes<br>Add additional packs | See the [App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html) for limits defined per pack. |
| Adobe I/O Runtime | Capacity of the underlying serverless runtime (I/O Runtime) and eventing (I/O Events) services to support App Builder | | | See [System Settings](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) in the *App Builder Runtime Guides*.|

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
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
