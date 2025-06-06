---
title: Filter Products
description: Define conditions that either include or exclude products from being used as recommendations.
exl-id: 140bf047-4f6a-48da-b536-d96e78ae3d17
---
# Filter Products

Adobe Commerce automatically applies non-configurable default filters to recommendation units. If you have multiple recommendation units deployed to a page, Adobe Commerce filters out any products that are repeated in the units. Only the first reference to a repeated product is used, to make room for other products to be recommended. Adobe Commerce also filters out any previously purchased products and those that are in the cart.

When you [create](create.md) a recommendation unit, you can define filters that control which products can be displayed in recommendations. These filters are based on a set of inclusion or exclusion conditions that you define. Only products that match all inclusion conditions appear in recommendations. Products that match any of the exclusion conditions are not recommended.

You can configure multiple filters and enable only those you want by selecting the toggle on each filter page. This allows you to create drafts of filters for future use. The number of enabled filters is displayed on each tab.

## Conditions

Conditions can be static or dynamic.

- A static condition uses existing product attributes to determine which products can appear in the unit. For example, you can specify that only in-stock products with a price greater than $25 appear in the unit. Static conditions are available on all page types.

- A dynamic condition keys off a shopper's current context, such as the currently viewed category or product. For example, when creating a product recommendation to be deployed on product detail pages, you can create a condition to recommend only products that are within a relative price range of the currently viewed product. Dynamic conditions are available on every page type except the Home page and on pages with recommendations that are placed with Page Builder.

### Logical operators

The logical operators `AND` and `OR` are used to join multiple conditions. If using both inclusion and exclusion filters, the inclusions are evaluated first to determine all possible products that can be recommended, then products that match any exclusion filters are removed from the list.

- `AND` - Joins two inclusion-filtering conditions
- `OR` - Joins two exclusion-filtering conditions

>[!NOTE]
>
> Inclusion and exclusion filters replace the legacy category exclusions in versions 3.2.2 and later of the `magento/product-recommendations` module. See the [release notes](release-notes.md) to learn more about Adobe Commerce releases.

## Types of filters {#filtertypes}

![Filters](assets/rec-conditions.png)

### Category

[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}

Filters products based on their category. The category filter uses direct category assignments and their subcategories. For example, enabling an exclusion condition for category `Gear` excludes products assigned to `Gear` and all of its subcategories such as `Gear/Bags` or `Gear/Fitness Equipment`. The same applies for an inclusion filter on a category. For example, enabling an inclusion condition for category `Gear` includes products assigned to `Gear` and all of its subcategories such as `Gear/Bags` or `Gear/Fitness Equipment`.

The category field displays categories that belong to the current storeview. 

>[!NOTE]
>
>For B2B merchants, the Category filter adheres to any [customer-specific product categories](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html) you have configured.

Adobe Commerce recommends you use the following category filter configuration when you deploy recommendations to your page types:

|Page|Filter by|
|---|---|
|Home|Do not filter products.|
|Category|Filter products in the specific category.|
|Product Detail|Filter products in the same categories.|
|Cart|Filter categories of products in the cart.|
|Order Confirmation|Filter categories of products purchased.|

### Product

Product filters specify which specific products are eligible, or not eligible, to be displayed in recommendations. You cannot select products that are disabled or not visible individually because those products can never appear in recommendations.

>[!NOTE]
>
>Child products of a configurable product are not displayed in a recommendation unit because those child products have the visibility of _Not Visible Individually_.

### Type

[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}

A filter based on product type either includes or excludes all products of a specific type. Supported types include _simple_, _configurable_, _virtual_, _downloadable_, or _gift card_. _Bundle_, _grouped_, and custom product types are not supported.

### Visibility

[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}

Filters products based on visibility, such as: _Catalog_, _Search_, or both.

### Price

A filter based on the product price uses the final price to perform the comparison. The final price includes any discounts or special pricing available to anonymous shoppers. For B2B merchants, the price displayed reflects the [customer-specific group pricing](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) you have configured.

### Stock status

The following exclusion filters can be used to filter out products based on stock status:

- Out of stock - (Exclusion only) Excludes products that are out of stock.
- Low in stock - (Exclusion only) Excludes products that are low in stock. Low stock status is based on the _Only X left Threshold_ value in [Inventory configuration](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/inventory.html).
