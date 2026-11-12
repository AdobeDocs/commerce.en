---
title: Merchandising Rules Best Practices
description: Learn the best practices for implementing merchandising rules for search, search suppression, default listings, and category pages.
role: Admin, Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
TQID: https://experienceleague.adobe.com/DrdrBBXeMyqQr16h1LrlSoet3F6ihn57LBmPFBUXmTs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Merchandising Rules Best Practices

To optimize conversion and revenue, implement effective **search rules**, a strong **default listing** rule, and **[category rules](add.md#rule-types)**. Adjust rankings using sales data, stock, promotions, and [intelligent ranking](add.md#intelligent-ranking).

Use **[search suppression rules](overview.md#search-suppression-rules)** when specific search terms must not return results, rather than when products only need a different ranking.

It is crucial to establish a well thought out **default rule**. Your [default rule](overview.md#default-rule) determines how search results are initially sorted when no more specific search rule applies, which improves discovery and purchase likelihood. Review it regularly so it keeps pace with shopper needs and campaigns.

## Tips to optimize search rules

- Pin or boost products with high sales volumes or recent sales activity.
- Prioritize products with high ratings and positive reviews.
- Ensure that in-stock items are ranked higher.
- Slightly prioritize products with higher profit margins without compromising relevance.
- Highlight products that are on sale or part of special promotions.
- Set search rules during promotion or sales periods automatically by using the date range during your promotion period.
- Tailor search results based on individual shopper behavior using [intelligent ranking](add.md#intelligent-ranking), such as "recommended for you", "most viewed" and so on.
- When an intelligent strategy other than **None** is selected, tune **[Intelligent ranking boost](add.md#intelligent-ranking-boost)** per rule and validate in **Test your rule** before publishing.
- Always use the "Test your rule" panel to preview how your intelligent ranking strategy affects actual search results for different queries.

## Tips for category rules

- Use [category rules](add.md#rule-types) on high-traffic or high-margin **category pages** where curated order matters as much as search—for example, seasonal collections or featured departments.
- Align **intelligent ranking** (for example, trending, most viewed) with how shoppers browse that category; category pages do not use search query text the way search rules do. See [Intelligent ranking](add.md#intelligent-ranking). For intelligent methods other than **None**, use **[Intelligent ranking boost](add.md#intelligent-ranking-boost)** and category preview to tune behavioral strength for that category rule.
- Apply **pin**, **boost**, and **bury** consistently with your campaign plan; remember that manual positions usually apply only when the shopper uses the **default sort** for the listing. See [Manual ranking](add.md#manual-ranking).
- Preview in the **category** rule flow in the editor and validate on the storefront after publish, the same discipline you use for the "Test your rule" panel on search.

## Search suppression best practices and use cases {#search-suppression-best-practices}

Search suppression blocks matching queries and returns the standard **Zero Results** experience. Choose the narrowest condition that meets the restriction, then follow [Create and manage search suppression rules](add.md#search-suppression-rules). A preview is not shown for search suppression rules; verify searches on the storefront after the rule becomes active.

| Use case | Suggested configuration | What to check |
| --- | --- | --- |
| Regulatory compliance for search | Scope the rule to the affected catalog view and match the restricted search terms. | Confirm the terms with your compliance team. Search suppression alone does not prevent access through categories, merchandising pages, recommendations, or direct product URLs. |
| Branding restrictions | Use **Query contains** for a restricted brand name that must be blocked within longer queries. | After the rule becomes active, check unrelated storefront queries that contain similar text to avoid suppressing legitimate searches. |
| Prevent a specific search term from returning results | Use **Query is** for an exact phrase that should return no products. | Check related phrases separately. An exact-match condition does not block every query containing that phrase. |
| Restrictions on query prefixes or suffixes | Use **Query starts with** or **Query ends with** when the location of the restricted text matters. | After the rule becomes active, check storefront queries with the text at the beginning, middle, and end to confirm the intended scope. |
| Temporary search restrictions | Set a start and end date for a time-limited restriction. | Confirm the schedule and enabled status, and review whether the rule is still needed after the restriction ends. |

- Give each rule a descriptive name and record the reason for the restriction in its description.
- Review query conditions before publishing changes. After the rule becomes active, check storefront queries that should be blocked and queries that should still return products. Cached query results can take up to 15 minutes to refresh.
- Review the storefront's Zero Results experience so shoppers have a useful path to continue browsing.
- Do not use query suppression as a substitute for product-level exclusions. To exclude products across search results, search suggestions, and autocomplete, use manual exclusions or **Attribute Based Merchandising Events** with a **Hide** action in the **default search rule**.
- Review active suppression rules regularly. Disable rules that are no longer needed, or edit and publish them when restrictions change.
