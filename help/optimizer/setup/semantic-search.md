---
title: Semantic Search
description: Enable AI semantic search in [!DNL Adobe Commerce Optimizer] from Settings. No attribute setup or storefront changes required.
role: Admin, User
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
---
# Semantic search

Semantic search uses AI to understand what shoppers mean, not just the exact words they type. Queries such as "dress for a beach wedding" or "comfortable shoes for standing all day" can return relevant products even when your catalog does not use those exact phrases.

[!DNL Adobe Commerce Optimizer] combines keyword matching and semantic matching in one search experience. You do not manage separate keyword and semantic modes on the storefront. In the Admin, go to the [Settings](../settings.md#advanced-search) workspace and turn semantic search on with a single toggle. You can optionally tune advanced controls on the same tab.

## Benefits

- **Fewer empty search pages** — Shoppers find products when their wording does not match catalog text exactly.
- **Better intent matching** — Natural, descriptive queries return useful results.
- **Less synonym maintenance** — Common word variations (for example, couch and sofa) are often handled without manual synonym lists.
- **No storefront or developer work** — Enable the feature in Settings. You do not change theme code, drop-ins, or APIs to turn it on.

## How it works

When semantic search is enabled, [!DNL Adobe Commerce Optimizer] uses predefined catalog attributes chosen by the system (such as product name and description) to interpret query meaning alongside traditional keyword search. You do not select or prioritize attributes in the Admin.

For example:

- A search for "leather couch" can return products labeled "leather sofa."
- "Spring dress" can surface seasonal dresses even when "spring" is not in the product name.
- "Shoes for trail running" can match products described as off-road or hiking footwear.

## What happens when you enable semantic search

Semantic search works alongside your existing [!DNL Adobe Commerce Optimizer] search configuration. You do not replace keyword search or reconfigure the storefront.

When you turn semantic search on:

- Your existing [merchandising rules](../merchandising/rules/overview.md), [synonyms](../merchandising/synonyms/overview.md), [facets](../merchandising/facets/overview.md), boosts, and filters continue to apply.
- Semantic search adds AI-powered understanding of shopper intent to improve result relevance alongside keyword matching.
- Predefined catalog attributes are indexed automatically. You do not select attributes or publish a separate configuration.

## Enable semantic search

1. In the Admin, go to **[!UICONTROL Settings]**.
1. On the **[!UICONTROL Advanced search]** tab, turn **[!UICONTROL Enable semantic search]** **on**.
1. Click **[!UICONTROL Save]**.

Search results update after indexing completes. For a medium-sized catalog, indexing can take up to half an hour. For large catalogs with millions of products, it can take a few hours.

>[!NOTE]
>
> Semantic search is available for **English** catalogs only. If you change **[!UICONTROL Language]** to a non-English catalog, **[!UICONTROL Enable semantic search]** is turned off automatically.

You do not need to publish a separate configuration or change storefront settings after you save.

## Validate after enablement

After indexing completes, Adobe recommends validating search performance before and after you enable semantic search. Use the [Search performance](../manage-results/search-performance.md) page to review metrics and test queries that matter to your business.

1. Review your top searched terms in the **Unique searches** report.
1. Test historical zero-result queries from the **Zero results** report on the storefront.
1. Compare search results for the same queries before and after enablement.
1. Monitor search conversion and engagement metrics, including click-through rate, conversion rate, and zero results rate.

## Optional tuning

On the **[!UICONTROL Advanced search]** tab, you can adjust how search behaves after semantic search is enabled:

- **[!UICONTROL Semantic boost]** — Increase or decrease how strongly meaning-based matches influence ranking.
- **[!UICONTROL Similarity threshold]** — Set how close a match must be before a product appears. Lower values show more results; higher values show fewer, tighter matches.
- **[!UICONTROL Fuzzy search]** and **[!UICONTROL Fuzzy search similarity threshold]** — Help shoppers find products when queries include typos or small spelling differences.

See [Advanced search](../settings.md#advanced-search) for control descriptions and step-by-step guidance.

## Best practices

- Use clear, descriptive product names and descriptions so both keyword and semantic matching have strong catalog text to work with.
- Start with the default **[!UICONTROL Enable semantic search]** setting, then adjust **[!UICONTROL Semantic boost]** or **[!UICONTROL Similarity threshold]** only if results feel too broad or too narrow.
- Keep brand-specific or highly technical [synonyms](../merchandising/synonyms/overview.md) where semantic search may not cover specialized terms.

## Troubleshooting

| Issue | What to do |
| --- | --- |
| No change on the storefront right after saving | Wait for indexing to finish. Large catalogs can take longer. |
| Results feel too broad | Raise **[!UICONTROL Similarity threshold]** or lower **[!UICONTROL Semantic boost]** on the **[!UICONTROL Advanced search]** tab. |
| Results feel too narrow | Lower **[!UICONTROL Similarity threshold]** or raise **[!UICONTROL Semantic boost]**. |
| Typos still return no results | Turn **[!UICONTROL Fuzzy search]** **on** and tune **[!UICONTROL Fuzzy search similarity threshold]**. |
| Semantic search is unavailable | Confirm **[!UICONTROL Language]** is set to **English**. |

## Limitations {#semantic-search-limitations}

- **Catalog language:** Semantic search is available only for **English**-language catalogs.

## More help on this topic

- [Advanced search](../settings.md#advanced-search)
- [Synonyms](../merchandising/synonyms/overview.md)
- [Search performance](../manage-results/search-performance.md)
