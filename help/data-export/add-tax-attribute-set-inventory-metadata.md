---
title: Extend and customize SaaS data export feed data
description: Learn how to extend the product schema and feed data to include metadata for tax classification, attribute set information, and advanced inventory settings
role: Admin, Developer
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/

---
# Add tax, attribute set, and inventory metadata

The Adobe Commerce Extra Product Attributes module enriches your product data feeds with additional product information. The module extends the standard product schema to include product metadata for tax classification, attribute set information, and advanced inventory settings. After you install this module, the data export automatically captures and exports the extended metadata values.

This is an optional module for customers with Adobe Commerce on cloud infrastructure projects that use the [Adobe Commerce Catalog Data Exporter](https://experienceleague.adobe.com/docs/commerce-admin/catalog/services/data-exporter.html) module to export product data to Adobe Commerce SaaS services like Live Search, Catalog Service, and Product Recommendations.

## Key Benefits

- **Enhanced Product Data**: Automatically enriches product feeds with tax class, attribute set, and inventory information
- **Improved Integration**: Provides additional context for external systems and services consuming product data
- **Zero Configuration**: Works automatically after installation with no additional setup required
- **Real-time Synchronization**: Data is updated automatically during product synchronization processes

## Installation

### Requirements

- PHP 8.1, 8.2, 8.3, or 8.4
- [Adobe Commerce Data Export extension](manage-extension.md#update-a-module-to-a-specific-version), version 103.4.11 or later.

### Installation Steps

1. **Install the module using Composer:**

   ```bash
   composer require adobe-commerce/module-extra-product-attributes
   ```

2. **Deploy the changes:**

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   bin/magento setup:static-content:deploy
   ```

3. **Verify installation** by running a product synchronization:

   ```bash
   bin/magento saas:resync --feed=products
   bin/magento saas:resync --feed=productAttributes
   ```

## Features and exported attributes

The module adds three additional attributes to your existing product data feeds:

### 1. Tax Class Information (`ac_tax_class`)

**Purpose**: Provides tax classification information for each product.

**Data Format**: String value containing the tax class name

**Example Output**:

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

**Use Cases**:

- Tax compliance reporting
- Integration with external tax calculation services
- Product categorization for accounting systems

### 2. Attribute Set Information (`ac_attribute_set`)

**Purpose**: Identifies which attribute set is assigned to each product.

**Data Format**: String value containing the attribute set name

**Example Output**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": ["Default"]
    }
  ]
}
```

**Use Cases**:

- Product template identification
- Catalog management and organization
- Third-party system integration requiring attribute set context

### 3. Advanced Inventory Data (`ac_inventory`)

**Purpose**: Provides inventory management settings for each product.

**Data Format**: JSON-encoded string containing inventory configuration

**Included Fields**:

- `manageStock` (boolean): Whether stock management is enabled
- `cartMinQty` (float): Minimum quantity allowed in shopping cart
- `cartMaxQty` (float): Maximum quantity allowed in shopping cart
- `backorders` (string): Backorder policy - "no", "allow", or "allow_notify"
- `enableQtyIncrements` (boolean): Whether quantity increments are enabled
- `qtyIncrements` (float): Required quantity increment value

**Example Output**:

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

**Backorder Policy Values**:

- `"no"`: No backorders allowed
- `"allow"`: Allow quantity below 0
- `"allow_notify"`: Allow quantity below 0 and notify customer

**Use Cases**:

- Inventory management system integration
- Shopping cart validation rules
- Order fulfillment process optimization
- Customer experience customization

### Data Export feed enhancement

**Important**: This module does not create new data export feeds. Instead, it enhances existing Adobe Commerce data export feeds by adding additional product attributes to them.

The module automatically integrates with the following existing feeds:

- **Products Feed** (`products`): Enhanced with the three additional attributes described below

  - The module adds three new attributes to each product record in the existing `products` feed
  - Original product data remains unchanged - only additional attributes are appended
  - Maintains backward compatibility with existing feed consumers

- **Product Attributes Feed** (`productAttributes`): Enhanced with attribute metadata for the new attributes

  - Automatically registers metadata for the three new attributes in the `productAttributes` feed
  - Provides attribute configuration details (data types, visibility settings, etc.)
  - Ensures external systems understand the new attribute schema

### Synchronization commands

When you need to synchronize product data after installing this module, use the standard Adobe Commerce SaaS resync commands:

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products

# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## Troubleshooting

### Common Issues

**Products missing additional attributes:**

- Verify the module is properly installed and enabled
- Run the resync commands to refresh product data
- Check that products have valid tax class and attribute set assignments

**Inventory data appears incorrect:**

- Verify inventory settings are properly configured in Admin
- Check for website-specific inventory overrides
- Ensure CatalogInventory module is functioning correctly

**Performance concerns:**

- Monitor export process performance after installation
- Consider scheduling resyncs during low-traffic periods

### Logging and Debugging

The module logs export errors and warnings to the standard Commerce logging system. If you encounter issues during product synchronization, check the data export logs. For details, see [Review logs and troubleshoot](troubleshooting-logging.md).

## Support and Compatibility

This module is designed to work seamlessly with the Adobe Commerce data export infrastructure and is compatible with:

- Multi-store and multi-website configurations
- Custom product types and attribute sets
- Third-party inventory management extensions
- External PIM and ERP integrations

For additional support, contact your Adobe Commerce support team.

