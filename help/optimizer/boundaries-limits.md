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

Follow these best practices to stay within limits and avoid operational issues:

- **Review your limits**—Understand your [capacity limits](#adobe-commerce-optimizer-limits) before launching new storefronts or campaigns.
- **Track your usage**—Use built-in metrics dashboards or CDN logs.

## License limits and system boundaries

The following tables summarize the license limits and system boundaries by capability area and includes information about adding additional licenses to expand capacity where applicable.

>[!NOTE]
>
> For information about packages available for increasing capacity, see the [Adobe Commerce Optimizer product licensing description](https://helpx.adobe.com/legal/product-descriptions/adobe-commerce-optimizer.html).

### Environment limits

| **Environment**              | **Description**                            | **Base allocation**      | **Expandable?** |
| ---------------------------- | -------------------------------------------| ---------------| ----------------|
| **Sandbox environment**      | Number of sandbox environments included    | 2 per instance | Yes<br>Add additional environment license per instance |
| **Production environment**   | Number of production environments included | 1 per instance | License<br>Add additional environment license per instance |

{style="table-layout:auto"}

### Catalog

| **Capability**            | **Description**                               | **Base allocation**      | **Expandable?**  | **Max limit** |
|---------------------------|---------------------------------------------------|----------------|---------------- | ------ |
| Product ingestion rate    | Number of products created or updated | 1K updates per minute: total 100K updates per day | Yes<br>Add 5K update per minute (500K) pack or, <br>10K updates per minute (1M updates per day) | 10K updates per minute: total 1M updates per day |
| Product payload size | Maximum amount of data allowed when creating, updating, or ingesting product information using the API | 200 KB | No |
| Catalog Variations                  | Number of views of a catalog that are available to storefront users,<br>which are counted as (*Number of Catalog Views × Number of Price Books*) | 100 variations  |  Yes<br>Add 100 catalog variations license pack | |
| Products in a single catalog source | SKUs supported in the catalog | 250K SKUs      | Yes<br>Add 10K SKU license packs | |
| Variants per product       | Number of product variants (size, color combinations) allowed per product | 10K  | No | |
| Catalog sources            | Number of catalog data contexts (for example, locales or data sources like PIMs and ERPs) | 50  | No | |

{style="table-layout:auto"}

### Price books

| **Capability**             | **Description**                                      | **Base allocation** | **Expandable?** | **Max limit** |
| -------------------------- | ---------------------------------------------------- | --------- | --------------- | ------ |
| Price books | Number of price books allowed per instance           | 1,000     | No       | |
| Discounts per price record | Number of discounts that can be applied to a product price within a single price book | 10  | No
No | |

{style="table-layout:auto"}

### Product Visuals powered by AEM Assets

| **Capability**            | **Description**                                             | **Base allocation**            | **Expandable?** | **Max limit** |
| ------------------------- | ----------------------------------------------------------- | -------------------- | --------------- |
| Product Visuals Power users | Licensed user with full digital asset management capabilities, including AI tools, Adobe Express/Firefly integrations, and Content Hub sharing, handling core DAM tasks and advanced cloud-native features for optimal efficiency. | 2 | Yes<br>Upgrade to AEM Assets license |
| Product Visuals Collaborator users | Access and work with assets through the AEM Commerce integration, create and edit content using Adobe Express and Firefly, and—if enabled—leverage approved assets via the Content Hub portal. | 2 | Yes<br>Upgrade to AEM Assets license |
| Product Visuals storage | Allocated storage space for assets | 1 TB storage | No |
| Dynamic Media operations  | Allowance for dynamic media processing operations   | Determined by GMV<br>minimum allocation of 5M operations/month  | Yes<br>Purchase license for additional operations|
| Video delivery | A single delivery or download of a video or transformed variant of a video consumes 20 Dynamic Media Operations.  | Up to 300 videos, a maximum of 1 minute per video| Yes<br>Upgrade to AEM Assets license |
| Adobe Express | Access to Adobe Express generative AI for creating images | Power and Collaborator users | No |

{style="table-layout:auto"}

>[!NOTE]
>
>**Power Users** can access Adobe Express directly or within Adobe Commerce Optimizer. **Collaborator Users** can access the Adobe Express application directly. Usage is governed by the [Adobe Express with Firefly Product Specific Licensing Terms](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


### Catalog views and policies

| **Capability**            | **Description**                               | **Base allocation**      | **Expandable?**   | **Max limit** |
|---------------------------|---------------------------------------------------|----------------|---------------| ---- |
| Catalog views | Number of configurable subsets of your master catalog | 30K per instance     | No | |
| Policies per catalog view  | Number of data filters allowed  | 10  | No            | |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100  | No | |

{style="table-layout:auto"}

### Catalog storefront

The base allocation for catalog storefront capabilities is determined based on GMV tier. The table indicates the minimum allocation for each capability.

| **Capability**            | **Description**                               | **Base allocation**      | **Expandable?**   | **Max limit** |
|---------------------------|---------------------------------------------------|----------------|---------------|------|
| Catalog retrieval rate    | Number of times a catalog API is called per month by a system (for example, commerce backend, storefront, or other service) to retrieve data from the catalog | 10M/month minimum         | Yes<br>Add 1M requests per month license packs | |
| Content requests  | Requests to Commerce Storefront for HTML page views or JSON API calls. Counted as 1 page view or 5 API calls. <br>2M/month minimum         | Yes<br>Add 1M per month license pack | |
| GenAI variations          | Allowance for text-based content generation in any environment | 1K variations/month minimum | Yes | |

{style="table-layout:auto"}

>[!NOTE]
>
>Image generation requires an Adobe Firefly license provisioned to the same IMS org as Adobe Commerce Optimizer.


### Product discovery

| **Capability**  | **Description**       | **Base allocation**       | **Expandable?**  | **Max limit**           |
|-----------------|-----------------------|------------------|------------|--------------------------|
| Products per search request | Maximum number of products returned per page in search results  | 100  | No         |                                      |
| Filterable attributes | Number of product characteristics (like color, size, brand, or material) that can be enabled for layered navigation and facets | 200 |      No |                                 |
| Searchable attributes | Number of product characteristics that can be configured for use with the product catalog search service | 200  | No            |                                        |
| Sortable attributes | Number of product characteristics that can be configured for determining the order of search result values | 50 |  No |   |
| Search pagination depth | Maximum number of products accessible through pagination (for example, page 100 × 100 products/page) | 10K |  No    |     |
| Facets | Number of filterable product attributes (like Brand, Color, Size, Price) that can be configured to help shoppers refine search results and browse categories | 100<br>Must be filterable attributes | No | |
| Options per facet | The number of filterable product attribute values (like "Red," "Blue" for Color; "Small," "Medium" for Size) that shoppers can select from a list | 100              | Yes<br>Can increase via support request | |

{style="table-layout:auto"}


### Recommendations

The following capabilities are available for product recommendations. Some features available in other Adobe Commerce products are not supported in [!DNL Adobe Commerce Optimizer].

| **Capability** | **Description** | **Base allocation**    | **Expandable?** | **Max limit**                         |
|----------------|-----------------|--------------|-----------------|-----------------------------------|
| Active recommendation units | Number of live recommendation components on your storefront (like "Customers also viewed" or "You might also like") | 50 | No  |   |
| Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported |  | |
| Preview recommendations | Preview how recommendations appear on the storefront before publishing | Not supported | | |

{style="table-layout:auto"}

### Extensibility

| **Capability**  | **Description**     | **Base allocation** |  **Expandable?** |   **Notes**      |
| ---------------- | ------------------ | --------- | ------------ | ------------- |
| Adobe Developer App Builder | Capacity for building cloud-native extensions and integrations | Determined by GMV tier<br>Minimum allocation: 1 pack/year | Yes<br>Add additional packs | For limits defined per pack, see:<ul><li>[App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html) for limits defined per pack.</li><li>[System Settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) in the *App Builder Runtime Guides*.</li></ul> |
| Adobe I/O Runtime | Capacity of the underlying serverless runtime (I/O Runtime) and eventing (I/O Events) services to support App Builder | | | See [System Settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) in the *App Builder Runtime Guides*.|

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
