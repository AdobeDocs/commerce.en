---
title: Adobe Commerce SaaS vs PaaS comparison
description: Compare Adobe Commerce SaaS vs PaaS models to determine the best implementation approach for your business needs.
role: Architect, Developer
---

# Feature comparison

{{accs-early-access}}

Adobe Commerce offers three deployment models:

- [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) (on-premises)

This comparison focuses on the differences between software as a service (SaaS) and platform as a service (PaaS) models, which provide different levels of customization, extensibility, and control over your commerce implementation. The on-premises model shares similar capabilities with the PaaS model, so this comparison also applies when considering SaaS versus on-premises implementations.

The following table compares platform capabilities and extensibility features to help you understand the differences and make an informed decision about which model best suits your business requirements before starting an implementation.

>[!NOTE]
>
>See [New feature solutions](#new-feature-solutions) to learn about replacement features and new solutions that help you manage store operations in the SaaS model.

<table>
    <thead>
        <tr>
            <th>Feature</th>
            <th>SaaS model</th>
            <th>PaaS model</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce Admin customization</strong></td>
        </tr>
        <tr>
            <td>Extensible core Admin screens</td>
            <td>✅ Preset filters, visibility controls</td>
            <td>✅ Complete layout and functionality customization</td>
        </tr>
        <tr>
            <td>Extensible new Admin screens</td>
            <td>✅ External app injection (Admin UI SDK)</td>
            <td>✅ Standard Admin UI integration and external app injection (Admin UI SDK)</td>
        </tr>
        <tr>
            <td>Customizable Admin theme</td>
            <td>⚠️ No theming framework</td>
            <td>✅ Extensible theming framework</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibility</strong></td>
        </tr>
        <tr>
            <td>Extensibility model</td>
            <td>✅ Out-of-process only (APIs, events, App Builder)</td>
            <td>✅ In-process (PHP customization) and out-of-process (APIs, events, App Builder)</td>
        </tr>
        <tr>
            <td>Extensible web APIs</td>
            <td>✅ API Mesh with custom resolvers<sup>1</sup></td>
            <td>✅ Native REST/GraphQL extensibility and API Mesh with custm resolvers</td>
        </tr>
        <tr>
            <td>Data model extensibility</td>
            <td>✅ Custom attributes for core and B2B entities<sup>2</sup></td>
            <td>✅ Complete data model customization</td>
        </tr>
        <tr>
            <td>Technologies</td>
            <td>CSS, CLI, HTML, JS, Node</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Data & storage</strong></td>
        </tr>
        <tr>
            <td>Search index customizations</td>
            <td>⚠️ Requires third-party solutions</td>
            <td>✅ Native search customization</td>
        </tr>
        <tr>
            <td>Custom email types</td>
            <td>⚠️ Standard email templates only</td>
            <td>✅ Full email customization</td>
        </tr>
        <tr>
            <td>Custom data storage</td>
            <td>✅ state-lib, file only, App Builder storage<sup>3</sup></td>
            <td>✅ DB, file, cache, queue</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Functionality</strong></td>
        </tr>
        <tr>
            <td>B2B functionality</td>
            <td>✅ Pre-installed with core B2B features<sup>4</sup></td>
            <td>✅ Full B2B capabilities available after installation</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> <a href="https://developer.adobe.com/commerce/services/reference/cloud/rest/">REST</a> and <a href="https://developer.adobe.com/commerce/services/reference/cloud/graphql/">GraphQL</a> API schemas can only be extended using <a href="https://developer.adobe.com/graphql-mesh-gateway/">API Mesh</a>.
                <br><br>
                <sup>2</sup> Data model extensibility in SaaS supports <a href="https://developer.adobe.com/commerce/services/cloud/guides/custom-attributes/">extending core entities</a> beyond product and customer, including B2B entities. However, industry-specific data models (for example, dealer-specific attributes) could require additional architectural considerations.
                <br><br>
                <sup>3</sup> For the SaaS model's App Builder storage limitations, Adobe is actively working on solutions including Document DB integration to address persistent storage needs. Currently, implementations requiring long-term data storage may need to provision and maintain additional infrastructure.
                <br><br>
                <sup>4</sup> Core <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B features</a>, like company management and quoting, are available out-of-the-box in SaaS. However, industry-specific customizations may require additional implementation considerations.
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>When considering migration to SaaS, Adobe recommends that you:
>
>- Move suitable functionality to out-of-process extensibility where possible.
>- Reduce the surface area that requires transition.
>- Consider API Mesh for extending API functionality.
>- Monitor Adobe's ongoing platform evolution and new capability releases.
>- Evaluate industry-specific data model requirements against available extensibility options.
>- Consider adopting [Merchandsing Services powered by Channels and Policies](../optimizer/catalog/overview.md).

## New feature solutions

The [Commerce Admin UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) is the primary interface for accessing features to manage backend store operations, inventory, pricing, promotions, and customer interactions. However, [!DNL Adobe Commerce as a Cloud Service] offers unique solutions that replace some of the well-known features available in Adobe Commerce on Cloud and on-premises projects.

The following table describes the features and replacement solutions available in [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>Feature</th>
            <th>Solution</th>
            <th>Availability</th>
            <th>Details</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Digital asset management</a></td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">Product Visuals</a></td>
            <td>Available</td>
            <td>A robust digital asset management (DAM) system that integrates with Adobe Experience Manager for managing rich media content. Alternatively, the default digital file and asset management feature provides basic asset management tools for storing and managing digital assets.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">Content Management System (CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
            <td rowspan="3">Available</td>
            <td rowspan="3">A CMS allowing users to create and manage storefront content easily using document authoring or a Visual Editor and includes native experimentation capabilities.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">Page Builder</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL rewrites</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">Content staging</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">Catalog Service</a></td>
            <td rowspan="2">Roadmap</td>
            <td rowspan="2">A rich view-model (read-only) service for managing catalog data and rendering product-related storefront experiences.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">Payments</a></td>
            <td><a href="../payment-services/guide-overview.md">Payment Services</a></td>
            <td>Available</td>
            <td>An integrated payment service that facilitates secure and efficient transactions.</td>
        </tr>
    </tbody>
</table>
