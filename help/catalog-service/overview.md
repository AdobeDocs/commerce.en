---
title: '[!DNL Catalog Service]'
description: '[!DNL Catalog Service] for Adobe Commerce provides a way to retrieve the contents of Product Display Pages and Product List Pages much more quickly than the native Adobe Commerce GraphQL queries.'
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
---
# [!DNL Catalog Service] for Adobe Commerce

The [!DNL Catalog Service] for Adobe Commerce extension provides rich view-model (read-only) catalog data to render product-related storefront experiences quickly and fully, including:

* Product detail pages
* Product list and category pages
* Search result pages
* Product carousels
* Product comparison pages
* Any other pages that render product data, such as cart, order, and wish list pages

The [!DNL Catalog Service] uses [GraphQL](https://graphql.org/) to request and receive catalog data including products, product attributes, inventory, and prices. GraphQL is a query language that a frontend client uses to communicate with the application programming interface (API) defined on a backend such as Adobe Commerce. GraphQL is a popular method of communication because it is lightweight and allows a system integrator to specify the contents and order of each response.

Adobe Commerce has two GraphQL systems. The core GraphQL system provides a wide range of queries (read operations) and mutations (write operations) that allow a shopper to interact with many types of pages, including product, customer account, cart, checkout, and more. However, the queries that return product information are not optimized for speed. The services GraphQL system can only perform queries on products and related information. These queries are more performant than similar core queries.

The data available to the Catalog Service is delivered by the SaaS Data Export extension. This extension synchronizes data between the Commerce application and connected Commerce Services to ensure that queries to the services GraphQL API endpoints return the most current catalog data. For information about managing and troubleshooting SaaS data export operations, see the [SaaS Data Export Guide](../data-export/overview.md).

[!DNL Catalog Service] customers can use the [SaaS price indexer](../price-index/price-indexing.md), which provides faster price updates and synchronization time.

## Architecture

The following diagram shows the two GraphQL systems:

![Catalog architecture diagram](assets/catalog-service-architecture.png)

In the core GraphQL system, the PWA sends a request to the Commerce application, which receives each request, processes it, possibly sending a request through multiple subsystems, then returns a response to the storefront. This round trip can cause slow page load times, potentially leading to lower conversion rates.

[!DNL Catalog Service] is a Storefront Services Gateway. The service accesses a separate database that contains product details and related information, such as product attributes, variants, prices, and categories. The service keeps the database in sync with the Adobe Commerce through indexation.
Because the service bypasses direct communication with the application, it is able to reduce the latency of the request and response cycle.

The core and service GraphQL systems do not directly communicate with each other. You access each system from a different URL, and calls require different header information. The two GraphQL systems are designed to be used together. The [!DNL Catalog Service] GraphQL system augments the core system to make product storefront experiences faster.

You can optionally implement [API Mesh for Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) to integrate the two Adobe Commerce GraphQL systems with private and third-party APIs and other software interfaces using Adobe Developer. The mesh can be configured to ensure calls routed to each endpoint contain the correct authorization information in the headers.

## Architectural details

The following sections describe some of the differences between the two GraphQL systems.

### Schema management

Since Catalog Service operates as a service, integrators do not need to be concerned about the underlying version of Commerce. The syntax of the queries is the same for all versions. In addition, the schema is consistent for all merchants. This consistency makes it easier to establish best practices, and increase reuse of storefront widgets significantly.

### Simplification of product types

The schema reduces the diversity of product types to two use cases:

* Simple products are products that are defined with a single price and quantity. Catalog Service maps the simple, virtual, downloadable, and gift card product types to `simpleProductViews`.

* Complex products are comprised of multiple simple products. The component simple products can have different prices. A complex product can also be defined so that the shopper can specify the quantity of component simple products. Catalog Service maps the configurable, bundle, and grouped product types to `complexProductViews`.

Complex product options are unified and distinguished by their behavior, not type. Each option value represents a simple product. This option value has access to the simple product attributes, including price. When the shopper selects all the options for a complex product, the combination of selected options points to a specific simple product. The simple product remains ambiguous until the shopper selects a value for all the available options.

#### Product view attributes

Both simple and complex products have customer-defined attributes that can be displayed on the storefront. These attributes are returned as [ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type). In Adobe Commerce, the available attributes are defined when the product is created. You can add additional attributes from the Adobe Commerce backend or programmatically. See [Extend and customize SaaS data export feed data](../data-export/extensibility-and-customizations.md).

>[!TIP]
>
>Instead of adding data types to the Commerce backend, you can use [API Mesh with the Catalog Service](mesh.md) to extend the Catalog Service GraphQL schema to add data or configure existing catalog data to enable new functionality.

### Prices

Simple products represent the base selling unit that has a price. [!DNL Catalog Service] calculates the regular price before discounts as well as the final price after discounts. Pricing calculations can include fixed product taxes. They exclude personalized promotions.

A complex product does not have a set price. Instead, Catalog Service returns the prices of linked simples. As an example, a merchant can initially assign the same prices to all the variants of a configurable product. If certain sizes or colors are unpopular, the merchant can reduce the prices of those variants. Thus, the price of the complex (configurable) product at first shows a price range, reflecting the price of both standard and unpopular variants. After the shopper has selected a value for all the available options, the storefront displays a single price.

The Catalog Service ensures accurate price updates and calculations by supporting prices with large values (up to 16 digits) and high decimal precision (up to 4 decimal places).

>[!NOTE]
>
> Commerce customers with [!DNL Catalog Service] can take advantage of faster price changes updates and synchronization time on their websites with the [SaaS price indexer](../price-index/price-indexing.md).

## Implementation

[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}

The installation process requires configuration of the [Commerce Services Connector](../landing/saas.md). Once that is accomplished, the next step is for a systems integrator to update the storefront code to incorporate the [!DNL Catalog Service] queries. All [!DNL Catalog Service] queries are routed to the GraphQL gateway. The URL is provided during the onboarding process.
