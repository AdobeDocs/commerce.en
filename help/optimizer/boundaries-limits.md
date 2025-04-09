---
title: Boundaries and Limits
description: Learn about the boundaries and limits for [!DNL Adobe Commerce Optimizer] to ensure it meets the needs of your business.
role: Admin, Developer
---
# Boundaries and limits

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

The following provides boundaries and limits for Adobe Commerce Optimizer.

## Catalog

- Base product ingestion rate is 1000 records per minute. Max product ingestion rate is 100,000 per minute.
- The base number of product updates per day is 1,000,000.
- The base number of products in a single scope is 250,000. The maximum number of products in a single scope is 100,000,000.
- The maximum number of scopes is 50.
- The number of variants per product is 10,000.
- The product size cannot exceed 200kb.
- Do we need a limit on the number of options a single product may have? The same question applies to the number of values within the option.

## Prices

- The maximum number of price books is 30,000. The base tier number of price books cannot exceed 100 and should follow the rule where (the number of price books) x (the number of channels) must be less than or equal to 100.
- Base price ingestion rate is 5000 records per minute. Max product ingestion rate is 500,000 per minute.
- A single price record cannot have more than 10 discounts.
- The base number of price updates per day is 5,000,000.

## Search and storefront

- The number of products that a single search request can return is 100.
- The maximum number of filtrable attributes is 200
- The maximum number of searchable attributes is  200
- The maximum number of sortable attributes is 50
- The maximum number of facets is 100. All the facets must be filterable attributes.
- The maximum number of options a single facet cat returns is 100, which can be increased per support request.

## Channels and polices
 
- The maximum number of channels per tenant is 30,000.
- The maximum number of polices assigned to one channel is 10.
- The maximum number of attribute values used in a policy is 100. 
- Do we need a limit on the number of price books a single channel can serve? 
- Explanation for limit suggestions
- The existing limit that allows pulling 500 items from search is too weak. Currently, we experience significant pressure from EDS publication scripts that exercise our API to pull the whole catalog data, with a step of 500. However, in real life, we do not have a customer who draws more than 48 items per request for the storefront scenario.
- The ingestion rate is calculated by the number of calls to the corresponding APIs, each containing up to 100 elements for products and 500 for prices.
- The ingestion rate for the product and prices works under the OR condition. Meaning, for the base tier, you may import 1000 products per minute OR 5000 prices.
- If underloaded, the system can process more requests. The rates we list as limits are guaranteed rates covered by SLA.
