---
title: Boundaries and limits
description: Learn about the boundaries and limits for [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
---
# Boundaries and limits

The following provides boundaries and limits for [!DNL Adobe Commerce Optimizer].

## Catalog

- The guaranteed rate of catalog ingestion is: 1000 products/minute and 5000 prices/minute.
- The base number of product updates per day is 1,000,000.
- The total number of SKUs allowed in a single instance is 250,000. 
- The maximum number of catalog sources is 50.
- The number of variants per product is 10,000.
- The product size cannot exceed 200kb.

## Prices

- The maximum number of price books is 1,000.

## Product discovery and storefront

- The number of products that a single search request can return is 100.
- The maximum number of filterable attributes is 200.
- The maximum number of searchable attributes is 200.
- The maximum number of sortable attributes is 50.
- The maximum number of facets is 100. All the facets must be filterable attributes.
- The maximum number of options a single facet cat returns is 100, which can be increased per support request.

## Catalog views and policies

- The maximum number of catalog views per tenant is 1000.
- The maximum number of polices assigned to one catalog view is 10.
- The maximum number of attribute values used in a policy is 100. 

## Recommendations

- There is no support for category or attribute inclusions or exclusions.
- You cannot preview recommendations in [!DNL Adobe Commerce Optimizer].
