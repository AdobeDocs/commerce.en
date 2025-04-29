---
title: Boundaries and Limits
description: Learn about the boundaries and limits for [!DNL Adobe Commerce Optimizer] to ensure it meets the needs of your business.
role: Admin, Developer
---
# Boundaries and limits

>[!NOTE]
>
>This documentation describes the boundaries and limits for early-access development and does not reflect all functionality intended for general availability.

The following provides boundaries and limits for Adobe Commerce Optimizer.

## Catalog

- The guaranteed rate of catalog ingestion is: 1000 products/minute and 5000 prices/minute
- The base number of product updates per day is 1,000,000.
- The total number of SKUs allowed in a single instance is 250,000. 
- The maximum number of scopes is 50.
- The number of variants per product is 10,000.
- The product size cannot exceed 200kb.

## Prices

- The maximum number of price books is 30,000. The base tier number of price books cannot exceed 100 and should follow the rule where (the number of price books) x (the number of channels) must be less than or equal to 100.
- The guaranteed price feed ingestion rate is 5000 records per minute. 
- A single price record cannot have more than 10 discounts.
- The base number of price updates per day is 5,000,000.

## Search and storefront

- The number of products that a single search request can return is 100.
- The maximum number of filterable attributes is 200
- The maximum number of searchable attributes is 200
- The maximum number of sortable attributes is 50
- The maximum number of facets is 100. All the facets must be filterable attributes.
- The maximum number of options a single facet cat returns is 100, which can be increased per support request.

## Channels and polices

- The maximum number of channels per tenant is 1000.
- The maximum number of polices assigned to one channel is 10.
- The maximum number of attribute values used in a policy is 100. 

## Product discovery and recommendations

- For product discovery, attribute based merchandising and price settings are not supported.
- For recommendations,  only one recommendation type is supported; no category/attribute inclusions or exclusions, No recommendations preview on admin