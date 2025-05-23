---
title: Install and Configure
description: Learn how to install, update, and uninstall [!DNL Product Recommendations].
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Install and Configure

Deploying [!DNL Product Recommendations] to your storefront and Admin requires that you install the module and configure the [Commerce Services Connector](../landing/saas.md). As updates are released, you can easily update the installation with the latest version.

- [Install](#install)
- [Configure](#configure)
- [Update](#update)
- [Uninstall](#uninstall)

## Install [!DNL Product Recommendations] {#install}

Because the [!DNL Product Recommendations] module is a stand-alone metapackage, updates are released more frequently than Adobe Commerce. To make sure you are up to date with the latest bug fixes and features, refer to the [release notes](release-notes.md).

>[!IMPORTANT]
>
>Make sure you have the correct [entitlements](../landing/saas.md#credentials) to use Product Recommendations.

Install the `magento/product-recommendations` module with Composer:

```bash
composer require magento/product-recommendations
```

### Add Page Builder support {#pbsupport}

[!DNL Product Recommendations] for Page Builder is an optional module and is installed separately. To use [!DNL Product Recommendations] with Page Builder, install the module by running the following command:

```bash
composer require magento/module-page-builder-product-recommendations
```

By enabling [!DNL Product Recommendations] in Page Builder, you can add an existing, active [recommendation unit](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) to any content created in Page Builder, such as pages, blocks, and dynamic blocks.

See [Using [!DNL Product Recommendations] with Page Builder Content](page-builder.md) for further instructions.

### Add Visual similarity recommendation type {#vissimsupport}

The _Visual similarity_ recommendation type allows you to deploy a recommendation unit to your product detail page that displays products that are [visually similar](type.md#visualsim) to the product being viewed. This recommendation type is most useful where images and visual aspects of the products are important parts of the shopping experience. Install the _Visual similarity_ recommendation type by running the following command:

```bash
composer require magento/module-visual-product-recommendations
```

## Configure [!DNL Product Recommendations] {#configure}

1. After you install the `magento/product-recommendations` module, configure the [Commerce Services Connector](../landing/saas.md) by specifying API Keys and selecting a SaaS Data Space.

   Configuring this connection enables the data synchronization and communication between the Commerce instance, the Catalog Service, and other supporting services. Data synchronization is handled by the [SaaS Data Export extension](../data-export/overview.md).

1. To ensure that catalog export can run correctly, confirm that the [cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) jobs and the [indexers](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) are running and the `Product Feed` indexer is set to `Update by Schedule`.

After you successfully link the Commerce application to Commerce Services and specify the [SaaS Data Space](../landing/saas.md#saas-configuration), the catalog sync begins. You can then [verify](verify.md) that behavioral data is being sent to your storefront.

## Monitor and troubleshoot data synchronization

From the Commerce Admin, you can monitor the synchronization process using the [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Use the [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) and logs to manage and troubleshoot the process.

 You can then [verify](verify.md) that behavioral data is being sent to your storefront.

## Update your [!DNL Product Recommendations] installation {#update}

Like all of Adobe Commerce, [!DNL Product Recommendations] uses Composer for installation and updates. To update the `magento/product-recommendations` module, run the following:

```bash
composer update magento/product-recommendations --with-dependencies
```

To update to a major version, such as from 5.0 to 6.0, you must edit the root `composer.json` file for your project. (See the [release notes](release-notes.md) for information about the latest version.) For example, let's open the main `composer.json` file and search for the `magento/product-recommendations` module:

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Let's bump the major version from `5.0` to `6.0`:

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

Save the `composer.json` file and run:

```bash
composer update magento/product-recommendations --with-dependencies
```

Or if you have installed the `magento/module-visual-product-recommendations` and `magento/module-page-builder-product-recommendations` modules:

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> In versions 3.x.x of Product Recommendations, you only needed a single API key. In versions 4.x.x and higher, you must provide public and private API keys for both the sandbox and production environments. If you do not provide both pairs of API keys, you cannot access the Product Recommendations feature in the Admin. However,  data collection continues on your storefront and existing recommendations continue to be shown to your shoppers.

## Firewalls

To let Product Recommendations through a firewall, add `commerce.adobe.io` to the allow list.

## Uninstall [!DNL Product Recommendations] {#uninstall}

If necessary, you can [uninstall](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) the product-recommendations module.
