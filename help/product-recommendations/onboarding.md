---
title: Onboarding
description: Learn the requirements and supported platforms in [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Onboarding

The onboarding process for [!DNL Product Recommendations] requires access to the command line of the server and consists of the following steps. If you are not familiar with working from the command line, ask a developer or system integrator to help.

- [Implementation Workflow](implementation-workflow.md)
- [Install and Configure](install-configure.md)
- [Settings](settings.md)
- [Verify](verify.md)
- [Staging Environment](staging-environment.md)

## Requirements

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Composer 2

### Supported platforms

- Adobe Commerce on premise (EE) : 2.4.4+
- Adobe Commerce on Cloud (ECE) : 2.4.4+

## Endpoint

[!DNL Product Recommendations] communicates through the endpoint at `https://catalog-service.adobe.io/graphql`.

### Page Builder support

[!DNL Product Recommendations] can be added to a page as a Page Builder content type. To add Page Builder support to Product Recommendations, refer to [Install and Configure](install-configure.md).

See [[!DNL Page Builder] Integration](page-builder.md) for instructions on how to add [!DNL Product Recommendations] into [!DNL Page Builder] content.

### SaaS price indexing

Product Recommendation customers can use [SaaS price indexing](../price-index/price-indexing.md), which provides faster price changes updates and synchornization time.

### B2B support {#b2bsupport}

B2B storefronts often require complex logic that dictates product visibility and pricing for each shopper or customer group. [!DNL Product Recommendations] now [support](release-notes.md) this functionality by honoring [category permissions](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html), [shared catalogs](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html), and [customer group-specific pricing](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html). For example, if you have hidden certain categories from your retail customer segment, then a shopper in that segment would not be shown recommendations for products in those categories. Also, when you define a shared catalog for specific customer groups and companies, those shoppers see recommendations only for products they can access. All recommended products reflect correct customer group-specific price based on each shopper's customer group.

>[!NOTE]
>
>Merchants may customize and extend widgets or storefront elements by using the [Catalog Service](../catalog-service/overview.md) Storefront API but any customization is out of scope for Adobe's support team.
