---
title: Adobe Commerce SaaS vs PaaS comparison
description: Compare Adobe Commerce SaaS vs PaaS models to determine the best implementation approach for your business needs.
role: Architect, Developer
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
---
# Feature comparison

{{accs-early-access}}

Adobe Commerce offers three deployment models:

- [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."} [Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) (on-premises)

This comparison focuses on the differences between software-as-a-service (SaaS) and platform-as-a-service (PaaS) models, which provide different levels of customization, extensibility, and control over your commerce implementation.

>[!NOTE]
>
>The on-premises model shares similar capabilities with the PaaS model, so this comparison also applies when considering SaaS versus on-premises implementations.

## Store management features

The [Commerce Admin UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) is the primary interface for accessing features to manage backend store operations, inventory, pricing, promotions, and customer interactions. However, [!DNL Adobe Commerce as a Cloud Service] offers unique solutions that replace some of the well-known features available in Adobe Commerce on Cloud and on-premises projects.

The following table describes the features and replacement solutions available in [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>PaaS model [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}</th>
            <th>SaaS model [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."}</th>
            <th>Details</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Digital asset management</a></td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">Product Visuals</a></td>
            <td>A robust digital asset management (DAM) system that integrates with Adobe Experience Manager for managing rich media content. Alternatively, the default digital file and asset management feature provides basic asset management tools for storing and managing digital assets.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">Content Management System (CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
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
            <td rowspan="2">A rich view-model (read-only) service for managing catalog data and rendering product-related storefront experiences.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">Payments</a></td>
            <td><a href="../payment-services/guide-overview.md">Payment Services</a></td>
            <td>An integrated payment service that facilitates secure and efficient transactions.</td>
        </tr>
    </tbody>
</table>

## Extensibility and platform features

The following table compares platform capabilities and extensibility features to help you understand the differences and make an informed decision about which model best suits your business requirements before starting an implementation.

<table>
    <thead>
        <tr>
            <th>Feature</th>
            <th>PaaS model [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}</th>
            <th>SaaS model [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Platform capabilities</strong></td>
        </tr>
        <tr>
            <td>B2B functionality</td>
            <td>Full B2B capabilities available after installation</td>
            <td>Pre-installed with core B2B features<sup>1</sup></td>
        </tr>
        <tr>
            <td>Experimentation</td>
            <td>Add-on for certain tiers</td>
            <td>A/B testing to optimize engagement and conversion</td>
        </tr>
        <tr>
            <td>Feature and security updates</td>
            <td>Requires manual upgrade and patching</td>
            <td>Automatically deployed</td>
        </tr>
        <tr>
            <td>Hosting infrastructure</td>
            <td>Single-tenant</td>
            <td>Multi-tenant</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce Admin customization</strong></td>
        </tr>
        <tr>
            <td>Extensible core Admin screens</td>
            <td>Complete layout and functionality customization</td>
            <td>Preset filters, visibility controls</td>
        </tr>
        <tr>
            <td>Extensible new Admin screens</td>
            <td>Standard Admin UI integration and external app injection (Admin UI SDK)</td>
            <td>External app injection (Admin UI SDK)</td>
        </tr>
        <tr>
            <td>Customizable Admin theme</td>
            <td>Extensible theming framework</td>
            <td>No theming framework</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibility</strong></td>
        </tr>
        <tr>
            <td>Extensibility model</td>
            <td>In-process (PHP customization) and out-of-process (APIs, events, App Builder)</td>
            <td>Out-of-process only (APIs, events, App Builder)</td>
        </tr>
        <tr>
            <td>Extensible web APIs</td>
            <td>Native REST/GraphQL extensibility and API Mesh with custom resolvers</td>
            <td>API Mesh with custom resolvers</td>
        </tr>
        <tr>
            <td>Data model extensibility</td>
            <td>Complete data model customization</td>
            <td>Custom attributes for core and B2B entities<sup>2</sup></td>
        </tr>
        <tr>
            <td>Technologies</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Node</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Data & storage</strong></td>
        </tr>
        <tr>
            <td>Search index customizations</td>
            <td>Native search customization</td>
            <td>Requires third-party solutions</td>
        </tr>
        <tr>
            <td>Custom email types</td>
            <td>Full email customization</td>
            <td>Standard email templates only</td>
        </tr>
        <tr>
            <td>Custom data storage</td>
            <td>DB, file, cache, queue</td>
            <td>App Builder state library (file only)<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> Core <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B features</a>, like company management and quoting, are available out-of-the-box in SaaS. However, industry-specific customizations may require additional implementation considerations.
                <br><br>
                <sup>2</sup> Data model extensibility in SaaS supports <a href="https://developer.adobe.com/commerce/services/cloud/guides/custom-attributes/">extending core entities</a> beyond product and customer, including B2B entities. However, industry-specific data models (for example, dealer-specific attributes) could require additional architectural considerations.
                <br><br>
                <sup>3</sup> Adobe is actively working Document DB integration to address persistent storage needs for SaaS. Currently, implementations requiring long-term data storage may need to provision and maintain additional infrastructure.
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
>- Consider adopting [Merchandising Services powered by Channels and Policies](../optimizer/catalog/overview.md).
