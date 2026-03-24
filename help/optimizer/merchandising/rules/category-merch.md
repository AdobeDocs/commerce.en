---
title: Category Merchandising
description: Control and optimize how products appear on category pages in [!DNL Adobe Commerce Optimizer] using category rules, intelligent ranking, and manual actions.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
---
# Category Merchandising

Category merchandising helps you control how products are ordered on category pages. You combine **category rules** with **intelligent ranking** (including AI-driven signals), optional **price-based sorting**, and **manual** actions such as pin, boost, and bury—so you can curate discovery, run promotions, and align category pages with your strategy without relying on external tools.

Category behavior is configured as a **Category rule** in the merchandising rules workflow, alongside [search rules and default product-listing rules](overview.md).

## Where to work

1. In the left rail, go to _Merchandising_ > **Merchandising Rules**.
1. (Optional) Use the **Catalog view** control to choose the catalog view where the rule applies. See [Merchandising Rules workspace](workspace.md#select-catalog-view) for how catalog view scoping works.

   >[!IMPORTANT]
   >
   >Catalog view controls for rules are currently in beta.

1. [Create a rule](add.md) and set the **Rule type** to **Category rule** so the editor shows the category selector and category-page ranking options.

## Rule types

Each rule type has an information icon with a short explanation. Use the type that matches where shoppers should see the merchandising logic:

| Rule type | Purpose |
| --- | --- |
| **Search rule** | Applies merchandising and ranking logic when shoppers run a search that matches the rule's conditions. |
| **Category rule** | Applies merchandising and ranking logic to one or more selected categories, controlling product order on those category pages. |
| **All products rule** | Applies a default ranking and merchandising logic across product listings when no more specific search or category rule applies. |

## Select categories and catalog view

When **Category rule** is selected:

- Use **Catalog view** to choose which catalog view the rule applies to (or **All views**, depending on your setup).
- Use the **Category** control—a searchable list—to pick the category or categories the rule should affect. Selected categories appear below the control so you can confirm the scope.

## Intelligent ranking for categories

Intelligent ranking uses behavioral signals and (where applicable) AI to order products in the category listing. Depending on product and configuration, strategies can include:

- **Most viewed** – Ranks by how often products were viewed in a recent window.
- **Most purchased** / **Most bought** – Ranks by purchase frequency in a recent window.
- **Most added to cart** – Ranks by add-to-cart activity in a recent window.
- **Recommended for you** – Personalized ordering based on the shopper's behavior.
- **Trending** – Emphasizes products with recent upswings in popularity (for example, based on views).
- **Price (ascending / descending)** – Sorts the category listing by price.
- **None / default** – Uses the default merchandising order for the category when you do not choose another intelligent strategy.

Exact labels and time windows match what you see in the rule editor and may be refined over time. For how intelligent ranking combines relevance and behavioral signals in search contexts, see [Intelligent ranking](add.md#intelligent-ranking) in the rules topic.

## Manual ranking

Manual ranking overrides or adjusts the order produced by intelligent ranking (if any). You can define actions such as:

- **Pin** – Fix a product at a specific position in the category listing.
- **Boost** – Move products higher in the listing.
- **Bury** – Move products lower in the listing.

As with search rules, you can often pin by dragging products in the preview, or add events explicitly. See [Manual ranking](add.md#manual-ranking) for limits (for example, number of events), pinning behavior, and how to add events manually.

>[!NOTE]
>
>Merchandising and manual positions typically apply when the shopper uses the default sort for the listing (for example, relevance or position). If a shopper changes sort (for example, by name or price), pinned, boosted, buried, or hidden behavior may no longer match the preview. See the note in [Create and manage rules](add.md#manual-ranking).

## Create, edit, and publish a category rule

Use the same overall flow as other merchandising rules:

1. Click **[!UICONTROL Create rule]** (or open an existing rule and choose **Edit**).
1. Set **Rule type** to **Category rule**.
1. Choose **Catalog view** and **Category** as needed.
1. Select **Intelligent ranking** and any **Manual ranking** events.
1. Complete **Name**, **Description**, and **Date range**, test in the preview, then **Save and publish**.

For editing, viewing details, deleting, and field-level descriptions, see [Create and manage rules](add.md) and [Merchandising Rules workspace](workspace.md).

## Related topics

- [Merchandising rules overview](overview.md)
- [Create and manage rules](add.md)
- [Catalog views](../../setup/catalog-view.md)
