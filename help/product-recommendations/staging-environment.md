---
title: Test in Staging Environment
description: Learn how to use [!DNL Product Recommendations] from your production environment in your staging environment for testing purposes.
feature: Services, Recommendations, Staging
exl-id: 5b6d7615-6021-4419-98ea-006c8a299fe4
TQID: https://experienceleague.adobe.com/7e7e3T-vgkN-Pbqx6TwrBAWTEozhzS0h--tguOGe0yI
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
    internal-label: Machine learning
---
# Test in Staging Environment

Before you deploy recommendations to your production environment, test the service in a non-production environment to ensure that everything is working as expected.

[!DNL Product Recommendations] return products based on [shopper-behavioral data](events.md) collected from your storefront. In a non-production environment, however, it is likely you do not have any behavioral data from shoppers. The only recommendation type that you can test without behavioral data is `More like this`. This recommendation type does not require any input data, as it uses a direct content similarity match.

The following recommendation types require behavioral data:

- Most Viewed
- Viewed this, viewed that
- Bought this, bought that

How can you test your recommendations in a non-production environment using behavioral data? There are a couple of options.

## Fetch recommendations from production environment (recommended)

Adobe Commerce allows you to fetch recommendations from your production environment and preview them in your non-production environment by [switching](settings.md) the SaaS data space.

To fetch recommendations from your production environment, you must make sure that:

- Storefront data collection is [configured and enabled](install-configure.md) in the production environment.
- The catalog in your non-production environment is largely the same as the one in the production environment. Using similar catalogs ensures that the products returned in the recommendation units closely mimic those in the production environment.

## Generate behavioral data on non-production environment

1. Deploy the `magento/product-recommendations` module to a non-production environment where the catalog data is similar to your production catalog.

1. Use one of the non-production Data Space IDs for [configuration](../landing/saas.md#saas-configuration) in the Admin.

1. Generate the data yourself by clicking around your storefront to mimic the behavior of actual shoppers (or create an automation script). Through your testing, you generate behavioral events on your non-production environment. Those events are used to produce the product affinities that power recommendations. For testing, [!DNL Commerce] suggests that you interact with the following recommendation types:

   - Most Viewed - Requires minimal input data. Users must view products.
   - Viewed this, viewed that - Requires multiple users to view multiple products.
   - Bought this, bought that - Requires multiple users to purchase multiple products.

### Caveats

- The behavioral and catalog data from the non-production [SaaS Data Space](../landing/saas.md#saas-configuration) identify an isolated environment in which the resulting product recommendations are based entirely on the behavioral data generated on the associated storefront.

- Because you do not have large amounts of behavioral data, input data for computing product associations is sparse. However, that data is still sent to Sensei to compute the machine learning models and provide recommendations based on data generated within this environment.
