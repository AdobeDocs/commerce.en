---
title: Manage Out-of-Stock Products in [!DNL Live Search]
description: 'Learn how to manage out-of-stock products in [!DNL Live Search] for Adobe Commerce. Configure inventory display, the inStock filter, and GraphQL API filtering.'
feature: Services, Search
role: Admin, Developer
level: Intermediate
---
# Manage out-of-stock products

You can control how out-of-stock products appear in [!DNL Live Search] search and category results using inventory configuration, query-time filters, and optional backend feature flags. These options have important limits, which this topic explains.

## Stock status filters

The Adobe Commerce stock attribute `quantity_and_stock_status` is not supported as a facet and does not appear in the **[!UICONTROL Add Facet]** dialog. However, [!DNL Live Search] exposes an `inStock` field you can use as a filter at query time.

## Hide out-of-stock products

Use one of the following approaches to hide out-of-stock products.

### Commerce configuration

1.From the *Admin*, go to **[!UICONTROL Stores]** > _[!UICONTROL Settings]_ > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]**.

1.Set **[!UICONTROL Display Out of Stock Products]** to **[!UICONTROL No]**.

1. Click **[!UICONTROL Save Config]**.

When **[!UICONTROL Display Out of Stock Products]** is **[!UICONTROL No]**, [!DNL Live Search] adds `inStock = 'no` to storefront queries through the PLP widget, so out-of-stock products are not returned.

### API filter

When you call the [!DNL Live Search] API directly (GraphQL or REST), filter out out-of-stock products explicitly, for example:

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

Use this approach when you do not route the request through the [Live Search PLP Widget](plp-styling.md).

### Show out-of-stock after in-stock results

To keep out-of-stock products in the result set but always after in-stock products when sorting by relevance, Adobe can enable an internal feature flag for your environment.

- This feature flag is not exposed in the [!DNL Live Search] Admin UI.
- To request it, [contact Adobe Support](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"} and reference the feature to move out-of-stock products to the end of search results.

>[!NOTE]
>
>After the flag is enabled, any remaining out-of-stock products in the result set move to the bottom when sorting by *Relevance*. Other sort orders (for example, *Price* or *Product Name*) are not affected.

### Search Merchandising rules and stock

Search Merchandising rules are query-based and target individual products, not whole groups by stock state or facet value:

- Rule conditions depend only on the shopper's search phrase (`Query is`, `Query contains`, `Query starts with`, `Query ends with`).
- Rule events (Boost, Bury, Pin, Hide) apply to one SKU per event.

Because of these constraints:

- You cannot create a rule that buries or hides all out-of-stock products based on stock status alone.
- You can manually hide or bury specific SKUs you add as events in a rule (subject to limits of 50 rules and 25 events per rule).

To hide or deprioritize out-of-stock products across the catalog, use the inventory configuration and `inStock` filter (and the optional feature flag) described in this topic instead of Search Merchandising rules.

>[!MORELIKETHIS]
>
> - [Search Merchandising rules](/rules.md)
> - [Configure Inventory Management global options](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/configuration)
