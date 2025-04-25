---
title: Adobe Commerce SaaS vs PaaS comparison
description: Compare Adobe Commerce SaaS vs PaaS models to determine the best implementation approach for your business needs.
role: Architect, Developer
---

# Feature comparison

Adobe Commerce offers three deployment models:

- Software-as-a-Service (SaaS)
- Platform-as-a-Service (PaaS)
- On-premises

This comparison focuses on the differences between SaaS and PaaS models, which provide different levels of customization, extensibility, and control over your commerce implementation. The on-premises model shares similar capabilities with the PaaS model, so this comparison also applies when considering SaaS versus on-premises implementations.

The following table compares platform capabilities and extensibility features to help you understand the differences and make an informed decision about which model best suits your business requirements before starting an implementation.

>[!NOTE]
>
>For information about feature replacements and new solutions for managing store operations available in the SaaS model, see [New feature solutions](#new-feature-solutions).

| Feature | SaaS model | PaaS model |
|---------|------------|------------|
| Customizable Admin theme | Not supported (Admin UI theming not available) | Supported (via extensible admin theming framework) |
| Extensible core Admin screens | Limited control / extension points (e.g., preset filters, visibility controls) | Full control over layout and functionality |
| Extensible new Admin screens | Supported via external app injection (Admin UI SDK) | Supported via standard admin UI |
| In-process execution customization | Out-of-process only (App Builder, microservices-based) | Supported (native extensibility framework) |
| B2B functionality | Supported (pre-installed with core B2B features)<sup>1</sup> | Supported |
| Data model extensibility | Supported via custom attributes for core and B2B entities<sup>2</sup> | Full control of data model |
| Search index customizations | Not supported (requires 3rd party) | Supported |
| Custom (new use case) email types | Not supported | Supported |
| Custom data storage | Limited (state-lib, file only, App Builder storage limitations)<sup>3</sup> | Supported (DB, file, cache, queue) |
| Primary technologies | CSS, HTML, JS, Node, CLI | PHP, XML, HTML, CSS, JS, CLI |
| Extensible web APIs | Limited (API Mesh with custom resolvers can extend functionality)<sup>4</sup> | Supported (native REST/GraphQL extensibility) |

<sup>1</sup> Core B2B features, like company management and quoting, are available out-of-the-box in SaaS. However, industry-specific customizations may require additional implementation considerations.

<sup>2</sup> Data model extensibility in SaaS supports extending core entities beyond just product and customer, including B2B entities. However, industry-specific data models (for example, dealer-specific attributes) may require additional architectural considerations.

<sup>3</sup> For the SaaS model's App Builder storage limitations, Adobe is actively working on solutions including Document DB integration to address persistent storage needs. Currently, implementations requiring long-term data storage may need to provision and maintain additional infrastructure.

<sup>4</sup> While direct extension of REST and GraphQL APIs is limited in SaaS, API Mesh can be used to modify schemas and add custom resolvers to augment the out-of-box APIs.

>[!NOTE]
>
>For future readiness when considering SaaS migration, it's recommended to:
>
>- Move suitable functionality to out-of-process implementations where possible.
>- Reduce the surface area that would need transition.
>- Consider API Mesh for extending API functionality.
>- Monitor Adobe's ongoing platform evolution and new capability releases.
>- Evaluate industry-specific data model requirements against available extensibility options.

## New feature solutions

The [Commerce Admin UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) is the primary interface for accessing features to manage backend store operations, inventory, pricing, promotions, and customer interactions. However, [!DNL Adobe Commerce as a Cloud Service] offers unique solutions that replace some of the well-known features available in Adobe Commerce on Cloud and on-premises projects.

The following table describes the features and replacement solutions available in [!DNL Adobe Commerce as a Cloud Service]:

| Feature | Solution | Availability | Details|
|---------|----------|--------------|--------|
| [Digital asset management](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management) | [Product Visuals](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration) or mini-DAM | Available | A robust digital asset management (DAM) system that integrates with Adobe Experience Manager for managing rich media content. Alternatively, the mini-DAM provides basic asset management tools for storing and managing digital assets. |
| [Content Management System (CMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview) | [Commerce Storefront](https://www.aem.live/) | Available | A basic CMS allowing users to create and manage documents and website content easily using document-based authoring. Alternatively, a Universal Editor that allows for more advanced content management and customization across multiple platforms. |
| [Content staging](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging) | [Catalog Service](../catalog-service/overview.md) | Roadmap | A catalog management tool that ties into Adobe Experience Platform, allowing for the management of large catalogs. |
| [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview) | [Commerce Storefront](https://www.aem.live/) | Available | A basic CMS allowing users to create and manage documents and website content easily using document-based authoring. Alternatively, a Universal Editor that allows for more advanced content management and customization across multiple platforms. |
| [Payments](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments) | [Payment Services for Adobe Commerce](../payment-services/overview.md) | Available | An integrated payment service that facilitates secure and efficient transactions. |
| [Shared catalog](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared) | [Price Indexing Service](../price-index/price-indexing.md) | Roadmap | Analyzes pricing data and suggests optimal pricing strategies for products based on various factors. |
| [URL rewrites](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite) | [Commerce Storefront](https://www.aem.live/) | Available | A basic CMS allowing users to create and manage documents and website content easily using document-based authoring. Alternatively, a Universal Editor that allows for more advanced content management and customization across multiple platforms. |
| [Visual Merchandiser](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser) | [Catalog Service](../catalog-service/overview.md)| Roadmap | A catalog management tool that ties into Adobe Experience Platform, allowing for the management of large catalogs. |
