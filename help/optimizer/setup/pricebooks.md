---
title: Price Books
description: Learn how to manage price books in [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Price Books

This article describes how to define and assign price books to catalog views with proper data governance controls.

See the [developer documentation](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books) to learn how to ingest price book information from a third-party system into [!DNL Adobe Commerce Optimizer] using the Price Book API.

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


## Price Book Assignment

- Enable ACO users to assign one or multiple price books to a catalog view as "allowed price books"
- Provide capability to set a default price book for each catalog view
- Support hierarchical price book structures with maximum depth of 3 levels

### Hierarchical Price Book Structure

- Transition from the current "main" price book concept to hierarchical price books
- Support multiple price book trees, each with maximum depth of 3 (including root)
- Enable selective assignment of price books from any hierarchy level

**Example**: In hierarchy `Price Book A → Price Book B → Price Book C`, users can select only Price Books A and C as allowed price books.

### ACO User Interface

- **Display**: Present comprehensive list of all available price books during catalog view creation/editing
- **Assignment**: Enable multiple price book assignment to catalog views
- **Access Control**: Restrict catalog view operations to assigned price books only
- **Flexibility**: Support catalog views without assigned price books (storefront API restrictions apply)
- **Global Access**: Option to allow all price books for a catalog view (pending UX finalization)

### Commerce Optimizer UI

- **Assignment**: Enable default price book selection from allowed price books list
- **Constraint**: Enforce single default price book per catalog view
- **Flexibility**: Support catalog views without default price books
- **Validation**: Restrict default assignment to allowed price books only