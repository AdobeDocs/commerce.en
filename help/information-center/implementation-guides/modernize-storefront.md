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
>This guide applies to Adobe Commerce as a Cloud Service and Adobe Commerce (on Cloud or on premises) connected to Adobe Commerce Optimizer, and stand-alone Adobe Commerce Optimizer with an existing or third-party backend. See [Architecture options at a glance](../architecture-options/overview.md#architecture-options-at-a-glance) to confirm which option applies to your project.

## Where to start

1. Review the [Adobe Commerce Storefront overview](https://experienceleague.adobe.com/developer/commerce/storefront/) to understand what a storefront built on Edge Delivery Services looks like compared to your current implementation.

1. Use the [Storefront Developer Guide](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) to scope which pages or flows to migrate first.

1. For Adobe Commerce as a Cloud Service, keep your existing Commerce services connections ([!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations], [!DNL Payment Services]) in place—see [Set up Commerce services](set-up-commerce-services.md).

## Related guidance

- [Build a new storefront](build-new-storefront.md)
- [Architecture options](../architecture-options/overview.md)
