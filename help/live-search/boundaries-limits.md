---
title: Boundaries and Limits
description: Learn about the boundaries and limits for [!DNL Live Search] to ensure it meets the needs of your business.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
---
# Boundaries and limits

When it comes to site search, Adobe Commerce gives you options. Review the following boundaries and limits to ensure that [!DNL Live Search] and [!DNL Catalog Service] meet the needs of your business. If you need advanced search capabilities such as content search, bring-your-own-algorithm (BYOA), or attribute-based merchandising, consider a third-party search solution.

## General

- The [Advanced Search](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) module is disabled when [!DNL Live Search] is installed, and the Advanced Search link in the storefront footer is removed.
- [Tier Pricing](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier) is not supported in the [!DNL Live Search] field and Product Listing Page Widget.
- Product prices include value-added tax (VAT), but [!DNL Live Search] cannot display the VAT as a separate value.
- Content search (CMS pages and blocks) is not supported.
- The maximum number of results that can be paginated is 10,000. To ensure that shoppers do not have to use deep pagination when a category or search result includes a large number of products, provide meaningful ways to filter products.
- There is a hard limit of 1MB per attribute, including description and custom attributes.
- The search adapter does not support product attributes that are created with a custom source model and used as facets. To support this functionality, you must use the [Product Listing Page Widget](plp-styling.md).
- The search adapter has been deprecated as of Live Search 4.0.0.
- Custom product types are not supported.
- Custom attributes created programmaticaly with `"is_user_defined": false` are not supported.
- You can filter results using the "starts with" or "contains" conditions with some limitations as described in the [developer documentation](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations).
- You can only track performance metrics within the last year.
- If a search query contains multiple words, the blank space between the words causes them to be treated as separate search terms. Use [synonyms](./synonyms.md) if you want to account for multi-word search queries.
- [!DNL Live Search] does not support [search term redirects](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) natively. Implement redirects by using Fastly or another custom configuration.

## Indexing

- [!DNL Live Search] [indexes](indexing.md) up to a total of 450 product attributes per store view. These are distributed as follows:
   - 50 sortable attributes
   - 200 filterable attributes
   - 200 searchable attributes
- [!DNL Live Search] indexes only products from the Adobe Commerce database.
- CMS pages are not indexed.
- SKU, name, and category attributes are searchable by default and cannot be excluded from the search. Make sure you unassign the products from the categories if they are not intended to be in those categories.

## Facets

- From the set of defined filterable attributes, you can configure up to 100 attributes as facets.
- Within a facet, a maximum of 100 buckets can be returned. If you need to return more than 100 buckets, [create a support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) so Adobe can analyze the performance impact and determine if it is feasible to increase this limit for your environment.
- Dynamic facets can cause performance issues in large indexes and indexes with high ordinality. If you have created dynamic facets and notice any performance deterioration or page not loading with timeout errors, try changing your facets to pinned to determine if that resolves your performance issue.
- Stock status (`quantity_and_stock_status`) is not supported as a facet. You can use `inStock: 'true'` to filter out of stock products. This is supported out of the box in the `LiveSearchAdapter` module when "Display out of stock products" is set to "True" in the [!DNL Commerce] Admin.
- Date type attributes are not supported as a facet.
- Any changes made to the attribute metadata after that attribute is added as a facet, are not reflected in the facet.
- You can have up to 50 sortable attributes and 200 searchable attributes.

## Query

- [!DNL Live Search] uses a unique [GraphQL endpoint](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) for queries to support features such as dynamic faceting and search-as-you-type. Although similar to the [GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/), there are a few differences and some fields may not be fully compatible.
- The maximum number of results that can be returned in a search query is 10,000.
- The maximum number of results per page is 500.
- It is not possible to filter results using a date type attribute.

## Search merchandising

- The maximum number of search merchandising [rules](rules.md) per store view is 50.
- The maximum number of conditions per rule is 10.
- The maximum number of events per rule is 25.
- Rules and manually ranked products are applied to the search results when the default sort order, "Sort by: Most Relevant," is selected. If a shopper changes the sort order to something like sort by name or price, rules and manual rankings are no longer in effect.
- To avoid unpredictable results in paginated responses, the number of pinned products should not exceed the requested page size.

## Synonyms

- [!DNL Live Search] can manage up to 200 [synonyms](synonyms.md) per store view.

## Category merchandising

- You can create one rule per category for each store view.
- The maximum number of conditions per rule is 10.
- The maximum number of events per rule is 25.
- Rules are applied when a specific category is opened on the storefront and a rule exists for that category. For Category Merchandising rules, the default sort order is "Sort by: Position". If a shopper changes the sort order, all hidden, pinned, and buried products are no longer sorted.

## B2B and category permissions

- Products are not displayed if they are not added to a default shared catalog.
- To restrict customer groups using [category permissions](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions):
   - Products must be assigned to the root category. (**Note:**  You can remove this limitation by updating the SaaS Data Export extension to version 103.4.0+. See [Manage the data export extension](../data-export/manage-extension.md). 
   - The "Not Logged in" customer group must be given "Allow" browsing permissions.
   - To restrict products to the "Not Logged In" customer group, go to each category and set permission for each [customer group](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- Out-of-the-box support for B2B with the PLP widget on PWA Studio is not supported at this time. However, you can [use the API](install.md#pwa-support) to implement this functionality.
- Category facets in [!DNL Live Search] might display categories that are not displayable to a specific [customer group](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- [!DNL Live Search] can support up to 1,000 customer groups.

## [!DNL Storefront popover]

- The [[!DNL popover]](storefront-popover.md) is available only for stores that use the *Luma* theme, or a customized theme that is based on *Luma*. Breadcrumbs on the search results page will not have *Luma* styling.
- The [!DNL popover] does not support the *Blank* theme.
- The [!DNL popover] is not supported on the Quick Order form.
- Wishlists and product comparisons are not supported.
- The currency symbol for the Peruvian sol (PEN) is not supported.

## Troubleshooting

For help with troubleshooting common issues in [!DNL Live Search], see the following knowledgebase articles:

- [[!DNL Live Search] catalog not synchronized](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) - Provides solutions for when product catalog data is not syncing correctly between your Adobe Commerce store and the Live Search service. This article covers how to verify sync status, identify sync errors, and resolve data synchronization issues.
- [[!DNL Live Search] dashboard and search result ranking is incorrect](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect) - Addresses issues where search results or performance metrics displayed in the Live Search dashboard are not showing as expected. This article explains how to troubleshoot ranking discrepancies and dashboard data inconsistencies.
- [[!DNL Live Search] facets are not alphabetically sorted](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted) - Resolves the issue where facet values appear in an unexpected order rather than alphabetically. This article provides steps to configure and correct facet sorting behavior on your storefront.

If you need additional assistance, contact [support](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
