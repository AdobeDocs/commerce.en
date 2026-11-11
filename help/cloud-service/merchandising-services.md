---
title: Composable Catalog Data Model and Merchandising Services
description: Learn how the Composable Catalog Data Model changes catalog delivery in [!DNL Adobe Commerce as a Cloud Service] and what merchants and storefront teams need to know.
feature: Catalog Management, Personalization, Saas
role: Leader
level: Beginner
autotag-review: '2026-11-09T05:07:21.124Z'
TQID: 'https://experienceleague.adobe.com/5Aaumfx9-lOBMDOg59rr-MMl-0sgFLSVUzngkdzfyR0'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---

# Merchandising Services

Adobe Commerce as a Cloud Service now supports the composable catalog data model (CCDM) through Merchandising Services. Adobe Commerce Optimizer introduced this data model, and CCDM gives both products a common foundation for serving storefront catalog browsing and merchandising capabilities, while the Commerce Foundation continues to manage products, prices, and transactions.

This topic explains what changes with CCDM, which features continue, and what the change means for merchants, partners, and storefront developers.

## What changes does CCDM introduce?

The original catalog model uses Catalog Service to deliver product data to storefronts, with Live Search and Product Recommendations providing search, merchandising, and recommendation capabilities. In this model, Commerce synchronizes using [SaaS data export](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview).

With CCDM, these capabilities operate on the same catalog foundation that powers Adobe Commerce Optimizer. [Catalog views](../optimizer/setup/catalog-view.md) and [policies](../optimizer/setup/policies.md) define the catalog context available to a storefront. Policies determine the product assortment, and merchandising rules can apply across all catalog views or be tailored to a specific view.

This changes how the catalog is configured, accessed, and merchandised. CCDM builds on the original Commerce catalog's search, recommendations, and merchandising capabilities while introducing controls at the catalog view-level. Additional management and reporting capabilities are described below.

Commerce Foundation remains the canonical source for products and prices. Product and price data synchronize one way to CCDM through a native Adobe Commerce as a Cloud Service integration. Website, store, and store-view configuration remains in Commerce, alongside the existing cart, checkout, and order-management workflows.

## Licensing and provisioning

Merchandising Services is included in the existing Adobe Commerce as a Cloud Service SKU. It is not a second product or subscription, and it does not require a separate Adobe Commerce Optimizer purchase, entitlement, or tenant.

## Architecture overview

The [!DNL Commerce Foundation] remains the primary record for products and prices and continues to manage transactions. The native integration synchronizes product and price data one way from [!DNL Commerce] to CCDM. You do not install a separate connector or an [!DNL App Builder] app for this synchronization.

Storefronts use CCDM-backed Merchandising Services to retrieve catalog data and context for browsing, search, recommendations, and merchandising. Requests use the catalog context to retrieve products and prices for the intended audience. You continue to manage website, store, and store-view configuration in [!DNL Commerce].

The following diagram shows the position of Merchandising Services in the broader Adobe Commerce as a Cloud Service architecture.

![Commerce architecture showing the catalog data flow into Merchandising Services](./assets/data-flow-ccdm.png){zoomable="yes"}

## What's new for merchants?

The new model lets you scope existing merchandising rules to all catalog views or to a specific view. This lets you apply merchandising to each storefront audience. Learn how to [scope a merchandising rule to catalog views](../optimizer/merchandising/rules/add.md#create-a-rule).

In the Admin, you can configure catalog context with [!UICONTROL Catalog Views] and [!UICONTROL Policies]. You can also use [!UICONTROL Success Metrics] to review revenue, conversion, engagement, acquisition, and bounce rate. See [Success Metrics](../optimizer/manage-results/success-metrics.md) for details.

## Considerations before adoption

Review how the CCDM model affects your licensing, catalog integrations, storefront, and Admin workflows before adopting Merchandising Services.

### Catalog management and integrations

Continue managing products and prices in [!DNL Commerce Foundation]. The native integration synchronizes them to CCDM. Do not create a second product catalog for Merchandising Services.

### Storefront implementation

How your storefront retrieves catalog data depends on your implementation:

- **[!DNL Adobe Commerce Storefront]** drop-ins—The drop-ins handle the transition. No code changes are required. See the [storefront setup documentation](https://experienceleague.adobe.com/en/tools/commerce-storefront/).
- **Custom or other storefronts**—Update your catalog request headers as described in the [header configuration reference](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

Review your catalog queries and request headers for the CCDM-based model. Do not assume that existing queries or headers remain unchanged. The Merchandising GraphQL queries differ from queries used in the original catalog-services model. Additional queries support CCDM. Use the [Merchandising GraphQL API reference](https://developer.adobe.com/commerce/services/reference/graphql/) and verify the required catalog context against the [storefront header reference](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

### Third-party apps and extensions

Review third-party apps and extensions that read catalog data or consume catalog events with their provider. Compatibility depends on how each app or extension uses those interfaces.

### Admin experience

Adobe Commerce as a Cloud Service with CCDM uses [[!DNL Adobe Unified Experience]](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/admin-unified-experience) (Unified Shell). Adobe released Unified Shell separately from CCDM. Existing instances on the original catalog-services model retain access to both Classic and Unified Shell.

### Limits

The CCDM model does not change Adobe Commerce as a Cloud Service limits. Sharing a catalog foundation with Optimizer does not mean that Commerce inherits Optimizer capacity or limits.

## Availability and migration

Organizations that start with Adobe Commerce as a Cloud Service after this release receive Merchandising Services by default. If your organization requires the original catalog data model, contact your Adobe account team to discuss whether an exception is available.

Organizations that had Adobe Commerce as a Cloud Service before this release can choose either catalog model when [provisioning a new instance](./getting-started.md#create-an-instance). By default, the [!UICONTROL Enable CCDM] switcher is disabled. Once CCDM is enabled, you cannot disable it.

Existing instances do not change automatically. At general availability (GA), you cannot migrate an existing original catalog-services instance to Merchandising Services.
