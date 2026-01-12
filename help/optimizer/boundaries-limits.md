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

## Request additional capacity

License limits can be increased by purchasing the license packages described in the [License limits and system boundaries](#license-limits-and-system-boundaries) section, or by negotiating custom licensing for unique use cases. Contact your Adobe Account representative to discuss your requirements.

For questions about system boundaries, contact [Adobe Support](https://experienceleague.adobe.com/home?lang=en#support).

## Prevent performance issues

Follow these best practices to stay within limits and avoid operational issues:

- **Review your limits**—Understand your [capacity limits](#license-limits-and-system-boundaries) before launching new storefronts or campaigns.
- **Track your usage**—Use built-in metrics dashboards or CDN logs.

## License limits and system boundaries

The following tables summarize the license limits and system boundaries by capability area and includes information about adding additional licenses to expand capacity where applicable.

### Environment limits

| **Environment** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| **Sandbox environment** | The number of sandbox environments included | 2 per instance | Yes<p>Add an additional environment license per instance</p> |
| **Production environment** | The number of production environments included | 1 per instance | License<p>Add an additional environment license per instance</p> |

{style="table-layout:auto"}

### Catalog

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Product ingestion rate | The number of products created or updated | 1K updates per minute<p>A maximum of 100K updates per day</p> | Yes<p>Add one license pack:</p><ul><li>5K updates per minute<br>Maximum of 500K updates per day</li> <li>10K updates per minute<br>Maximum of 1M updates per day</li></ul><p>The maximum capacity for data ingestion is 1M updates per day.</p> |
| Product payload size | Maximum amount of data allowed when creating, updating, or ingesting product information using the API | 200 KB | No |
| Catalog variations | The number of views of a catalog that are available to storefront users,<p>which are counted as (*Number of Catalog Views × Number of Price Books*)</p> | 100 variations | Yes<p>Add 100 catalog variations license pack</p> |
| Products in a single catalog source | SKUs supported in the catalog | 250K SKUs | Yes<p>Add 100K SKU license pack</p> |
| Variants per product | The number of product variants (size, color combinations) allowed per product | 10K | No |
| Catalog sources | The number of catalog data contexts (for example, locales or data sources like PIMs and ERPs) | 50 | No |

{style="table-layout:auto"}

### Price books

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}

### Product Visuals powered by AEM Assets

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Product Visuals Power users | Licensed user with full digital asset management capabilities, including AI tools, Adobe Express/Firefly integrations, and Content Hub sharing, handling core DAM tasks and advanced cloud-native features for optimal efficiency. | 2 | Yes<p>Upgrade to AEM Assets license</p> |
| Product Visuals Collaborator users | Access and work with assets through the AEM Commerce integration, create and edit content using Adobe Express and Firefly, and—if enabled—leverage approved assets via the Content Hub portal. | 2 | Yes<p>Upgrade to AEM Assets license</p> |
| Product Visuals storage | Allocated storage space for assets | 1 TB storage | No |
| Dynamic Media usage | Allowance for dynamic media processing operations which includes:<ul><li>Image delivery</li><li>Smart Imaging</li><li>Video Delivery</li></ul><p>For details, see *Calculate Dynamic Media usage* below. | Based on GMV<p>Minimum allocation: 5M operations/month</p> | Yes<ul><li>Purchase license for additional operations</li><li>Upgrade to AEM Assets license</li></ul> |
| Video delivery | Allowance for video delivery or downloads | 300 videos, 1 minute per video | Yes<p>Upgrade to AEM Assets license</p> |
| Asset generation | Access to Adobe Express and Adobe Firefly generative AI for creating images | None | Purchase Generative AI credits separately |

{style="table-layout:auto"}


>[!NOTE]
>
>**Power Users** can access Adobe Express directly or within Adobe Commerce Optimizer. **Collaborator Users** can access the Adobe Express application directly. Usage is governed by the [Adobe Express with Firefly Product Specific Licensing Terms](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


>[!BEGINSHADEBOX "Calculate Dynamic Media usage"]

Dynamic Media usage tracks API requests coming into the Product Visuals components within Adobe Commerce Optimizer to facilitate one of the following actions:

- **Image delivery consumes one dynamic media operation** for each occurrence of the following:
   - **basic image transformation** of a digital asset, for example resize, scale, format conversion, compression, or crop operations.
   - **static image delivery or download** of said digital assets or digital asset rendition (other than video)
- **Smart Image delivery consumes 20 Dynamic Media Operations** for each optimized delivery of a single digital asset by automatically generating the most appropriate image rendition for an end user's device and browser.
- **Video delivery consumes 20 Dynamic Media Operations** for a single delivery or download of a video, or a transformed variant of a video.

>[!ENDSHADEBOX]


### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |

{style="table-layout:auto"}

### Catalog storefront

The base allocation for catalog storefront capabilities is determined based on GMV tier. The table indicates the minimum allocation for each capability.

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog retrieval rate | Number of times a catalog API is called per month by a system (storefront, transaction system, ERP, or other) to retrieve data from the catalog | Based on GMV tier<p>Minimum allocation: 10M/month</p> | Yes<p>Add 1M requests per month license packs</p> |
| Content requests | Requests to Commerce Storefront for HTML page views or JSON API calls. Counted as 1 page view or 5 API calls. | Based on GMV tier<p>Minimum allocation: 2M/month</p> | Yes<p>Add 1M per month license pack</p> |
| Storefront GenAI variations | Allowance for text-based content generation | Based on GMV tier<p>Minimum allocation: 1K variations/month</p> | Yes<p>Purchase Generative AI credits separately</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>Image generation requires an Adobe Firefly license provisioned to the same IMS org as Adobe Commerce Optimizer.


### Product discovery

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Products per search request | Maximum number of products returned per page in search results | 100 | No |
| Filterable attributes | The number of product characteristics (like color, size, brand, or material) that can be enabled for layered navigation and facets | 200 | No |
| Searchable attributes | The number of product characteristics that can be configured for use with the product catalog search service | 200 | No |
| Sortable attributes | The number of product characteristics that can be configured for determining the order of search result values | 50 | No |
| Search pagination depth | Maximum number of products accessible through pagination (for example, page 100 × 100 products/page) | 10K | No |
| Facets | Number of filterable product attributes (like Brand, Color, Size, Price) that can be configured to help shoppers refine search results and browse categories | 100<p>Must be filterable attributes</p> | No |
| Options per facet | The number of filterable product attribute values (like "Red," "Blue" for Color; "Small," "Medium" for Size) that shoppers can select from a list | 100 | Yes<p>Can increase via support request</p> |

{style="table-layout:auto"}

### Recommendations

The following capabilities are available for product recommendations. Some features available in other Adobe Commerce products are not supported in [!DNL Adobe Commerce Optimizer].

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Active recommendation units | Number of live recommendation components on your storefront (like "Customers also viewed" or "You might also like") | 50 | No |
| Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | |
| Preview recommendations | Preview how recommendations appear on the storefront before publishing | Not supported | |

{style="table-layout:auto"}

### Extensibility

| **Capability** | **Description** | **Base allocation** | **Expandable?** | **Notes** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacity for building cloud-native extensions and integrations | Based on GMV tier<p>Minimum allocation: 1 pack/year</p> | Yes<p>Add additional packs</p> | For limits defined per pack, see:<ul><li>[App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html) for limits defined per pack.</li><li>[System Settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) in the *App Builder Runtime Guides*.</li><li>[App Builder Storage requirements]( https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/#)</li></ul> |

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
