---
title: Migration and Adoption
description: Learn about routes for adopting Adobe Commerce Optimizer, modernizing an existing storefront, or migrating fully to Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
---

# Migration and adoption

Adoption doesn't need to be a single, all-at-once platform change. Select a route based on whether your immediate goal is storefront modernization, merchandising improvement, backend modernization, or a complete move to managed SaaS.

## Adoption routes

### Modernize the existing Adobe Commerce deployment

- Keep the existing Commerce Foundation as the transactional backend.
- Adopt the Commerce Storefront powered by [!DNL Edge Delivery Services].
- Use Storefront Services, App Builder, API Mesh, and an optional AEM Assets integration.

### Use Commerce Optimizer as a bridge

- Connect [!DNL Adobe Commerce] on Cloud or on premises using the [!DNL Adobe Commerce Optimizer Connector].
- Adopt Merchandising Services, discovery, recommendations, and an Edge Delivery Services storefront.
- Keep [!DNL Adobe Commerce] as the source of truth for products, prices, catalog structure, cart, checkout, customers, and orders.
- Use this architecture as a possible stepping stone toward [!DNL Adobe Commerce as a Cloud Service].

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

- [Choose a Commerce option](../choose-commerce-option/overview.md)
- [Architecture options](../architecture-options/overview.md)
- [Modernize an existing storefront](../implementation-guides/modernize-storefront.md)
- [Enable Adobe Commerce Optimizer](../implementation-guides/enable-aco.md)
