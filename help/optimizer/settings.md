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
- **Semantic search** (beta) — Enable and configure AI-powered semantic search (attributes, priority, and related options).
- **Advanced search** (beta) — Tune semantic ranking boost, similarity cutoffs, and optional fuzzy fallback when direct search returns no matches.

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

## Semantic search (beta) {#semantic-search}

Semantic search uses AI to understand the meaning and intent behind a shopper's search query, not just exact keyword matches. This helps shoppers find relevant products even when they use natural language, synonyms, or descriptive phrases that don't exactly match your product catalog.

>[!IMPORTANT]
>
>This feature is currently in [beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta#semantic-search-smarter-context-aware-shopping-experiences-private-beta).

### Semantic search benefits

Enabling semantic search can improve your store's search performance in several key ways:

- **Reduced zero-results searches:** Shoppers find products even when they use terms that are not in your catalog.
- **Better natural language understanding:** Queries like "dress for beach wedding" or "leather recliner for media room" return relevant results.
- **Automatic synonym handling:** You do not need to manually create synonyms for similar terms like "couch/sofa" or "pants/trousers."
- **Improved conversion rates:** More relevant results lead to higher search-to-cart conversion.
- **Enhanced customer satisfaction:** Shoppers can search using natural expressions rather than guessing exact product terms.

### How semantic search works

Semantic search uses AI and natural language processing to understand the contextual meaning of search queries and match them to products based on semantic similarity rather than just text matching. For example:

- A search for "leather couch" returns products labeled as "leather sofa."
- "Spring dress" finds seasonal dresses even without the word "spring" in the catalog.
- "Shoes for trail running" surfaces products described as "off-road sneakers."
- "Brakepad" finds products listed as "brake pad" (compound word variations).

Traditional keyword search fails when shoppers add descriptive words that do not exist in your catalog. Semantic search overcomes this limitation by understanding the overall intent of the search phrase.

### Enable semantic search

In this section, you select which product attributes to use for semantic search. Learn which [attributes are recommended](#recommended-attributes-for-semantic-search) for semantic search.

>[!NOTE]
>
>Before you enable semantic search, review the [performance impact](#performance-impact) described below, especially if you have a large catalog.

![Semantic search attribute configuration](./assets/semantic-search-attributes.png)

**To enable semantic search:**

1. On the **Settings** workspace, select the **[!UICONTROL Semantic search beta]** tab.
1. In the **Semantic search attributes** section, a table lists the selected attributes (if any). To add attributes, select **[!UICONTROL Select attributes]**.

   The **Select attributes for semantic search** dialog appears.

1. Select the product attributes to include in semantic search by selecting the checkbox for each attribute, then click **[!UICONTROL Add selected]**.

   The dialog closes and the selected attributes appear in the **Semantic search attributes** table.

1. Set the **[!UICONTROL Priority]** for each attribute.

   Priority sets the order in which text from attributes are concatenated. Since the model truncates tokens beyond a certain limit, setting a priority ensures that tokens from the most important attributes are not truncated.

1. To remove an attribute from semantic search, select the minus icon on that row.
1. When you are finished setting the priority, click the **[!UICONTROL Publish]** button.

   The **Publish** button is enabled only when there are unsaved changes. After publishing, updated settings are applied to the catalog; indexing may take a few minutes to reflect on the storefront.

### Field descriptions

| Field | Description |
| --- | --- |
| Attribute label | The display name of the product attribute. |
| Attribute code | The system code for the attribute. |
| Priority | Importance of this attribute in semantic search ranking. A priority of `1` is highest; that attribute is searched first. |

### Recommended attributes for semantic search {#recommended-attributes-for-semantic-search}

Not all product attributes are appropriate for semantic search. Use semantic search for descriptive text fields like:

- Product name
- Description
- Category
- Marketing attributes (for example, style, use case, occasion)

Avoid using semantic search for:

- SKU and part numbers
- UPC/EAN codes
- Identifiers and technical codes
- Numeric-only fields
- Boolean fields such as weight, price, and so on because only attribute values are indexed
- Lengthy text attributes — Values from all semantic attributes are concatenated in **priority** order into one string used to generate vector embeddings. Text beyond the model's current effective length (about 256 tokens; longer input is truncated) may not be encoded reliably, so very long fields add little benefit. Token limits and the underlying model can change in a future release.

>[!TIP]
>
>Start with product name and description, then add additional attributes based on how your customers search.

### Performance impact {#performance-impact}

Semantic search adds AI processing to your search operations. This includes:

**Indexing**

- Incremental product updates process normally with minimal delay.
- Full reindex operations take longer (noticeable for catalogs with 10,000+ products).
- Reindexing happens in the background; your storefront continues using the current index with no downtime.

**Search speed**

- Individual search queries may take slightly longer (typically 15-20% increase in response time).
- For most stores, this difference is not noticeable to shoppers.
- Example: A query that takes 180ms may take 210ms with semantic search enabled.

### Best practices

**Optimize your product data:**

- Use clear, descriptive product names and descriptions.
- Include common use cases and occasions in product descriptions.
- Add relevant attributes that describe how products are used.
- Avoid overly technical jargon unless your audience expects it.

**Tune semantic behavior (Advanced search tab):**

- On the **[Advanced search](#advanced-search)** tab, adjust **[!UICONTROL Semantic boost]** when you want semantically relevant products to rank higher or lower relative to other matches—increase the boost if semantic matches should carry more weight in the result set, decrease it if results feel dominated by broad semantic matches.
- Use **[!UICONTROL Similarity threshold]** to control how strict semantic matching must be before products appear: a **higher** threshold keeps stronger semantic matches and can reduce noisy or weak matches; a **lower** threshold allows more borderline matches when shoppers still need options.
- Configure **[!UICONTROL Fuzzy search]** on the same tab when you want near matches (for example, typos) as a fallback when direct search returns no results, and tune **[!UICONTROL Fuzzy search similarity threshold]** so fuzzy results stay relevant.

**Monitor and measure:**

- Track your zero-results search rate before and after enabling.
- Monitor search-to-cart conversion rates.
- Review common search queries to identify gaps in your catalog data.

**Start conservatively:**

- Test with your most common search queries.

**Relationship with synonyms:**

- Semantic search reduces but does not eliminate the need for synonyms.
- Keep brand-specific or highly technical synonyms you've already created.
- Use semantic search to handle general language variations automatically.

### Troubleshooting

**Search results seem less relevant after enabling semantic search:**

1. Verify which attributes are configured for semantic search.
1. Review whether SKUs or identifiers are incorrectly included in semantic search fields.
1. Consider whether your product descriptions need improvement.
1. Increase the **[!UICONTROL Similarity threshold]** on primary and fuzzy (fallback) search. For control descriptions, see [Advanced search](#advanced-search).

**Searches for product codes return unexpected results:**

- Ensure that you do not configure SKU, part numbers, and product codes as semantic search attributes.
- Match product codes with exact keyword search instead of semantic search.

**Performance is slower than expected:**

- Large catalogs (50,000+ products) may experience more noticeable delays.
- Ensure that your catalog has completed initial indexing.

**Zero-results rate hasn't improved:**

- Review your most common zero-results queries.
- Improve product descriptions to include more natural language terms.
- Ensure that semantic search is enabled for your primary descriptive attributes.

### Limitations {#semantic-search-limitations}

Keep the following constraints in mind when you use semantic search (beta):

- **Catalog language:** Semantic search is available only for **English**-language catalogs.
- **Attribute limit:** You can assign up to **20** product attributes to semantic search.
- **Combined text and embeddings:** Attribute values are concatenated in priority order for embedding; input beyond the model's current effective length (about 256 tokens) is truncated, and token limits or the model may change in a future release. For guidance on long fields, see [Recommended attributes for semantic search](#recommended-attributes-for-semantic-search).
- **Data space cleanup:** If a **data space cleanup** runs on your project, existing semantic search attribute configuration is cleared. Reconfigure attributes using catalog ingestion or the **[!UICONTROL Semantic search beta]** tab after product metadata has resynced, and verify the configuration if it does not match what you expect after sync.

>[!TAB Advanced search]

## Advanced search (beta) {#advanced-search}

Use the **[!UICONTROL Advanced search]** tab to adjust how strongly semantic matches influence ranking, how strict semantic matching must be, and whether fuzzy matching runs when direct search finds no results.

>[!IMPORTANT]
>
>This feature is currently in [beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta#semantic-search-smarter-context-aware-shopping-experiences-private-beta).

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
