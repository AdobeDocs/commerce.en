---
title: Migration and Adoption
description: Learn about routes for adopting Adobe Commerce Optimizer, modernizing an existing storefront, or migrating fully to Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---

# Migration and adoption

Adoption does not need to be a single, all-at-once platform change. Select a route based on whether your immediate goal is storefront modernization, merchandising improvement, backend modernization, or a complete move to managed software as a service (SaaS).

## Adoption routes

### Modernize the existing Adobe Commerce deployment

- Keep the existing Commerce Foundation as the transactional backend.
- Adopt the Commerce Storefront powered by [!DNL Edge Delivery Services].
- Use Storefront Services, App Builder, API Mesh, and an optional AEM Assets integration.

### Use Commerce Optimizer as a bridge

- Connect [!DNL Adobe Commerce] cloud or on-premises using the [!DNL Adobe Commerce Optimizer Connector].
- Adopt Merchandising Services, discovery, recommendations, and an Edge Delivery Services storefront.
- Keep [!DNL Adobe Commerce] as the primary system of record for products, prices, catalog structure, cart, checkout, customers, and orders.
- Use this architecture as a possible transition toward [!DNL Adobe Commerce as a Cloud Service].

### Migrate fully to Adobe Commerce as a Cloud Service

- Assess the current application, customizations, integrations, storefront, and data.
- Modernize customizations using SaaS-compatible extensibility patterns.
- Rebuild or adapt the storefront and integrations.
- Migrate and validate catalog, customers, orders, configuration, and supported custom data.
- Test, cut over, and operate the new SaaS environment.

### Adopt stand-alone Adobe Commerce Optimizer

- Ingest catalog and price data from a third-party Commerce platform, PIM, ERP, or other source.
- Use [!DNL Adobe Commerce Optimizer] Merchandising Services for catalog retrieval, discovery, recommendations, and merchandising.
- Use the Commerce Storefront powered by [!DNL Edge Delivery Services].
- Keep cart, checkout, customers, orders, payments, tax, shipping, and fulfillment in the connected third-party systems.

## Recommended sequence

1. Assess the current state and define system ownership.
1. Establish API-first integration boundaries.
1. Modernize the storefront and experience layer.
1. Adopt merchandising services and AEM Assets in parallel.
1. Migrate the Commerce Foundation when required.
1. Validate, cut over, monitor, and optimize.

## Related guidance

- [Choose a Commerce option](../portfolio/choose-commerce-option.md)
- [Architecture options](../architecture-options/overview.md)
- [Modernize an existing storefront](../implementation-guides/modernize-storefront.md)
- [Enable Adobe Commerce Optimizer](../implementation-guides/enable-aco.md)
