---
title: Semantic Search
description: Enable AI semantic search for [!DNL Live Search] from Settings. No attribute setup or storefront changes required.
role: Admin
recommendations: noCatalog
---
# Semantic search

Semantic search uses AI to understand what shoppers mean, not just the exact words they type. Queries such as "dress for a beach wedding" or "comfortable shoes for standing all day" can return relevant products even when your catalog does not use those exact phrases.

[!DNL Live Search] combines keyword matching and semantic matching in one search experience. You do not manage separate keyword and semantic modes on the storefront. In the Admin, go to the [Settings](settings.md#semantic-search) workspace and turn semantic search on with a single toggle. [!DNL Live Search] does not offer advanced semantic controls (for example, boost or similarity sliders) in the Admin. Enablement is on or off.

## Benefits

- **Fewer zero-result searches** — Shoppers find products when their wording does not match catalog text exactly.
- **More relevant results** — Natural, descriptive queries return useful matches based on meaning and context.
- **Less synonym maintenance** — Common word variations (for example, couch and sofa) are often handled without manual synonym lists.
- **No storefront or developer work** — Enable the feature in Settings. You do not change theme code, widgets, or APIs to turn it on.

## How it works

When semantic search is enabled, [!DNL Live Search] uses predefined catalog attributes chosen by the system (such as product name and description) to interpret query meaning alongside traditional keyword search. You do not select or prioritize attributes in the Admin.

For example:

- A search for "leather couch" can return products labeled "leather sofa."
- "Spring dress" can surface seasonal dresses even when "spring" is not in the product name.
- "Shoes for trail running" can match products described as off-road or hiking footwear.

## Enable semantic search

1. In the Admin, go to **Marketing** > *SEO & Search* > **[!DNL Live Search]**.
1. On the **Settings** workspace, turn **[!UICONTROL Semantic search]** **on**.

   When enabled, search matches products based on meaning and context, which can produce more relevant results, fewer zero-result searches, and improved conversion.

1. Click **[!UICONTROL Save]**.

   Search results update after indexing completes. For a medium-sized catalog, indexing can take up to half an hour. For large catalogs with millions of products, it can take a few hours.

>[!NOTE]
>
> Semantic search is available for **English** catalogs only. If you change **Language** to a non-English catalog on the **Settings** workspace, **[!UICONTROL Semantic search]** is turned off automatically.

You do not need a separate publish step or storefront configuration after you save.

## Best practices

- Use clear, descriptive product names and descriptions so both keyword and semantic matching have strong catalog text to work with.
- Review zero-result queries on the [Performance](performance.md) workspace after you enable semantic search.
- Keep brand-specific or highly technical [synonyms](synonyms.md) where semantic search may not cover specialized terms.

## Troubleshooting

| Issue | What to do |
| --- | --- |
| No change on the storefront right after saving | Wait for indexing to finish. Large catalogs can take longer. |
| Semantic search is unavailable or turns off | Confirm **Language** on the **Settings** workspace is set to **English**. |
| Results still miss common terms | Add [synonyms](synonyms.md) for brand or industry terms semantic search may not resolve. |

## Limitations {#semantic-search-limitations}

- **Catalog language:** Semantic search is available only for **English**-language catalogs.
- **Admin controls:** [!DNL Live Search] provides an on/off toggle only. You cannot tune semantic boost, similarity threshold, or fuzzy search from the **Settings** workspace.

## More help on this topic

- [Settings](settings.md#semantic-search)
- [Synonyms](synonyms.md)
- [Performance](performance.md)
