---
title: Semantic Search
description: Enable AI semantic search in [!DNL Adobe Commerce Optimizer] from Settings. No attribute setup or storefront changes required.
role: Admin, User
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
---
# Semantic search

Semantic search uses AI to understand what shoppers mean, not just the exact words they type. Queries such as "dress for a beach wedding" or "comfortable shoes for standing all day" can return relevant products even when your catalog does not use those exact phrases.

[!DNL Adobe Commerce Optimizer] combines keyword matching and semantic matching in one search experience. You do not manage separate keyword and semantic modes on the storefront. In the Admin, turn semantic search on from **[Settings](../settings.md#advanced-search)** and optionally tune advanced controls on the same tab.

## Benefits

- **Fewer empty search pages** — Shoppers find products when their wording does not match catalog text exactly.
- **Better intent matching** — Natural, descriptive queries return useful results.
- **Less synonym maintenance** — Common word variations (for example, couch and sofa) are often handled without manual synonym lists.
- **No storefront or developer work** — Enable the feature in Settings; you do not change theme code, drop-ins, or APIs to turn it on.

## How it works

When semantic search is enabled, [!DNL Adobe Commerce Optimizer] uses predefined catalog attributes chosen by the system (such as product name and description) to interpret query meaning alongside traditional keyword search. You do not select or prioritize attributes in the Admin.

For example:

- A search for "leather couch" can return products labeled "leather sofa."
- "Spring dress" can surface seasonal dresses even when "spring" is not in the product name.
- "Shoes for trail running" can match products described as off-road or hiking footwear.

## Enable semantic search

1. On the **[!UICONTROL Settings]** workspace, open the **[!UICONTROL Advanced search]** tab.
1. Turn **[!UICONTROL Enable semantic search]** **on**.
1. Click **[!UICONTROL Save]**.

Search results update after indexing completes. Depending on catalog size, this can take up to half an hour for a medium size catalog and up to a few hours for large catalogs with millions of products.

>[!NOTE]
>
> Semantic search is available for **English** catalogs only. If you change **[!UICONTROL Language]** to a non-English catalog, **[!UICONTROL Enable semantic search]** is turned off automatically.

You do not need to publish a separate configuration or change storefront settings after you save.

## Optional tuning

On the **[!UICONTROL Advanced search]** tab, you can adjust how search behaves after semantic search is enabled:

- **[!UICONTROL Semantic boost]** — Increase or decrease how strongly meaning-based matches influence ranking.
- **[!UICONTROL Similarity threshold]** — Set how close a match must be before a product appears. Lower values show more results; higher values show fewer, tighter matches.
- **[!UICONTROL Fuzzy search]** and **[!UICONTROL Fuzzy search similarity threshold]** — Help shoppers find products when queries include typos or small spelling differences.

See [Advanced search](../settings.md#advanced-search) for control descriptions and step-by-step guidance.

## Best practices

- Use clear, descriptive product names and descriptions so both keyword and semantic matching have strong catalog text to work with.
- Review zero-result and low-conversion queries in search performance reports after you enable semantic search.
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
