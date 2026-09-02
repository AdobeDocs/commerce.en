---
title: Collect Data
description: Learn how events collect data for [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
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
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
    internal-label: Machine learning
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
---
# Collect Data

When you install and configure [[!DNL Product Recommendations]](install-configure.md), the module deploys behavioral data collection to your storefront. This mechanism collects anonymized behavioral data from your shoppers and powers [!DNL Product Recommendations]. For example, the `view` event is used to compute the `Viewed this, viewed that` recommendation type, and the `place-order` event is used to compute the `Bought this, bought that` recommendation type.

To learn more about the behavioral data that the [!DNL Product Recommendations] events collect, see the [developer documentation](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

>[!NOTE]
>
>Data collection for the purposes of [!DNL Product Recommendations] does not include personally identifiable information (PII). All user identifiers, such as cookie IDs and IP addresses, are strictly anonymized. Learn [more](https://www.adobe.com/privacy/experience-cloud.html).

## Healthcare customers

If you are a healthcare customer and have installed the [Data Services HIPAA extension](../data-connection/hipaa-readiness.md#installation), which is included with the [Data Connection](../data-connection/overview.md) extension, [!DNL Product Recommendations] stops collecting storefront event data because it is generated on the client side.

To resume collecting and sending storefront event data, re-enable event collection for [!DNL Product Recommendations]. For more information, see [General configuration](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Data types and events

There are two types of data used in Product Recommendations:

- **Behavioral** - Data from a shopper's engagement on your site, such as product views, items added to a cart, and purchases.
- **Catalog** - Product metadata, such as name, price, availability, and so on.

When you install the `magento/product-recommendations` module, Adobe AI aggregates the behavioral and catalog data, creating Product Recommendations for each recommendation type. The Product Recommendations service then deploys those recommendations to your storefront in the form of a widget that contains the recommended product _items_.

Some recommendation types use shoppers' behavioral data to train machine learning models and generate personalized recommendations. Others rely only on catalog data. To start using Product Recommendations quickly, choose from the following catalog-only recommendation types:

- `More like this`
- `Visual similarity`

### Cold start

When can you start using recommendation types that use behavioral data? It depends. This situation is referred to as the _Cold Start_ problem.

The _Cold Start_ problem is the time required for a machine learning model to train before it can produce effective recommendations. For Product Recommendations, Adobe AI must collect enough data to train its models before you deploy recommendation units. More data generally improves recommendation accuracy and usefulness. Because data collection occurs on your live site, start this process early by installing and configuring the `magento/product-recommendations` module.

The following table provides some general guidance for the amount of time that it takes to collect enough data for each recommendation type:

| Recommendation type | Training Time | Notes |
|---|---|---|
|Popularity-based (`Most viewed`, `Most purchased`, `Most added to cart`) | Varies | Depends on volume of events - views are most common, and therefore learns faster; then adds to cart, then purchases|
|`Viewed this, viewed that` | Requires more training |Product views are decently high in volume|
|`Viewed this, bought that`, `Bought this, bought that`| Requires the most training |Purchase events are the most rare events on a commerce site, especially compared to product views|
|`Trending` | Requires three days of data to establish a popularity baseline| Trending is a measure of recent momentum in a product's popularity compared with its own popularity baseline. A product's trending score is computed using a foreground set (recent popularity over 24 hours) and a background set (popularity baseline over 72 hours). If the popularity of an item increases significantly within a 24 hour period as compared with its baseline popularity, then it receives a high trending score. Every product has this score, and the items with the highes score  at any time comprise the set of top trending products. |

Other variables that can impact the time needed to train:

- Higher traffic volume contributes to faster learning
- Some recommendation types train faster than others
- Adobe Commerce recomputes behavioral data every four hours. Recommendations become more accurate the longer they are used on your site.

To help you visualize the training progress of each recommendation type, the [create recommendation](create.md#readiness-indicators) page displays readiness indicators.

While your live site collects data and the machine learning models train, complete the remaining testing and configuration tasks. Once the models have enough data to generate useful recommendations, deploy the recommendation units to your storefront.

If your site doesn't receive enough traffic (views, purchases, or trends) for most product SKUs, the learning process may not complete, causing readiness indicators in the Admin to appear stuck. Readiness indicators help merchants choose the best recommendation type for their store, but they are only a guide and may never reach 100%. Learn more about readiness indicators. [Learn more](create.md#readiness-indicators) about readiness indicators.

### Backup recommendations {#backuprecs}

When insufficient input data prevents a recommendation unit from returning all requested items, Adobe Commerce fills it with backup recommendations. For example, after you deploy the `Recommended for you` recommendation type on the homepage, a first-time shopper may not have generated enough behavioral data for personalized recommendations. In this case, Adobe Commerce displays items based on the `Most viewed `recommendation type.

If input data collection is insufficient, the following recommendation types fallback to `Most viewed` recommendation type:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Caveats

- Ad blockers and privacy settings can prevent events from being captured and might cause the engagement and revenue [metrics](workspace.md#column-descriptions) to be under-reported. Additionally, some events are not sent due to shoppers leaving the page or network issues.
- [Headless implementations](headless.md) must implement eventing to power the Product Recommendations dashboard.
- For configurable products, Product Recommendations use the parent product's image. If the parent product has no image, that product does not appear in the recommendation unit.

>[!NOTE]
>
>If [Cookie Restriction Mode](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law) is enabled, Adobe Commerce does not collect behavioral data until the shopper consents to using cookies. If Cookie Restriction Mode is disabled, Adobe Commerce collects behavioral data by default.
