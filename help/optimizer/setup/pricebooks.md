---
title: Price Books
description: Learn how to manage price books in [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
---
# Price Books

This article describes how to define and assign price books to catalog views with proper data governance controls.

See the [developer documentation](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books) to learn how to ingest price book information from a third-party system into [!DNL Adobe Commerce Optimizer] using the Price Book API.

With price books you can define pricing catalog sources to manage product prices across different customer tiers and markets. Price books support a hierarchical model, allowing up to three levels of nested child price books under each base price book. Each price book can reference a parent price book, forming a tree structure for pricing catalog sources.

The base price book defines the currency for itself and all its child price books. Child price books inherit this currency and cannot override it.

## Key concepts

| Term | Description |
|------|-------------|
| **Price Book** | Logical grouping that defines price catalog source; for example, specific region, or customer tier and is used to manage product prices. |
| **Fallback Price Book** | The top-most price book in a hierarchy. It has no parent and is the *only* price book that defines the currency for itself and all its descendant price books.<br/><br/>If no parent is defined during price book creation (through the API), a new fallback price book is created. |
| **Parent Price Book** | A higher-level price book from which a child price book can inherit prices if they aren't explicitly set in the child. |
| **Hierarchy Depth** | Maximum of 3 levels (Fallback → Child → Grandchild)<br/><br/>not enforced at ingestion time. |
| **Currency** | Defined at fallback price book only. Inherited by all children, price books.<br/><br/>If currency is not specified during fallback price book creation (through the API) the currency defaults to USD. |
| **Product Price** | The specific price assigned to a product (SKU) within a particular price book. |
| **Discounts** | Discounts are defined in Product Price. Not inherited. |
