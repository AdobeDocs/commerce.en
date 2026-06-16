---
title: Semantic Search
description: Enable AI semantic search for [!DNL Live Search] from Settings. No attribute setup or storefront changes required.
role: Admin
recommendations: noCatalog
---
# Semantic search

Semantic search uses AI to understand what shoppers mean, not just the exact words they type. Queries such as "dress for a beach wedding" or "comfortable shoes for standing all day" can return relevant products even when your catalog does not use those exact phrases.

[!DNL Live Search] combines keyword matching and semantic matching in one search experience. You do not manage separate keyword and semantic modes on the storefront. [!DNL Live Search] does not offer advanced semantic controls (for example, boost or similarity sliders) in the Admin. You can enable or disable semantic search.

## Enablement by deployment

Semantic search is managed from the **Settings** workspace in the [!DNL Live Search] Admin (**Marketing** > *SEO & Search* > **[!DNL Live Search]**). [!DNL Adobe Commerce as a Cloud Service] uses this same [!DNL Live Search] interface as PaaS merchants.

## Benefits

- **Fewer zero-result searches** — Shoppers find products when their wording does not match catalog text exactly.
- **More relevant results** — Natural, descriptive queries return useful matches based on meaning and context.
- **Less synonym maintenance** — Common word variations (for example, couch and sofa) are often handled without manual synonym lists.
- **No storefront or developer work** — Semantic search requires no theme code, widget, or API changes. PaaS merchants enable it in Settings; [!DNL Adobe Commerce as a Cloud Service] customers receive it enabled by default.

## How it works

When semantic search is enabled, [!DNL Live Search] uses predefined catalog attributes chosen by the system (such as product name and description) to interpret query meaning alongside traditional keyword search. You do not select or prioritize attributes in the Admin.

For example:

- A search for "leather couch" can return products labeled "leather sofa."
- "Spring dress" can surface seasonal dresses even when "spring" is not in the product name.
- "Shoes for trail running" can match products described as off-road or hiking footwear.

## What happens when you enable semantic search

Semantic search works alongside your existing [!DNL Live Search] configuration. You do not replace keyword search or reconfigure the storefront.

When semantic search is active:

- Your existing [search rules](rules.md), [synonyms](synonyms.md), [facets](facets.md), boosts, and [category merchandising](category-merch.md) settings continue to apply.
- Semantic search adds AI-powered understanding of shopper intent to improve result relevance alongside keyword matching.
- Predefined catalog attributes are indexed automatically. You do not select attributes or publish a separate configuration.

## Manage semantic search in the Admin

Go to the [Settings](settings.md#semantic-search) workspace to view or change the **[!UICONTROL Semantic search]** toggle.

>[!NOTE]
>
> Semantic search is available for **English** catalogs only. If you change **Language** to a non-English catalog on the **Settings** workspace, **[!UICONTROL Semantic search]** is disabled automatically.

### For PaaS merchants

Adobe Commerce on Cloud and on-premises merchants must enable semantic search manually:

1. In the Admin, go to **Marketing** > *SEO & Search* > **[!DNL Live Search]**.
1. On the **Settings** workspace, enable **[!UICONTROL Semantic search]**.

   When enabled, search matches products based on meaning and context, which can produce more relevant results, fewer zero-result searches, and improved conversion.

1. Click **[!UICONTROL Save]**.

   Search results update after indexing completes. For a medium-sized catalog, indexing can take up to half an hour. For large catalogs with millions of products, it can take a few hours.

### For [!DNL Adobe Commerce as a Cloud Service] customers

[!DNL Adobe Commerce as a Cloud Service] customers use the same **Settings** workspace in the [!DNL Live Search] Admin. Semantic search is **enabled by default** for eligible English catalogs. Confirm **[!UICONTROL Semantic search]** is enabled, or disable it if you do not want semantic matching on the storefront.

You do not need a separate publish step or storefront configuration after you save a change.

## Validate after enablement

After semantic search is active and indexing completes, Adobe recommends validating search performance. Use the [Performance](performance.md) workspace to review metrics and test queries that matter to your business. This applies whether semantic search was enabled by default or you enabled it manually.

1. Review your top searched terms in the **Unique searches** report.
1. Test historical zero-result queries from the **Zero results** report on the storefront.
1. Compare search results for the same queries before and after enablement.
1. Monitor search conversion and engagement metrics, including click-through rate, conversion rate, and zero results rate.

## Best practices

- Use clear, descriptive product names and descriptions (ideally 50-100 words) so both keyword and semantic matching have strong catalog text to work with.
- Keep brand-specific or highly technical [synonyms](synonyms.md) where semantic search may not cover specialized terms.

## Troubleshooting

| Issue | What to do |
| --- | --- |
| No change on the storefront right after saving | Wait for indexing to finish. Large catalogs can take longer. |
| Semantic search is unavailable or disabled automatically | Confirm **Language** on the **Settings** workspace is set to **English**. |
| Results still miss common terms | Add [synonyms](synonyms.md) for brand or industry terms semantic search may not resolve. |

## Limitations {#semantic-search-limitations}

- **Catalog language:** Semantic search is available only for **English**-language catalogs.
- **Admin controls:** [!DNL Live Search] provides an enable/disable control only. You cannot tune semantic boost, similarity threshold, or fuzzy search from the **Settings** workspace.

## More help on this topic

- [Settings](settings.md#semantic-search)
- [Synonyms](synonyms.md)
- [Performance](performance.md)
