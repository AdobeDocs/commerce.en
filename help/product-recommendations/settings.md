---
title: Settings
description: Learn how to change the source of your [!DNL Product Recommendations] data and how to enable visual recommendations.
exl-id: fe37624d-c53e-40cd-b182-10f62cba74c0
TQID: https://experienceleague.adobe.com/GJ8h9mX-3vlH1AUxk7FyM0-7rZTt40SGmdwfEMlvLvE
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
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
---
# Settings

When you [configure a SaaS data space](../landing/saas.md#saas-configuration) for Recommendations, the SaaS data space collects catalog data and storefront-behavioral data. [Adobe AI](https://business.adobe.com/ai.html) analyzes that data and computes product associations used to serve Product Recommendations.

Non-production environments for testing or staging usually don't have the quantity or quality of storefront behavioral data to serve realistic product recommendations. Actual shopper behavior at scale can be captured only in a production environment. To solve this problem, Adobe Commerce allows you to use product recommendations from your production environment with other, non-production SaaS data spaces. Using actual storefront data in a non-production environment allows you to preview the recommendations your shoppers see and experiment with different recommendation types and placement locations. Recommendations from a different SaaS data space can be previewed by shoppers, but not clicked.

Staging orders are recorded using the staging `environmentId`. It does not affect production data. The production data is retrieved using the `alternateEnvironmentId`.

>[!NOTE]
>
>When using Product Recommendations through REST, the `alternateEnvironmentId` parameter can be used to specify other dataspaces. When using Product Recommendations through [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/), this parameter is not available.

## Choose the recommendations source

To change the source of your product recommendations data, choose the SaaS data space with the behavioral data that you want to use. Before you begin, make sure that:

- Storefront data collection must be [configured and enabled](install-configure.md) for your production environment and [verified](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) that behavioral data is being sent to Adobe Commerce.
- Your non-production environment catalog should be essentially the same as your production catalog. Using similar catalogs ensures that the product recommendation units returned closely mimic those in production.

1. Log in to the Admin of your non-production Adobe Commerce environment.

1. On the _Admin_ sidebar, go to **Marketing** > _Promotions_ > **Product Recommendations**.

1. Click **Settings**.

   ![product recommendation settings](assets/settings.png)
   _Settings_

1. In the _Recommendations source_ section, enable the **Fetch recommendations from a different SaaS data space** option. The _Recommendations source_ section only appears in a non-production environment.

   A list of _Available SaaS Data Spaces_ appears.

   ![product recommendation settings](assets/settings-select-saas.png)
   _Settings_

1. Select the SaaS data space that has shopper data you want to use.

1. Click **Save changes**.

   Adobe Commerce now fetches recommendations from the selected data space.

   >[!NOTE]
   >
   > While you can view recommendations fetched from another SaaS data space on the non-production storefront, you cannot click the recommendations.

### Configure a new SaaS data space

1. In the Recommendations source section, click **Edit Configuration**.

1. Follow the instructions to configure a new [[!DNL Commerce] service](/help/landing/saas.md).

## Enable visual recommendations

If the [Visual Product Recommendations](install-configure.md) module is installed, you must enable Visual Recommendations to use the [Visual Similarity](type.md#visualsim) recommendation type.

In the _Visual Recommendations_ section, set **Enable Visual Recommendations** to the active position.
