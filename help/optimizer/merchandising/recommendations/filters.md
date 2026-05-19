---
title: Recommendation Filters
description: Learn how to use filters to control which products appear in [!DNL Adobe Commerce Optimizer] recommendations.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
TQID: https://experienceleague.adobe.com/-pmVrAgEsSkn66K00-eaoQ4TF-7Xyxuwlniip1cR4HM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Filter Products

[!DNL Adobe Commerce Optimizer] automatically applies non-configurable default filters to recommendation units. If you have multiple recommendation units deployed to a page, [!DNL Adobe Commerce Optimizer] filters out any products that are repeated in the units. Only the first reference to a repeated product is used, to make room for other products to be recommended. [!DNL Adobe Commerce Optimizer] also filters out any previously purchased products and those that are in the cart.

When you [create](create.md) a recommendation unit, you can define filters that control which products can be displayed in recommendations. These filters are based on a set of inclusion or exclusion conditions that you define. Only products that match all inclusion conditions appear in recommendations. Products that match any of the exclusion conditions are not recommended.

You can configure multiple filters and enable only those you want by selecting the toggle on each filter page. This allows you to create drafts of filters for future use. The number of enabled filters is displayed on each tab.

## Conditions

Conditions can be static or dynamic.

- A static condition uses existing product attributes to determine which products can appear in the unit. For example, you can specify that only in-stock products with a price greater than $25 appear in the unit.

- A dynamic condition keys off a shopper's current context, such as the currently viewed category or product. For example, when creating a product recommendation to be deployed on product detail pages, you can use a [dynamic price filter](#dynamic-price-filters-relative-to-current-product) to include or exclude products within a relative price range of the currently viewed product.

### Logical operators

The logical operators `AND` and `OR` are used to join multiple conditions. If using both inclusion and exclusion filters across filter types, inclusions are evaluated first to determine all possible products that can be recommended, then products that match any exclusion filters are removed from the list. **Price** filters use a different order among price rules: exclusions first, then inclusions. See [How include and exclude rules use price](#how-include-and-exclude-rules-use-price).

- `AND` - Joins two inclusion-filtering conditions
- `OR` - Joins two exclusion-filtering conditions

## Types of filters

Each filter type targets a different aspect of the catalog, such as product and price, so you can narrow or broaden which products are eligible for a unit. Choose the types that match your merchandising goals, then combine inclusion and exclusion conditions as needed; the subsections below describe how each type behaves and how [!DNL Adobe Commerce Optimizer] applies it.

>[!NOTE]
>
>Only products that match your **inclusion** filters can be recommended, and any product that matches an **exclusion** filter is removed.

### Price {#price}

>[!IMPORTANT]
>
>Price filtering is in beta.

Price filtering uses each product's **final computed price** for the storefront's **active price book**—the one assigned to the storefront where the recommendation unit is rendered. That value reflects discounts, promotions, and special pricing defined in that price book, not list price alone. It does not include shipping or cart-level adjustments. Evaluation uses only that storefront's price book; other storefronts or price books do not apply. How price books map to a storefront is configured with your catalog and [price books](../../setup/pricebooks.md) setup.

#### How include and exclude rules use price {#how-include-and-exclude-rules-use-price}

- **Exclusion rules** – Products whose final price **matches any** defined price exclusion are removed first.
- **Inclusion rules** – Among the remaining candidates, only products whose final price **matches all** defined price inclusion conditions stay eligible. That includes every enabled inclusion filter (for example, your price rule plus any other inclusion rules).

Price rules **filter** the recommendation candidate set; they do **not** re-rank products. The engine produces a ranked list, price include and exclude rules remove products from that list, and the relative order of remaining products stays the same. If fewer products qualify than the unit requests, only valid items are shown. If none qualify, the unit is not rendered (no empty placeholder).

**Displayed price** – The price shown on products inside the recommendation unit is the same **final price** from that storefront's price book, so what shoppers see matches the value used for filtering. In the Admin preview, configurable products may show a price range when variant prices differ; see [Configurable products in preview](#configurable-products-in-preview).

#### Static price range

Use a **static** price filter when you want a fixed minimum or maximum in your store's base currency, independent of the product a shopper is viewing.

##### Set up a static price filter

1. While [creating or editing](create.md) a recommendation unit, open **[!UICONTROL Filter products]** (or go to the _Filters_ step from the unit workflow).
1. Select the **[!UICONTROL Inclusions]** or **[!UICONTROL Exclusions]** tab, depending on whether you want to allow only products in a price range or block products in a range. The badge on each tab shows how many filters of that type are enabled.
1. In the list on the left, select **[!UICONTROL Price]**.
1. Turn **[!UICONTROL Enable filter]** on.

   Price values use the **website's base currency**, as noted on the page.

1. Open **[!UICONTROL Include products based on]** (on the **[!UICONTROL Inclusions]** tab) or the equivalent control on the **[!UICONTROL Exclusions]** tab, and choose **[!UICONTROL Set price range]**.
1. Set an optional **[!UICONTROL Min price]** and/or **[!UICONTROL Max price]** using the fields next to the currency symbol. You can type amounts or use the **-** and **+** controls to adjust values. Leave a bound empty if you do not need a minimum or maximum. The range is compared to each product's final computed price for the storefront's active price book.
1. Finish configuring the recommendation unit and save or publish as you normally would so the filter takes effect.

![Price Filter](../../assets/filter-price.png)

#### Dynamic price filters (relative to current product) {#dynamic-price-filters-relative-to-current-product}

Use a **dynamic** price filter when recommendations should be limited relative to the **currently viewed product** on a product detail page (PDP). The filter uses that product's final price as an **anchor** and compares recommended products against boundaries you define.

Dynamic operators are available only for [SKU-related recommendation types](types.md) that run in a product context, such as:

- Viewed this, viewed that
- Viewed this, bought that
- Bought this, bought that
- More like this
- Visual similarity

They are **not** available for popularity-based types (for example, **Most viewed** or **Most purchased**) because those units do not have a single current product to anchor the filter.

On the storefront, the recommendation drop-in reads the current product's price from the PDP context and sends it with the recommendation request. [!DNL Adobe Commerce Optimizer] uses that value as the anchor when evaluating dynamic price rules. For configurable products, the anchor is the **lowest variant** final price (`priceRange.minimum`).

##### Operators

In **[!UICONTROL Include products based on]** (or the exclusions equivalent), you can choose:

| Operator | Purpose |
| --- | --- |
| **Less than or equal to current product price** | Include or exclude products at or below a boundary derived from the anchor price plus an offset. |
| **Greater than or equal to current product price** | Include or exclude products at or above a boundary derived from the anchor price plus an offset. |
| **Within a value range of current product** | Include or exclude products whose final price falls within a fixed currency band around the anchor (offsets from the current price). |
| **Within a percentage range of current product** | Include or exclude products whose final price falls within a percentage band around the anchor. |

##### Offset semantics

For **Less than or equal to current product price** and **Greater than or equal to current product price**, the value you enter is a **numeric offset added to the anchor price** to form the boundary:

- A **negative** offset moves the boundary **below** the current product price.
- A **positive** offset moves the boundary **above** the current product price.
- **Empty** or **0** means **no limit** on that side; the backend treats them the same.
- You cannot use **0** to mean "exactly the current product price" as the boundary.

This matches [!DNL Product Recommendations] on PaaS. Labels in the Admin reflect these semantics directly.

##### Set up a dynamic price filter

1. [Create or edit](create.md) a **SKU-related** recommendation unit that is deployed on the **product detail** page (or another placement where a current product is always in context).
1. Open **[!UICONTROL Filter products]** and select the **[!UICONTROL Inclusions]** or **[!UICONTROL Exclusions]** tab.
1. Select **[!UICONTROL Price]** and turn **[!UICONTROL Enable filter]** on.
1. Open **[!UICONTROL Include products based on]** (or the exclusions equivalent) and choose a dynamic operator (for example, **Within a value range of current product**).
1. Enter offsets or range values as prompted. Use the preview to confirm results for a sample product.
1. Save or publish the unit.

Invalid values (non-numeric amounts, unsupported combinations, or ranges where minimum is greater than maximum) block save and show validation errors; **[!UICONTROL Save]** stays disabled until the filter is valid.

##### When no anchor price is available

If a dynamic price filter is enabled but the storefront cannot supply a current product price (for example, the unit is rendered outside a PDP context), [!DNL Adobe Commerce Optimizer] does not return unfiltered recommendations. The unit shows **no recommendations**, because showing unfiltered results would not match the rule you configured.

##### Configurable products in preview {#configurable-products-in-preview}

In the Admin **preview** panel, recommended product prices display as follows:

- **Simple products** – Single final price from the GraphQL response.
- **Configurable products** – If minimum and maximum variant prices differ, the preview shows a range (for example, `$min – $max`). If they are equal, a single price is shown.

The anchor price used for dynamic filter calculations on a configurable product is always the **minimum** variant final price, consistent with the storefront.

#### Price filter examples

The following examples use a current product price of **$500**. Adjust inclusion versus exclusion to match your merchandising goal.

| Operator | Tab | Goal | Example boundary |
| --- | --- | --- | --- |
| Less than or equal to current product price | Exclusions | Promote upsell by hiding lower-priced alternatives | Exclude products ≤ $500 |
| Less than or equal to current product price | Inclusions | Offer budget-friendly alternatives | Include products ≤ $500 |
| Greater than or equal to current product price | Exclusions | Avoid upsell in a budget-focused flow | Exclude products ≥ $500 |
| Greater than or equal to current product price | Inclusions | Surface premium alternatives | Include products ≥ $500 |
| Within a value range of current product | Exclusions | Diversify away from similar price points | Exclude $400–$600 |
| Within a value range of current product | Inclusions | Show comparable alternatives in a narrow band | Include $400–$600 |
| Within a percentage range of current product | Exclusions | Reduce similarly priced items (for example ±20%) | Exclude roughly $400–$600 |
| Within a percentage range of current product | Inclusions | Fair comparison within a comparable band | Include roughly $400–$600 |

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

<!--
### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.
-->
