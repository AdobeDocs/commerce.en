---
title: "[!DNL Manage the Data Export extension]"
description: Learn how to upgrade the [!DNL Data Export] extension and to remove or disable data export services that are not required.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
TQID: https://experienceleague.adobe.com/ghrA-YFR7hurQgEnjS8PdxR7Zcx-ayLTuyBfhbCC-KI
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
---
# Manage the SaaS data export Extension

The [[!DNL data export] extension](https://github.com/magento/commerce-data-export) for SaaS services is a collection of modules that enable data collection and synchronization between Adobe Commerce and connected Commerce Services.

Specific modules are included in the metapackages for Adobe Commerce Services extensions such
as [Live Search](/help/live-search/overview.md), [Product Recommendations](/help/product-recommendations/overview.md), [Catalog Service](/help/catalog-service/overview.md), and the [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md). If you are using these services, no separate installation is required to enable the Data Export extension.

## Remove or disable Commerce data export features

If you don't need one of the installed commerce data export modules, use the `magento:module:disable` CLI command to disable it.

For example, there is a [Categories API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) that uses the categories permission feed data internally. If you are not using this API, you can disable the data export for the categories permission feed.

```shell
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Update a module to a specific version

You can update any of the installed commerce data export modules by using Composer. Review the [release notes](release-notes.md) to determine whether a fix you need is available, then upgrade to that specific version and any required dependencies.

>[!NOTE]
>
>If you update to the latest version of [Live Search](/help/live-search/overview.md), [Catalog Service](/help/catalog-service/overview.md), [Product Recommendations](/help/product-recommendations/overview.md), or the [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md), you also get the latest version of the data export extension. The data export metapackage is a dependency of the Composer packages for these services.

1. Log into the Commerce application server.

1. From the command line, update the module using Composer:

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

If the Commerce instance is deployed on Cloud infrastructure, update the extension from your cloud project directory. See [Upgrade an extension](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) in the _Adobe Commerce on Cloud Infrastructure Guide_.

>[!MORELIKETHIS]
>
> - [Release notes](release-notes.md)
> - [SaaS Data Export modules](reference/data-export-modules.md)
> - [Guide overview](overview.md)
