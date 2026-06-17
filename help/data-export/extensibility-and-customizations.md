---
title: Extend and customize SaaS data export feed data
description: Learn how to extend and customize the [!DNL SaaS Data Export] feed data.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Extend and customize SaaS data export feed data

The [!DNL Commerce Data Export] extension provides a way to export data from the [!DNL Commerce] application to Commerce Services like Live Search, Catalog Service, and Product Recommendations. If needed, you can extend and customize the feed data to include additional attribute data or modify the collected data.

After adding attribute data, it is accessible from the [attributes field](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) in the GraphQL schema for storefront services.

>[!NOTE]
>
>Adding or modifying feed data can impact performance and processing logic on the Commerce backend. Test customized code before merging to production. Instead of adding data to the backend, use API Mesh to extend the Catalog Service GraphQL schema. For configuration details, see [Catalog Service and API Mesh](../catalog-service/mesh.md).

## Extend system attributes data in the products feed

The products feed includes default system attributes which are required for product processing or commonly used by consumers. You can include additional system attributes in the products feed by adding them to the feed.

To complete this task, update the `magento/catalog-data-exporter` module to add the additional system attributes to the [dependency injection configuration file](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`).

Add the attributes to the Product Attribute query(`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`).

**Example**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Add product attributes to Adobe Commerce

Developers can add product attributes that are accessible from the [product attributes field](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields) by using one of the following methods:

- Add the attribute to Adobe Commerce for inclusion in the `products` feed data exported to Commerce storefront services.
- Add the attribute dynamically during the feed synchronization process using a plugin.

### Add the attribute to Adobe Commerce

You can add a product attribute from the Commerce Admin, or programmatically using a custom PHP module to define the attribute and update Adobe Commerce. Adding the attribute from the Commerce Admin is the simplest method because you can add the attribute and all the required metadata at once. The new attribute and its metadata properties are exported to the SaaS services automatically during the next scheduled synchronization.

#### Create the product attribute from the Admin

1. From the Commerce Admin, create the attribute from the product attribute configuration page ([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. Add the attribute to an attribute set as needed.

See [Create product attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) in the *Adobe Commerce Admin Guide*.

#### Create the product attribute programmatically

Add a product attribute programmatically by creating a data patch that implements the `DataPatchInterface`, and instantiate a copy of the `EavSetup Factory` class within the constructor to configure the attribute options.

When you define the attribute options, all attribute parameters except `type`, `label`, and `input` are optional. Define the following additional parameters and any others that differ from the default settings.

- **`user_defined` = `1`**—Export the attribute to storefront services during data synchronization
- **`used_in_product_listing` = `1`**—Make the attribute accessible within the product listing database query

For information about creating data patches, see [Develop data and schema patches](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) in the *PHP Developer Guide*.

### Add the product attribute dynamically

For details about creating product attributes dynamically without introducing new EAV Attributes, see [Add product attributes dynamically](add-attribute-dynamically.md).

## Feed schema overview (`et_schema.xml`) {#feed-schema-overview}

Each feed data structure is declared in `etc/et_schema.xml` using a simple XML DSL. The framework reads this file to determine which fields to collect and which PHP provider classes to call.

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

Key elements:

- `<record>` - defines the feed entity
- `<field>` - declares a data field; the `provider` attribute points to a PHP class implementing `DataProcessorInterface` that fetches the data
- `repeated="true"` - the field is an array of objects
- `<using>` - input parameters passed from the parent record context to the provider

>[!IMPORTANT]
>
>Adding a new field to `et_schema.xml` only changes what [!DNL Adobe Commerce] collects locally. The receiving SaaS service must also be updated to accept and process the new field before it has any effect on the storefront.

## Observe data after submission {#observe-data-after-submission}

[!DNL SaaS Data Export] dispatches the `data_sent_outside` event after each successful batch submission to a SaaS service. Use this event for audit logging, webhook triggers, or metrics collection.

**Event:** `data_sent_outside`

**Available data:**

| Key | Description |
|---|---|
| `timestamp` | Unix timestamp of the submission |
| `type` | Feed name (for example, `products`, `prices`) |
| `data` | The submitted feed payload |

**Example observer:**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

Register the observer in `etc/events.xml`:

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

For general information about events and observers, see [Events and Observers](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"} in the Adobe Commerce Developer documentation.

## Filter data before submission

Use the `Magento\SaaSCommon\Model\DataFilter` extension point to redact sensitive fields or skip specific entities before data is sent to the SaaS service. This is useful for compliance requirements such as GDPR or PCI where certain fields must not leave the Commerce instance.

Implement the interface and wire it via a DI preference in `etc/di.xml`:

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>Filtering is applied after data collection. If `PERSIST_EXPORTED_FEED=1` is set, the feed table stores the unfiltered payload before filtering occurs.

>[!MORELIKETHIS]
>
> - [Add product attribute dynamically](add-attribute-dynamically.md)
> - [Add tax class, attribute set, and inventory metadata](add-tax-attribute-set-inventory-attributes.md)
> - [How synchronization works](sync-overview.md)
