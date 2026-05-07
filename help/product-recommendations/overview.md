---
title: What Are Product Recommendations?
description: Learn about Product Recommendations in Adobe Commerce. Discover AI-driven storefront units, privacy, Admin and storefront paths, and key data retention.
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
---
# What are [!DNL Product Recommendations]?

[!DNL Product Recommendations] help you show personalized product recommendations on Adobe Commerce storefronts using [Adobe AI](https://business.adobe.com/ai.html) and machine learning on aggregated shopper behavior and your catalog. This overview covers service constraints (including HIPAA), data and privacy, where recommendation units appear, storefront implementation paths, how recommendations complement product relationships, and catalog data retention.

>[!IMPORTANT]
>
>**[!DNL Product Recommendations] is not a HIPAA-ready service.** Do not enable or use [!DNL Product Recommendations] in any Adobe Commerce implementation that uses the HIPAA-ready offering or otherwise processes protected health information (PHI). [!DNL Product Recommendations] is part of the Commerce SaaS services that are currently classified as non-HIPAA ready.
>
>For details about which Adobe Commerce capabilities are HIPAA ready and which services must not be used with PHI, see [HIPAA readiness on Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) and [Operations](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

## Data handling and privacy

Data collection for [!DNL Product Recommendations] does not include any personally identifiable information (PII). All user identifiers such as cookie IDs and IP addresses are strictly anonymized. To learn more, see the [Adobe Privacy Policy](https://www.adobe.com/privacy/policy.html).

For more information about data syncing, see the [Data Management Dashboard](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html).

## Where recommendations appear

Recommendations appear on the storefront as units with labels, such as "Customers who viewed this product also viewed". You can create, manage, and deploy recommendations across your store views from the Adobe Commerce Admin. If your Commerce project uses the [Adobe Commerce Optimizer Connector](https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/overview), you create, manage, and deploy recommendations through [Adobe Commerce Optimizer](../optimizer/overview.md).

## Storefront implementations

Choose the documentation that matches your storefront:

- **PWA Studio** — [PWA documentation](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **Custom frontends (for example, React or Vue.js)** — [Integrate [!DNL Product Recommendations]](headless.md) in a headless storefront
- **Commerce Edge Delivery Services (EDS)** — [Adobe Commerce Storefront documentation for EDS](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)

>[!NOTE]
>
>Headless and custom setups vary by stack. This product area documents a PWA Studio path and a general headless integration pattern; it does not cover every third-party or custom scenario.

## Product recommendations versus product relationships

Given the ever-changing complexities of online shopping, what works best for your storefront is often a combination of multiple key technologies. Using both [!DNL Product Recommendations] and [Product Relationships](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html) gives you more flexibility when promoting products. You can leverage [!DNL Product Recommendations] powered by Adobe AI to intelligently automate your recommendations at scale. Then, you can leverage [Related Product Rules](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html) when you must manually intervene and ensure that a specific recommendation is being made to a target shopper segment, or when certain business goals must be met.

Product recommendations allow you to:

- Choose from nine distinct intelligent recommendation types based on the following areas: shopper-based, item-based, popularity-based, trending, and similarity-based
- Use behavioral data to personalize recommendations throughout the shopper's storefront journey
- Measure key metrics relevant to each recommendation to help you understand the impact of your recommendations

## Product recommendations demo

Watch this video to learn about [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## Catalog data retention policy

The [!DNL Product Recommendations] service depends on catalog data that stays in sync with your Adobe Commerce environment. Inactive catalogs or environments that stop querying that data can enter hibernation, which affects what the service returns until you reactivate.

If you do not submit a query for the catalog data in your **testing** environment for 90 consecutive days, the catalog data is set to hibernation mode and no data is returned for any query. Catalog data in your **production** environment is not affected by the 90-day rule.

If your environment has an **empty catalog** 45 days after being created, the catalog data is set to hibernation mode and no data is returned for any query. This applies to both production and testing environments.

### Reactivate catalog data

To restore catalog data after hibernation, [submit a support request](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) with the title "Reactivate [!DNL Product Recommendations]" and include the environment IDs. Catalog data should be restored within a couple of hours.
