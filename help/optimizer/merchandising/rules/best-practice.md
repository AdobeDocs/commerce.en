---
title: Merchandising Rules Best Practices
description: Learn the best practices for implementing merchandising rules for search, default listings, and category pages.
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

To optimize conversion and revenue, implement effective **search rules**, a strong **default listing** rule, and **[category rules](add.md#rule-types)** (beta). Adjust rankings using sales data, stock, promotions, and [intelligent ranking](add.md#intelligent-ranking).

It is crucial to establish a well thought out **default rule**. Your [default rule](overview.md#default-rule) determines how search results are initially sorted when no more specific search rule applies, which improves discovery and purchase likelihood. Review it regularly so it keeps pace with shopper needs and campaigns.

## Tips to optimize search rules

- Pin or boost products with high sales volumes or recent sales activity.
- Prioritize products with high ratings and positive reviews.
- Ensure that in-stock items are ranked higher.
- Slightly prioritize products with higher profit margins without compromising relevance.
- Highlight products that are on sale or part of special promotions.
- Set search rules during promotion or sales periods automatically by using the date range during your promotion period.
- Tailor search results based on individual shopper behavior using [intelligent ranking](add.md#intelligent-ranking), such as "recommended for you", "most viewed" and so on.
- Always use the "Test your rule" panel to preview how your intelligent ranking strategy affects actual search results for different queries.

## Tips for category rules

>[!IMPORTANT]
>
>Category rules are in beta.

- Use [category rules](add.md#rule-types) on high-traffic or high-margin **category pages** where curated order matters as much as search—for example, seasonal collections or featured departments.
- Align **intelligent ranking** (for example, trending, most viewed) with how shoppers browse that category; category pages do not use search query text the way search rules do. See [Intelligent ranking](add.md#intelligent-ranking).
- Apply **pin**, **boost**, and **bury** consistently with your campaign plan; remember that manual positions usually apply only when the shopper uses the **default sort** for the listing. See [Manual ranking](add.md#manual-ranking).
- Preview in the **category** rule flow in the editor and validate on the storefront after publish, the same discipline you use for the "Test your rule" panel on search.
