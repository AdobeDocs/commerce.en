---
title: Add tax class, attribute set, and inventory attributes
description: Learn how to extend the product feed data to include attributes for tax classification, attribute set, and advanced inventory settings
role: Admin, Developer
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
TQID: https://experienceleague.adobe.com/AWc-yAn-TyiBXQONoF2ZG9SFjj2u92CKbKvAY8mEVEE
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
---
# Add tax class, attribute set, and inventory attributes

The Adobe Commerce Extra Product Attributes module extends product data feeds. It includes additional product attributes from Adobe Commerce product configurations:

* [Tax classification](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [Attribute set](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [Inventory](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

Once installed, the module works automatically. It captures and exports the additional attributes during product synchronization. No additional configuration is required.

## Key benefits

* **Automatic enhancement**: Enriches product feeds with tax class, attribute set, and inventory attributes
* **Seamless integration**: Provides essential context for external systems and services
* **Zero configuration**: Works immediately after installation
* **Real-time updates**: Synchronizes automatically with product changes

## Features and exported attributes

The module adds three additional attributes to your existing product data feeds:

* `ac_tax_class`
* `ac_attribute_set` 
* `ac_inventory`

### 1. Tax class information (`ac_tax_class`)

**Purpose**: Provides tax classification information for each product

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

When you export tax class data to Commerce catalog services, this data becomes available for applications that support:

* Tax compliance reporting
* Integration with external tax calculation services
* Product categorization for accounting systems

### 2. Attribute set information (`ac_attribute_set`)

**Purpose**: Identifies which attribute set is assigned to each product

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

When you export attribute set data to Commerce catalog services, it enables advanced product management features in external systems. These features include:

* Product template identification
* Catalog management and organization
* Third-party system integration requiring attribute set context

### 3. Advanced inventory data (`ac_inventory`)

**Purpose**: Provides inventory management settings for each product

**Data Format**: JSON-encoded string containing inventory configuration

**Included fields**:

* `manageStock` (boolean): Whether stock management is enabled
* `cartMinQty` (float): Minimum quantity allowed in shopping cart
* `cartMaxQty` (float): Maximum quantity allowed in shopping cart
* `backorders` (string): Backorder policy. The value is one of the following:
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

When you export inventory data to Commerce catalog services, it enables advanced inventory management features in external systems. These features include:

* Inventory management system integration
* Shopping cart validation rules
* Order fulfillment process optimization
* Customer experience customization

## Data export feed enhancement

The Extra Product Attributes module enhances the existing product feeds. It integrates the new attribute data automatically.

* **Products Feed** (`products`): Enhanced with the three additional attributes

  * Adds the `ac_tax_class`, `ac_attribute_set`, and `ac_inventory` attributes to each product record
  * Keeps original product data unchanged
  * Maintains backward compatibility with existing feed consumers

* **Product Attributes Feed** (`productAttributes`): Enhanced with attribute metadata for the new attributes

  * Automatically registers metadata for the three new attributes in the `productAttributes` feed
  * Provides attribute configuration details (data types, visibility settings, and so on)
  * Helps external systems understand the new attribute schema

## Install the extension

**Requirements**

* PHP 8.1, 8.2, 8.3, or 8.4
* Adobe Commerce 2.4.4+
* [Adobe Commerce Data Export extension](manage-extension.md#update-a-module-to-a-specific-version), version 103.4.11 or later
* Access to [repo.magento.com](https://repo.magento.com)

  To generate keys and obtain the necessary rights, see [Get your authentication keys](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). For cloud installations, see the [Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/authentication-keys).
* Access to the command line of the Adobe Commerce application server.

### Installation steps

Add the `adobe-commerce/module-extra-product-attributes` module using Composer:

```shell
composer require adobe-commerce/module-extra-product-attributes
```

For detailed installation steps, see the following guides:

* [Install extension on Adobe Commerce on Cloud Infrastructure](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [Install extension Adobe Commerce on-premises](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Synchronize product data

After redeployment, the Adobe Commerce instance exports the additional data automatically during product synchronization. You can also use the `resync` CLI commands to synchronize immediately.

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

* Verify that the module is properly installed and enabled
* Run the resync commands to refresh product data
* Check that products have valid tax class and attribute set assignments

**Inventory data appears incorrect:**

* Verify that inventory settings are configured correctly in the Admin
* Check for website-specific inventory overrides
* Verify that the [Inventory Management module](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) is working correctly

For further details, see the [Inventory Management Guide](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) in the *Adobe Commerce Merchant Documentation*.

**Performance concerns:**

* Monitor export process performance after installation
* Consider scheduling resyncs during low-traffic periods

### Logging and debugging

The module logs export errors and warnings to the standard Commerce logging system. If you encounter issues during product synchronization, check the data export logs.

For details, see [Review logs and troubleshoot](troubleshooting-logging.md).

