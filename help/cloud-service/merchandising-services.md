---
title: Composable Catalog Data Model and Merchandising Services
description: Understand how Merchandising Services and the composable catalog data model change catalog delivery in [!DNL Adobe Commerce as a Cloud Service] for storefronts.
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

Merchandising Services provides catalog data to storefronts in [!DNL Adobe Commerce as a Cloud Service]. It uses the composable catalog data model (CCDM) to separate product data from the context that determines which products and prices a storefront can retrieve.

## What the model replaces

The traditional Adobe Commerce catalog model uses websites, stores, and store views to organize and scope catalog data. CCDM replaces that hierarchy as the model for composing storefront catalogs. It does not replace [!DNL Commerce Foundation] or its transaction flows, such as cart, checkout, and order management.

CCDM separates:

- **Product data**, such as SKUs, attributes, metadata, assets, and prices.
- **Product context**, including catalog views, policies, catalog sources (locales), and price books.

A catalog view combines this context to define the catalog data and prices available to a storefront. Policies filter products for a business requirement, such as a brand, region, or customer group. You can create views for different audiences without copying the underlying product data.

## What is new

For [!DNL Adobe Commerce as a Cloud Service], Merchandising Services introduces the CCDM-based catalog model:

- Product data is separate from the context used to deliver it.
- Catalog views and policies define the products and prices available to different storefront audiences without copying the underlying product data.
- Storefront requests can use catalog view and policy identifiers to retrieve data for the required context.

Search and recommendations are existing Commerce capabilities, not new capabilities introduced by CCDM. The change is the catalog model and how storefronts request catalog data.

## Impact on customers and partners

- **Merchants** can define audience-specific assortments and pricing with catalog views, policies, catalog sources, and price books.
- **Storefront developers and integration partners** map catalog requests to the appropriate catalog view and policy, and verify how requests provide locale and pricing context.
- **Existing customers** are not automatically changed to the CCDM-based model.

Cart, checkout, and order management remain part of [!DNL Commerce Foundation]. CCDM changes catalog organization and delivery, not those transaction workflows. New [!DNL Adobe Commerce as a Cloud Service] projects include Merchandising Services by default.

The following diagram shows the position of Merchandising Services in the [!DNL Adobe Commerce as a Cloud Service] architecture.

![Adobe Commerce as a Cloud Service architecture showing Merchandising Services alongside Commerce Foundation](./assets/data-flow-ccdm.png){zoomable="yes"}
