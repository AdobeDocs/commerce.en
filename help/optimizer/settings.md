---
title: Settings
description: Configure settings for [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
---
# Settings

Use the *Settings* workspace to configure search and product discovery for your storefront. The following tabs are available:

- **Price facets** — Configure price range groups and intervals used as search filters.
- **Language** — Set the catalog language used for indexing and search.
- **Semantic search** — Enable and configure AI-powered semantic search (attributes, priority, and related options).
- **Advanced search** — Tune semantic ranking boost, similarity cutoffs, and optional fuzzy fallback when direct search returns no matches.

>[!BEGINTABS]

>[!TAB Price facets]

## Price facets {#price-facets}

You can specify the number of price range groups and how price values are distributed among them. Each price range overlaps the previous group by one. For example, when you use five groups with an interval of 20, you get price ranges such as 0-20, 20-40, 40-60, 60-80, and >80. If there are not enough products in the catalog to fill all defined ranges, the display of the available groups is adjusted accordingly. For example: 0-20, 60-80, >80.

**To configure price facets:**

1. On the **Settings** workspace, select **[!UICONTROL Facets]**.
1. In the **Price facet** section, do the following:
   - Enter the **[!UICONTROL Number of selections]**, or price groupings to be available. Up to 100 price groupings can be defined.
   - Enter the **[!UICONTROL Interval value]**, or price range for each group. The maximum value is 40,000,000.
1. Click **[!UICONTROL Save]**.

   It takes about 15 minutes for the updated settings to be available in the storefront.

### Field descriptions

| Field | Description |
| --- | --- |
| Number of selections | Specifies the number of price range groupings that can be used as search filters in the storefront. Default value: 8, Maximum value: 100 |
| Interval value | Specifies the price range interval for each group. For example, five selections with an interval value of 20 yield groupings of 0-20, 20-40, 40-60, 60-80, and >80. Default value: 5, Maximum value: 40,000,000 |

>[!TAB Language]

## Language {#language}

The Language setting tells [!DNL Adobe Commerce Optimizer] which language to expect when reading the catalog and writing the index.

Languages have different sets of rules for grammar: how words are separated, verb tenses and word forms, for example.
The Language setting ensures that the correct set of rules is applied to the indexing mechanism.

Set the Language setting to the primary language of the catalog. When you change the language of the index, it can take from 5 to 60 minutes for the change to appear on the storefront, depending on the size and complexity of the catalog.

|Language|Code|
|----|----|
|Arabic|ar|
|Armenian|hy|
|Basque|eu|
|Bengali|bn|
|Brazilian|pt-br|
|Bulgarian|bg|
|Catalan|ca|
|Chinese (Simplified)|zh-cn|
|Chinese (Traditional)|zh-tw|
|Czech|cs|
|Danish|da|
|Dutch|nl|
|English|en|
|Estonian|et|
|Finnish|fi|
|French|fr|
|Galician|gl|
|German|de|
|Greek|el|
|Hindi|hi|
|Hungarian|hu|
|Indonesian|id|
|Irish|ga|
|Italian|it|
|Japanese (Katakana)|ja|
|Korean|ko|
|Latvian|lv|
|Lithuanian|lt|
|Norwegian|no|
|Persian|fa|
|Portuguese|pt|
|Romanian|ro|
|Russian|ru|
|Sorani|ku|
|Spanish|es|
|Swedish|sv|
|Turkish|tr|
|Thai|th|

>[!TAB Semantic search]

## Semantic search {#semantic-search}

Semantic search uses AI to interpret queries by meaning and intent, not only exact keywords, so shoppers who use natural language or wording that does not match your catalog verbatim can still find relevant products. On the **[!UICONTROL Semantic search]** tab, you choose which product attributes participate in semantic search, set their **[!UICONTROL Priority]**, and **[!UICONTROL Publish]** when you are ready. For benefits, detailed steps, recommended attributes, performance considerations, limitations, and troubleshooting, see [Semantic search](setup/semantic-search.md).

>[!TAB Advanced search]

## Advanced search {#advanced-search}

Use the **[!UICONTROL Advanced search]** tab to adjust how strongly semantic matches influence ranking, how strict semantic matching must be, and whether fuzzy matching runs when direct search finds no results.

![Advanced search settings](./assets/advanced-search.png)

**To configure advanced search:**

1. On the **Settings** workspace, select the **[!UICONTROL Advanced search]** tab.
1. Under **Semantic search boost**, adjust the **[!UICONTROL Semantic boost]** slider. This control applies a boost to prioritize semantically relevant results.
1. Under **Similarity threshold**, adjust the **[!UICONTROL Similarity threshold]** slider. This control applies a percentage to set the minimum semantic match score required for results to appear.

   A higher threshold keeps only stronger semantic matches visible and can reduce noise from weak matches. A lower threshold allows more products through when semantic confidence is borderline.

1. Under **Fuzzy search**, for **Use fuzzy search as a fallback when no direct search results are found?**, select **[!UICONTROL Yes]** or **[!UICONTROL No]**. Fuzzy search finds near matches for queries, which helps with typos and minor variations.

   If you select **[!UICONTROL Yes]**, adjust the **[!UICONTROL Fuzzy search similarity threshold]** slider to set the minimum similarity (as a percentage) required for fuzzy-matched products to appear.

   Lower fuzzy thresholds return more approximate matches (helpful for difficult spellings) but can surface less relevant products. Raise the threshold if fuzzy results feel too broad.

1. Click **[!UICONTROL Save]**.

### Field descriptions

| Control | Description |
| --- | --- |
| Semantic boost | A boost applied to prioritize semantically relevant results in ranking. |
| Similarity threshold | Percentage that sets the minimum semantic match score required for a product to appear in results. |
| Use fuzzy search as a fallback when no direct search results are found? | **Yes** enables fuzzy search only when direct (for example, keyword) search does not return results. **No** disables that fallback. |
| Fuzzy search similarity threshold | When fuzzy fallback is **Yes**, the minimum similarity (percentage) fuzzy matches must meet to be shown. |

>[!ENDTABS]
