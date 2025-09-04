---
title: Add tax, attribute set, and inventory metadata
description: Learn how to extend the product schema and feed data to include metadata for tax classification, attribute set information, and advanced inventory settings
role: Admin, Developer
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/

---
# Add tax, attribute set, and inventory metadata

The Adobe Commerce Extra Product Attributes module extends product data feeds to include additional product metadata from Adobe Commerce product configurations:

* [Tax classification](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [Attribute set](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [Inventory](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

Once installed, the module automatically captures and exports this metadata during product synchronization with no additional configuration required.

**Prerequisites**:

This optional module requires the [Adobe Commerce Catalog Data Exporter](https://experienceleague.adobe.com/docs/commerce-admin/catalog/services/data-exporter.html) and is designed for use with Live Search, Catalog Service, and Product Recommendations.

## Key benefits

* **Automatic enhancement**: Enriches product feeds with tax, attribute set, and inventory data
* **Seamless integration**: Provides essential context for external systems and services
* **Zero configuration**: Works immediately after installation
* **Real-time updates**: Synchronizes automatically with product changes

### Install the extension

>[!BEGINSHADEBOX]

**Requirements**

* PHP 8.1, 8.2, 8.3, or 8.4
* Adobe Commerce 2.4.4+
*[Adobe Commerce Data Export extension](manage-extension.md#update-a-module-to-a-specific-version), version 103.4.11 or later
* Access to [repo.magento.com](https://repo.magento.com)

  For key generation and obtaining the necessary rights, see [Get your authentication keys](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). For cloud installations, see the [Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys).
* Access to the command line of the Adobe Commerce application server.

>[!ENDSHADEBOX]

### Installation steps

Install the latest version of the Extra Product Attributes module (`adobe-commerce/module-extra-product-attributes`) on an Adobe Commerce instance that is running Adobe Commerce version 2.4.4 or later.

>[!BEGINTABS]

>[!TAB Cloud infrastructure (PaaS)]

Use this method to install the [!DNL Extra Product Attributes] module for a Commerce on cloud infrastructure instance.

1. On your local workstation, navigate to the project directory for your Adobe Commerce on cloud infrastructure project.

   >[!NOTE]
   >
   >For information about managing Commerce project environments locally, see [Managing branches with the CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) in the _Adobe Commerce on Cloud Infrastructure User Guide_.

1. Check out the environment branch to update using the Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Add the Catalog Service module.

   ```bash
   composer require adobe-commerce/extra-product-attributes --no-update
   ```

1. Update package dependencies.

   ```bash
   composer update adobe-commerce/extra-product-attributes
   ```

1. Add, commit, and push the code changes for the `composer.json` and `composer.lock` files to the cloud environment.

   ```shell
   git add -A
   git commit -m "Add extra product attributes module"
   git push origin <branch-name>
   ```

   Pushing the updates to the cloud environment initiates the [Commerce cloud deployment process](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) to apply the changes. Check the deployment status from the [deploy log](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

1. Verify installation by running a product synchronization:

   ```shell
   bin/magento saas:resync --feed=products
   bin/magento saas:resync --feed=productAttributes
   ```

>[!TAB On-premises]

Use this method to install the [!DNL Extra Product Attributes] for an on-premises instance.

1. Use Composer to add the Catalog Service module to your project:

   ```bash
   composer require adobe-commerce/extra-product-attributes --no-update
   ```

1. Update dependencies and install the extension:

   ```bash
   composer update adobe-commerce/extra-product-attributes
   ```

1. Run the following commands to complete the installation:

   ```shell
   bin/magento setup:upgrade
   ```

   ```shell
   bin/magento setup:di:compile
   ```

   ```shell
   bin/magento setup:static-content:deploy -f
   ```

   ```shell
   bin/magento cache:clean
   ```

1. **Verify installation** by running a product synchronization:

   ```bash
   bin/magento saas:resync --feed=products
   bin/magento saas:resync --feed=productAttributes
   ```

   >[!TIP]
   >
   >In some cases, particularly when deploying to production, you might want to avoid clearing compiled code because it can take time to rebuild. Ensure that you back up your system before making any changes.

>[!ENDTABS]

## Features and exported attributes

The module adds three additional attributes to your existing product data feeds:

### 1. Tax class information (`ac_tax_class`)

**Purpose**: Provides tax classification information for each product.

**Data Format**: String value containing the tax class name

**Example output**:

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**Use cases**:

* Tax compliance reporting
* Integration with external tax calculation services
* Product categorization for accounting systems

### 2. Attribute set information (`ac_attribute_set`)

**Purpose**: Identifies which attribute set is assigned to each product.

**Data Format**: String value containing the attribute set name

**Example output**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**Use cases**:

* Product template identification
* Catalog management and organization
* Third-party system integration requiring attribute set context

### 3. Advanced inventory data (`ac_inventory`)

**Purpose**: Provides inventory management settings for each product.

**Data Format**: JSON-encoded string containing inventory configuration

**Included fields**:

* `manageStock` (boolean): Whether stock management is enabled
* `cartMinQty` (float): Minimum quantity allowed in shopping cart
* `cartMaxQty` (float): Maximum quantity allowed in shopping cart
* `backorders` (string): Backorder policy where value is one of the following:
  * `"no"`: No backorders allowed
  * `"allow"`: Allow quantity below 0
  * `"allow_notify"`: Allow quantity below 0 and notify customer
* `enableQtyIncrements` (boolean): Whether quantity increments are enabled
* `qtyIncrements` (float): Required quantity increment value

**Example output**:

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**Use cases**:

* Inventory management system integration
* Shopping cart validation rules
* Order fulfillment process optimization
* Customer experience customization

### Data export feed enhancement

The Extra Product Attribute module enhances the following existing product feeds by integrating the new attribute data automatically.

* **Products Feed** (`products`): Enhanced with the three additional attributes

  * The module adds the `ac_tax_class`, `ac_attribute_set`, and `ac_inventory` attributes to each product record in the existing `products` feed
  * Original product data remains unchanged, only additional attributes are appended
  * Maintains backward compatibility with existing feed consumers

* **Product Attributes Feed** (`productAttributes`): Enhanced with attribute metadata for the new attributes

  * Automatically registers metadata for the three new attributes in the `productAttributes` feed
  * Provides attribute configuration details (data types, visibility settings, and so on)
  * Ensures external systems understand the new attribute schema

### Synchronization commands

When you need to synchronize product data after installing this module, use the [standard Adobe Commerce SaaS resync commands](data-export-cli-commands.md):

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## Troubleshooting

**Products missing additional attributes:**

* Verify the module is properly installed and enabled
* Run the resync commands to refresh product data
* Check that products have valid tax class and attribute set assignments

**Inventory data appears incorrect:**

* Verify that inventory settings are configured correctly in the Admin
* Check for website-specific inventory overrides
* Ensure that the [Inventory Management module](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) is functioning correctly

For further details, see the [Inventory Management Guide](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) in the *Adobe Commerce Merchant Documentation*.

**Performance concerns:**

* Monitor export process performance after installation
* Consider scheduling resyncs during low-traffic periods

### Logging and debugging

The module logs export errors and warnings to the standard Commerce logging system. If you encounter issues during product synchronization, check the data export logs. For details, see [Review logs and troubleshoot](troubleshooting-logging.md).

## Support and compatibility

This module is designed to work seamlessly with the Adobe Commerce data export infrastructure and is compatible with:

* Multi-store and multi-website configurations
* Custom product types and attribute sets
* Third-party inventory management extensions
* External PIM and ERP integrations

For additional support, contact your Adobe Commerce support team.
