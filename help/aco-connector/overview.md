---
title: Adobe Commerce Optimizer Connector
description: Learn how to connect your data from your Commerce cloud or on-premises project to Adobe Commerce Optimizer
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Adobe Commerce Optimizer Connector

The Adobe Commerce Optimizer Connector is a native, first-party integration between Adobe Commerce (cloud or on-premises) and Adobe Commerce Optimizer. It synchronizes catalog and pricing data from your Adobe Commerce stores into Commerce Optimizer so you can:

- Power **AI-driven product discovery and recommendations**
- Run **high-performance headless storefronts** (including Commerce storefronts powered by Edge Delivery)
- Analyze **before and after** KPIs and data-sync health in a single place

Commerce remains your system of record for products, prices, and catalog structure. Commerce Optimizer becomes your experience and merchandising layer, serving fast, relevant results to any connected storefront or channel.

## Key benefits {#key-benefits}

| Benefit | What it means for you |
| --- | --- |
| **No custom connector to build** | Use a supported, first-party integration instead of writing and maintaining bespoke feeds and scripts. |
| **Faster time to value with Commerce Optimizer** | Turn on AI search, recommendations, and headless storefronts on top of your existing Adobe Commerce deployment. |
| **Aligned with Commerce scopes** | Automatically maps Websites, Store Views, and customer groups into Commerce Optimizer catalog constructs (Catalog Sources and Price Books). |
| **Operational visibility** | Monitor feed health, last sync times, and per-SKU status from a dedicated Data Feed Sync Status view. |
| **Future-ready path toward SaaS** | Provides a low-risk modernization path from PaaS towards Adobe Commerce as a Cloud Service + Optimizer, without a re-platform. |

## Connector architecture {#connector-architecture}

The following diagram illustrates the end-to-end architecture for the connector, from Adobe Commerce through Commerce Optimizer and out to storefronts and checkout systems.

![Adobe Commerce Optimizer Connector end-to-end architecture diagram](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

In this architecture:

- Adobe Commerce (on cloud or on-premises) is the system of record and feed producer
- The Connector exports catalog, price, and category feeds
- Commerce Optimizer ingests and normalizes the feed data into Catalog Sources, Price Books, and Catalog Views
- Storefronts (Commerce storefront on Edge Delivery or custom headless builds) call Commerce Optimizer GraphQL APIs for discovery and recommendations and call Commerce or another connected third-party platform for cart and checkout operations

## How the connector works with Adobe Commerce

The Adobe Commerce Optimizer Connector operates by using your existing Commerce scopes (websites and store views) and customer segmentation to populate the Commerce Optimizer catalog model:

![Mapping Commerce data to Adobe Commerce Optimizer](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Store Views → Catalog Sources** — Each store view becomes a separate Catalog Source in Commerce Optimizer. That source includes localized product attributes and any store-view-specific data
- **Websites → Price Books** — Each Commerce website maps to one or more Price Books in Commerce Optimizer. Website pricing and customer group pricing export as price books and price entries
- **Customer groups → Price variants** — Commerce customer group pricing appears as additional entries in the relevant Price Books

After Commerce Optimizer ingests the data, you can configure:

- **Catalog Views and Policies** in Commerce Optimizer (for building region, brand, or customer-specific subsets)
- **Product Discovery** (search, facets, merchandising rules)
- **Product Recommendations**

When you enable the connector, the Adobe Commerce instance remains the system of record for catalog and price data. When you update data in Commerce, the connector syncs those updates to the [!DNL Adobe Commerce Optimizer] instance.

>[!NOTE]
>
>For details on configuring Commerce Optimizer, see [[!DNL Adobe Commerce Optimizer] Merchandising tools](../optimizer/overview.md#quick-tour).

## Typical workflows {#typical-workflows}

These workflows describe how teams set up and use the Adobe Commerce Optimizer Connector. For details on how to set up the integration and enable these workflows, see [Get Started](get-started.md).

### Initial setup and configuration {#initial-setup}


The high level steps for setup and configuration:

1. Install the connector package for Adobe Commerce.

1. Configure authentication and environment details.

1. Map Commerce scopes to Commerce Optimizer.

1. Verify connectivity.

For detailed instructions, see [Configuration steps](./get-started.md#configuration-steps) in the _Get Started_ guide.

### Ongoing data synchronization {#ongoing-sync}

After the initial configuration, the connector supports:

- **Full catalog sync** for initial migration or large structural changes
- **Delta syncs** for ongoing updates when products or prices change
- **Resync commands** for targeted feeds

The following feeds are available for the Adobe Commerce Optimizer Connector:

- `products` - products data
- `productAttributes` - metadata for product attributes
- `priceBooks` - price books
- `prices` - product prices
- `categories` - categories data

For additional details, see the following topics:

- Commerce command line interface (CLI) for resync operations, see the [CLI resync command](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="blank"}
- [Feed endpoints and configuration](reference/connector-reference.md)
- [Field mappings for connector feeds](reference/field-mapping.md)

### Configure merchandising and storefronts {#merchandising-storefronts}

Once Commerce data is available in Commerce Optimizer, use [Commerce Optimizer Studio](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour) to connect merchandising and storefront experiences to your synced catalog.

**To configure merchandising and storefronts in Commerce Optimizer Studio:**

1. **Create Catalog Views and Policies** from the [!UICONTROL Store setup] menu.

    - Filter the catalog by brand, region, customer segment, or channel
    - Enforce data-access rules per storefront or partner

1. **Configure Product Discovery and Recommendations** from the [!UICONTROL Merchandising] menu.

    - Create merchandising rules, facets, synonyms, and recommendation units
    - The connector offloads all search and recommendation configuration to Commerce Optimizer (Live Search rules and Product Recommendations in Commerce Admin no longer apply to these flows)

1. **Connect storefronts** to Commerce Optimizer:

    - For a Commerce Storefront powered by Edge Delivery Services, configure the storefront to use the correct Optimizer tenant and Catalog View, and to call search and recommendation endpoints through the Merchandising API
    - For third-party storefronts, use Optimizer public APIs or SDKs for search and recommendation calls

    >[!NOTE]
    >
    >For an example third-party integration, see the [Salesforce Commerce Connector for Commerce Optimizer](../optimizer/developer/salesforce-connector.md).

1. **Maintain checkout** on your existing platform:

    - Keep cart, checkout, order management, and customer accounts in Adobe Commerce or a third-party platform
    - Use App Builder and API Mesh for cart handoff when you integrate with external checkout systems

## Supported scenarios {#supported-scenarios}

The connector is designed for B2C merchants with Adobe Commerce on cloud and on-premises deployments who want to adopt Commerce Optimizer without rebuilding their backend.

**Common use cases:**

- **Modernizing the storefront only**
  Keep your existing Commerce backend, move PLP/Search/PDP to Edge Delivery storefronts powered by Commerce Optimizer

- **Scaling catalog and search performance**
  Offload heavy catalog indexing and search to Commerce Optimizer's SaaS services while maintaining product and price ownership in Commerce

- **Incremental SaaS adoption**
  Use the connector as a stepping stone toward Adobe Commerce as a Cloud Service + Optimizer, with a compatible composable Commerce catalog

## Responsibilities and implementation prerequisites {#responsibilities-prerequisites}

Commerce is the source of truth for products, pricing, and customer groups. Make changes in Commerce; the connector syncs them to Commerce Optimizer.

**Commerce Optimizer is responsible for:**

- Catalog modeling (Catalog Sources, Price Books, Catalog Views, Policies)
- Product discovery and recommendations
- Storefront metrics, data-sync dashboards, and Success Metrics reports

**The connector does not:**

- Modify Commerce cart, checkout, or order flows
- Automatically provision storefront projects (Commerce Storefront / Edge Delivery tooling handles that)

**Before you begin:**

- Verify that Commerce meets the minimum version and services connector requirements. See [Get Started](get-started.md#prerequisites) for details.
- Ensure that you have IMS org access, an [!DNL Adobe Commerce Optimizer] instance, and the necessary credentials and region details.

## Related documentation {#related-documentation}

- Set up the integration and enable key workflows: [Get Started with the Adobe Commerce Optimizer Connector](get-started.md)
- Learn about Commerce Optimizer concepts and architecture: [What is Adobe Commerce Optimizer?](../optimizer/overview.md)
- Understand the sync mechanism, initialization, and error handling: [Data synchronization](data-synchronization.md)
- Field-level data mapping for all feeds: [Field Mappings](reference/field-mapping.md)
- Integrate headless storefronts using GraphQL and bundle encoding: [Headless Storefront Integration](headless-storefront.md)
- Diagnose sync and configuration issues: [Troubleshooting](troubleshooting.md)
