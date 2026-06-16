---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: "Learn about the [!DNL Adobe Commerce Optimizer Connector] for catalog sync, search, and storefront delivery between [!DNL Adobe Commerce] and [!DNL Adobe Commerce Optimizer]."
feature: Integration, Storefront, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T19:00:00.000Z'
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# [!DNL Adobe Commerce Optimizer Connector]

The [!DNL Adobe Commerce Optimizer Connector] is a native, first-party integration between [!DNL Adobe Commerce] (cloud or on-premises) and [!DNL Adobe Commerce Optimizer]. It synchronizes catalog and pricing data from your [!DNL Adobe Commerce] stores into [!DNL Adobe Commerce Optimizer] so you can:

- Power **AI-driven product discovery and recommendations**
- Run **high-performance headless storefronts** (including Commerce storefronts powered by [!DNL Edge Delivery Services])
- Analyze **before and after** KPIs and data-sync health in a single place

[!DNL Adobe Commerce] remains your system of record for products, prices, and catalog structure. [!DNL Adobe Commerce Optimizer] becomes your experience and merchandising layer, serving fast, relevant results to any connected storefront or channel.

## Key benefits {#key-benefits}

| Benefit | What it means for you |
| --- | --- |
| **No custom connector to build** | Use a supported, first-party integration instead of writing and maintaining bespoke feeds and scripts. |
| **Faster time to value with [!DNL Adobe Commerce Optimizer]** | Turn on AI search, recommendations, and headless storefronts on top of your existing [!DNL Adobe Commerce] deployment. |
| **Aligned with Commerce scopes** | Automatically maps websites, store views, and customer groups into [!DNL Adobe Commerce Optimizer] catalog constructs (Catalog Sources and Price Books). |
| **Operational visibility** | Monitor feed health, last sync times, and per-SKU status from a dedicated [!UICONTROL Data Feed Sync Status] view. |
| **Future-ready path toward SaaS** | Provides a phased migration path from Commerce on cloud or on-premises to [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], without re-platforming. |

## Connector architecture {#connector-architecture}

The following diagram illustrates the end-to-end architecture for the connector, from [!DNL Adobe Commerce] through [!DNL Adobe Commerce Optimizer] and out to storefronts and checkout systems.

![Adobe Commerce Optimizer Connector end-to-end architecture diagram](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

In this architecture:

- [!DNL Adobe Commerce] (on cloud or on-premises) is the system of record and feed producer
- The connector exports catalog, price, and category feeds
- [!DNL Adobe Commerce Optimizer] ingests and normalizes the feed data into Catalog Sources, Price Books, and Catalog Views
- Storefronts (Commerce storefront on [!DNL Edge Delivery Services] or custom headless builds) call [!DNL Adobe Commerce Optimizer] GraphQL APIs for discovery and recommendations and call [!DNL Adobe Commerce] or another connected third-party platform for cart and checkout operations

Built on [[!DNL SaaS Data Export]](/help/data-export/overview.md), the connector maps collected feeds to the [!DNL Catalog Data Ingestion API] format and handles authentication and submission. See [Connector sync pipeline](/help/aco-connector/connector-sync-pipeline.md) for synchronization behavior, scope control, and error handling.

## How the connector works with [!DNL Adobe Commerce] {#how-the-connector-works-with-adobe-commerce}

The [!DNL Adobe Commerce Optimizer Connector] operates by using your existing Commerce scopes (websites and store views) and customer segmentation to populate the [!DNL Adobe Commerce Optimizer] catalog model:

![Mapping Commerce data to Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Store view → Catalog Sources** — Each store view becomes a separate Catalog Source in [!DNL Adobe Commerce Optimizer]. That source includes localized product attributes and any store-view-specific data
- **Website → Price Books** — Each [!DNL Adobe Commerce] website maps to one or more Price Books in [!DNL Adobe Commerce Optimizer]. Website pricing and customer group pricing export as price books and price entries
- **Customer group → Price variants** — [!DNL Adobe Commerce] customer group pricing appears as additional entries in the relevant Price Books

After [!DNL Adobe Commerce Optimizer] ingests the data, you can configure:

- **Catalog Views and Policies** in [!DNL Adobe Commerce Optimizer] Studio (for building region, brand, or customer-specific subsets)
- **Product Discovery** (search, facets, merchandising rules)
- **[!DNL Product Recommendations]**

When you enable the connector, the [!DNL Adobe Commerce] instance remains the system of record for catalog and price data. When you update data in [!DNL Adobe Commerce], the connector syncs those updates to the [!DNL Adobe Commerce Optimizer] instance.

>[!NOTE]
>
>For details on configuring [!DNL Adobe Commerce Optimizer], see [[!DNL Adobe Commerce Optimizer] Merchandising tools](/help/optimizer/overview.md#quick-tour).

## Typical workflows {#typical-workflows}

These workflows describe how teams set up and use the [!DNL Adobe Commerce Optimizer Connector]. For details on how to set up the integration and enable these workflows, see [Get Started](/help/aco-connector/get-started.md).

### Initial setup and configuration {#initial-setup}

See [Configuration steps](/help/aco-connector/get-started.md#configuration-steps) in the _Get Started_ guide.

### Ongoing data synchronization {#ongoing-sync}

After the initial configuration, the connector supports:

- **Full catalog sync** for initial migration or large structural changes
- **Delta syncs** for ongoing updates when products or prices change
- **Resync commands** for targeted feeds

For automated sync behavior, cron schedules, and error handling, see [Connector sync pipeline](/help/aco-connector/connector-sync-pipeline.md). Before a full catalog sync or large update, use [Estimate data volume and sync time](/help/aco-connector/reference/estimate-data-volume-sync-time.md) to plan timing and avoid site disruption.

The following feeds are available for the [!DNL Adobe Commerce Optimizer Connector]:

- `products` - products data
- `productAttributes` - metadata for product attributes
- `priceBooks` - price books
- `prices` - product prices
- `categories` - categories data

For additional details, see the following topics:

- Verify catalog data sync and manually resync connector feeds: [Manage synchronization](/help/aco-connector/data-sync-manage.md)
- For [!DNL Adobe Commerce] CLI resync operations, see [Sync feeds using the Commerce CLI](/help/data-export/data-export-cli-commands.md)
- [[!DNL Adobe Commerce Optimizer Connector] modules and feed endpoints](/help/aco-connector/reference/connector-reference.md)
- [Field mapping for connector feeds](/help/aco-connector/reference/field-mapping.md)

### Configure merchandising and storefronts {#merchandising-storefronts}

Once [!DNL Adobe Commerce] data is available in [!DNL Adobe Commerce Optimizer], use [[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour) to connect merchandising and storefront experiences to your synced catalog. Typical next steps include:

- **Catalog views and policies** — Define region-, brand-, or customer-specific subsets and access rules from the [!UICONTROL Store setup] menu
- **Product discovery and recommendations** — Configure search, facets, merchandising rules, synonyms, and recommendation units in the [!UICONTROL Merchandising] menu. Search and recommendation behavior is managed in [!DNL Adobe Commerce Optimizer]; [!DNL Live Search] and [!DNL Product Recommendations] settings in the [!DNL Adobe Commerce] Admin no longer apply to these flows
- **Storefront connections** — Point Commerce storefronts on [!DNL Edge Delivery Services] or third-party headless builds at the correct [!DNL Adobe Commerce Optimizer] tenant, catalog view, and Merchandising API endpoints. For custom headless integrations, see [Headless storefront integration](/help/aco-connector/headless-storefront.md). For an example third-party integration, see the [Salesforce Commerce Connector for [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)
- **Checkout** — Keep cart, checkout, order management, and customer accounts on [!DNL Adobe Commerce] or a connected third-party platform. Use [!DNL App Builder] and [!DNL API Mesh] for cart handoff when needed

For step-by-step configuration guidance, see [Get Started](/help/aco-connector/get-started.md) and the [[!DNL Adobe Commerce Optimizer] Merchandising tools](/help/optimizer/overview.md#quick-tour).

## Supported scenarios {#supported-scenarios}

The connector is designed for B2C merchants with [!DNL Adobe Commerce] on cloud and on-premises deployments who want to adopt [!DNL Adobe Commerce Optimizer] without rebuilding their backend.

**Common use cases:**

- **Storefront migration to Edge Delivery**
  Keep your existing [!DNL Adobe Commerce] backend, move PLP/Search/PDP to [!DNL Edge Delivery Services] storefronts powered by [!DNL Adobe Commerce Optimizer]

- **Scaling catalog and search performance**
  Offload heavy catalog indexing and search to [!DNL Adobe Commerce Optimizer]'s SaaS services while maintaining product and price ownership in [!DNL Adobe Commerce]

- **Incremental SaaS adoption**
  Use the connector as a stepping stone toward [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], with a compatible composable [!DNL Adobe Commerce] catalog

## Responsibilities and implementation prerequisites {#responsibilities-prerequisites}

[!DNL Adobe Commerce] is the source of truth for products, pricing, and customer groups. Make changes in [!DNL Adobe Commerce], and the connector syncs them to [!DNL Adobe Commerce Optimizer].

**[!DNL Adobe Commerce Optimizer] is responsible for:**

- Catalog modeling (Catalog Sources, Price Books, Catalog Views, Policies)
- Product discovery and recommendations
- Storefront metrics, data-sync dashboards, and Success Metrics reports

**The connector does not:**

- Modify [!DNL Adobe Commerce] cart, checkout, or order flows
- Automatically provision storefront projects (Commerce Storefront / [!DNL Edge Delivery Services] tooling handles that)

**Before you begin:**

- Verify that [!DNL Adobe Commerce] meets the minimum version and [!DNL Adobe Commerce Optimizer Connector] requirements. See [Get Started](/help/aco-connector/get-started.md#requirements-to-use-the-integration) for details.
- Ensure that you have IMS org access, an [!DNL Adobe Commerce Optimizer] instance, and the necessary credentials and region details.

>[!MORELIKETHIS]
>
> - [Get Started with the [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md) — Set up the integration and enable key workflows.
> - [Connector sync pipeline](/help/aco-connector/connector-sync-pipeline.md) — Understand sync mechanism, initialization, and error handling.
> - [Manage synchronization](/help/aco-connector/data-sync-manage.md) — Verify catalog data sync and manually resync feeds.
> - [Field mapping for connector feeds](/help/aco-connector/reference/field-mapping.md) — Review field-level data mapping for all feeds.
> - [Troubleshooting scenarios](/help/aco-connector/troubleshooting/troubleshooting-scenarios.md) — Resolve misconfiguration or unexpected sync results.
> - [Release notes](/help/aco-connector/release-notes.md) — Review connector updates and known issues.
