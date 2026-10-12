---
title: Modernize an Existing Storefront
description: Learn how to plan an incremental migration from a legacy Adobe Commerce storefront to a storefront built on Edge Delivery Services and drop-in components.
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
---

# Modernize an existing storefront

If you're running a legacy storefront—such as a Luma theme or an older PWA Studio implementation—you can migrate incrementally to a storefront built on Edge Delivery Services and Commerce drop-in components, rather than rebuilding everything at once.

>[!NOTE]
>
>This guide applies to Adobe Commerce (on Cloud or on premises), Adobe Commerce as a Cloud Service, Adobe Commerce Optimizer connected to Adobe Commerce, and stand-alone Adobe Commerce Optimizer with an existing or third-party backend. See [Architecture options at a glance](../architecture-options/overview.md#architecture-options-at-a-glance) to confirm which option applies to your project.

## Where to start

1. Review the [Adobe Commerce Storefront overview](https://experienceleague.adobe.com/developer/commerce/storefront/) to understand what a storefront built on Edge Delivery Services looks like compared to your current implementation.
2. Use the [storefront developer guide](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) to scope which pages or flows to migrate first.
3. Keep your existing Commerce services connections ([!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations], [!DNL Payment Services]) in place—see [Set up Commerce services](set-up-commerce-services.md).

## Related guidance

- [Build a new storefront](build-new-storefront.md)
- [Architecture center](../architecture-center/overview.md)
