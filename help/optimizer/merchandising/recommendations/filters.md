---
title: Recommendation Filters
description: Learn how to use filters to control which products appear in [!DNL Adobe Commerce Optimizer] recommendations.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
---
# Filter Products

[!DNL Adobe Commerce Optimizer] automatically applies non-configurable default filters to recommendation units. If you have multiple recommendation units deployed to a page, [!DNL Adobe Commerce Optimizer] filters out any products that are repeated in the units. Only the first reference to a repeated product is used, to make room for other products to be recommended. [!DNL Adobe Commerce Optimizer] also filters out any previously purchased products and those that are in the cart.

When you [create](create.md) a recommendation unit, you can define filters that control which products can be displayed in recommendations. These filters are based on a set of inclusion or exclusion conditions that you define. Only products that match all inclusion conditions appear in recommendations. Products that match any of the exclusion conditions are not recommended.

You can configure multiple filters and enable only those you want by selecting the toggle on each filter page. This allows you to create drafts of filters for future use. The number of enabled filters is displayed on each tab.

## Conditions

Conditions can be static or dynamic.

- A static condition uses existing product attributes to determine which products can appear in the unit. For example, you can specify that only in-stock products with a price greater than $25 appear in the unit.

- A dynamic condition keys off a shopper's current context, such as the currently viewed category or product. For example, when creating a product recommendation to be deployed on product detail pages, you can create a condition to recommend only products that are within a relative price range of the currently viewed product.

### Logical operators

The logical operators `AND` and `OR` are used to join multiple conditions. If using both inclusion and exclusion filters, the inclusions are evaluated first to determine all possible products that can be recommended, then products that match any exclusion filters are removed from the list.

- `AND` - Joins two inclusion-filtering conditions
- `OR` - Joins two exclusion-filtering conditions

## Types of filters

Each filter type targets a different aspect of the catalog, such as product and price, so you can narrow or broaden which products are eligible for a unit. Choose the types that match your merchandising goals, then combine inclusion and exclusion conditions as needed; the subsections below describe how each type behaves and how [!DNL Adobe Commerce Optimizer] applies it.

>[!NOTE]
>
>Only products that match your **inclusion** filters can be recommended, and any product that matches an **exclusion** filter is removed.

### Price

>[!IMPORTANT]
>
>The following feature is in beta.

Price filtering uses each product's **final computed price** for the storefront's **active price book**—the one assigned to the storefront where the recommendation unit is rendered. That value reflects discounts, promotions, and special pricing defined in that price book, not list price alone. Evaluation uses only that storefront's price book; other storefronts or price books do not apply. How price books map to a storefront is configured with your catalog and [price books](../../setup/pricebooks.md) setup.

#### How include and exclude rules use price

- **Inclusion rules** – Only products whose final price **matches all** defined inclusion conditions remain eligible. That includes every enabled inclusion filter (for example, your price range plus any other inclusion rules).
- **Exclusion rules** – Products whose final price **matches any** defined exclusion condition are removed from recommendations.

**Displayed price** – The price shown on products inside the recommendation unit is the same **final price** from that storefront's price book, so what shoppers see matches the value used for filtering.

#### Set up a price filter

1. While [creating or editing](create.md) a recommendation unit, open **[!UICONTROL Filter products]** (or go to the _Filters_ step from the unit workflow).
1. Select the **[!UICONTROL Inclusions]** or **[!UICONTROL Exclusions]** tab, depending on whether you want to allow only products in a price range or block products in a range. The badge on each tab shows how many filters of that type are enabled.
1. In the list on the left, select **[!UICONTROL Price]**.
1. Turn **[!UICONTROL Enable filter]** on.

   Price values use the **website's base currency**, as noted on the page.

1. Open **[!UICONTROL Include products based on]** (on the **[!UICONTROL Inclusions]** tab) or the equivalent control on the **[!UICONTROL Exclusions]** tab, and choose **[!UICONTROL Set price range]**.
1. Set an optional **[!UICONTROL Min price]** and/or **[!UICONTROL Max price]** using the fields next to the currency symbol. You can type amounts or use the **-** and **+** controls to adjust values. Leave a bound empty if you do not need a minimum or maximum. The range is compared to each product's final computed price for the storefront's active price book.
1. Finish configuring the recommendation unit and save or publish as you normally would so the filter takes effect.

![Price Filter](../../assets/filter-price.png)

### Product

Product filters target individual catalog items by **SKU**. You add one or more SKUs to either allow only those products (**Inclusions**) or block them (**Exclusions**), using the same **[!UICONTROL Filter products]** page as [price filters](#price). You cannot surface disabled products or products that are not visible individually in a recommendation unit; those products never appear on the storefront regardless of filters.

#### Set up a product filter

1. While [creating or editing](create.md) a recommendation unit, open **[!UICONTROL Filter products]** (or go to the _Filters_ step from the unit workflow).
1. Select the **[!UICONTROL Inclusions]** or **[!UICONTROL Exclusions]** tab. The badge on each tab shows how many filters of that type are enabled.
1. In the list on the left, select **[!UICONTROL Product]**.
1. Turn **[!UICONTROL Enable filter]** on.

   The right panel heading reflects the tab, for example **[!UICONTROL Product inclusions]** or the equivalent for exclusions.

1. In **[!UICONTROL Product SKU]**, enter a SKU and click **[!UICONTROL Add]**. Repeat to add more SKUs.

   Under **[!UICONTROL Product SKUs]**, each SKU appears as a removable tag. Click **X** on a tag to remove that SKU, or click **[!UICONTROL Clear All]** to remove every SKU from the list.

1. Finish configuring the recommendation unit and save or publish as you normally would so the filter takes effect.

For **inclusions**, only products whose SKUs are listed (and that satisfy your other enabled inclusion filters) can be recommended. For **exclusions**, any product whose SKU is listed is not recommended, even if it would otherwise qualify.

![Product Filter](../../assets/filter-product.png)

>[!NOTE]
>
>Child products of a configurable product are not displayed in a recommendation unit because those child products have the visibility of _Not Visible Individually_.

<!--### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
