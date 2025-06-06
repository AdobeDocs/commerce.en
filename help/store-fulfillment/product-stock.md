---
title: Product Stock Management
description: Configure the merchant stock messaging and features available to customers.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
exl-id: 199d9466-062e-44f9-ab6a-85bec028acee
---
# Product Stock Management

As a merchant, you can use Adobe Commerce [Inventory Management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) stock and source options. Also, you can use the Store Fulfillment solution to control other inventory availability options related to your merchant store operations.

- Home delivery option from Merchant stores

- Allow / Available for Store Pickup

- UPC / SKU / Other Unique Product Identifiers

- Out of Stock Threshold

- Decrementing Inventory from specific locations upon order

Configure Product Stock options from the Admin: **[!UICONTROL Catalog > Products > Select Product]**

## **Product Stock Options**

| **Field**                                                | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | **Scope**  | **Required** |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|--------------|
| **Available for Home Delivery**                          | <p>Sets the Home Delivery (Ship-from-Store) availability for the product. When enabled, any assigned merchant store locations with available inventory for the product are considered eligible for the Home Delivery option. When this option is disabled, the product is never eligible for Home Delivery.</p>Usually, setting this option at the merchant store level is sufficient. However, there might be unique cases for specific products, such as those under federal shipping restrictions, which should not be eligible for Home Delivery.</p> | Website    | No           |
| **[!UICONTROL Available for Store Pickup]**              | <p>Set the Store Pickup availability for the product. When enabled, any assigned merchant store locations with available inventory for the product are considered eligible for the Store Pickup option. When disabled, the product is never eligible for Store Pickup.</p><p>This option can be useful to track merchant inventory in the system that you do not want to sell from your ecommerce channel.</p>                                                                                                                                            | Website    | No           |
| **[!UICONTROL UPC / SKU / Custom Scannable Identifier]** | This attribute should exist as a product attribute and relates to the **[!UICONTROL Barcode Source / Barcode Type]** setting. This attribute is used to track a scannable barcode for your products. This value might be sent when an order is sent to your merchant stores for picking. Store associates can use the value with the pick list to match products on the shelf using a barcode scanner.                                                                                                                                                    | Store View | No           |

{style="table-layout:auto"}

## Sources for product-level inventory

| **Field**                               | **Description**                                                                                                                                                                                                                                                                                                                                                                                         | **Scope** | **Required** |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Out of Stock Threshold]** | <p>Set the stock threshold for the item within each source. When stock falls below the threshold, it is considered out of stock at the source.</p><p>To use the global Store Configuration setting, check the **[!UICONTROL Use Default]** option.</p>                                                                                                                                                  | Global    | No           |
| **[!UICONTROL Allow Store Pickup]**     | <p>Explicitly set whether the item is available for store pickup, regardless of available inventory or merchant store location configuration.</p><p>To use the product-level setting, uncheck the [!UICONTROL Use Default] option and make your selection. Otherwise, this setting is chosen based on the configuration for **[!UICONTROL Allow In-Store Pickup]** that is set on the stock source.</p> | Global    | No           |

{style="table-layout:auto"}
