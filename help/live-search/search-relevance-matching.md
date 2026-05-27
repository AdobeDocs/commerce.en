---
title: Search matching and ranking
description: Learn how [!DNL Live Search] prioritizes exact and near matches, same-field matches, and cross-field matches, and how ranking interacts with search weights, intelligent ranking, and merchandising rules.
role: Admin, Developer
recommendations: noCatalog
---
# Search matching and ranking

>[!IMPORTANT]
>
>The following feature is in [private beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta#search-matching-and-ranking-private-beta).

[!DNL Live Search] ranks results so shoppers see the most relevant products first. The service gives the strongest boost to products whose catalog text **closely matches** what the shopper types, then favors matches where query terms appear together in meaningful ways, and finally includes broader matches (including behavior that supports autocomplete-style matching).

## How matches are prioritized

At a high level, relevance uses three layers of matching strength (in addition to other scoring factors described below):

1. **Exact and near phrase match** — The full search phrase matches catalog text, or a **near** match after normalization such as stemming (for example, singular and plural forms resolve to the same root). These matches receive the **highest** relevance boost.

1. **All words in the same field** — Every word in the query appears in **one** searchable attribute (for example, both `red` and `pants` in the product **name**). This layer receives the **next** highest boost.

1. **Words across different fields** — Query terms appear in **different** searchable attributes (for example, `red` in **color** and `pants` in **name**). This is the broadest match behavior and aligns with how [!DNL Live Search] can surface useful alternatives, including partial matches that support **autocomplete** (for example, a query prefix matching products that contain `red` and another token such as in `pentagon`).

### Example

For a query like `red pants`:

- Products with **red pants** (or a stemmed near variant) in catalog text rank **first**.
- Next are products where **red** and **pants** both appear in the **same** field (for example, both in **name**).
- Then products where **red** and **pants** sit in **different** fields (for example, **color** and **name**).

## Decompounding (German)

For languages where [!DNL Live Search] supports **decompounding** (German today), compound words can be split so related tokens match (for example, matching behavior that relates **screw driver** and **screwdriver**). The same overall prioritization idea applies, but decompounding is rule-based and can add edge cases. For example, if a subword is missing from the dictionary, tokenization can be incomplete and return broader matches than you expect. If you use German storefront content, validate high-value queries on a staging storefront.

## What else affects ranking

Relevance is not determined by phrase matching alone. Several signals **interact**:

- Boost from **exact / near** phrase matching
- Boost when **all query terms** appear in the **same** field
- **Intelligent ranking** (when enabled), which blends textual relevance with behavioral signals — see [How intelligent ranking scoring works](rules-add.md#how-intelligent-ranking-scoring-works)
- **[Search weight](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)** on each attribute and other textual relevance factors (for example, how often terms occur and name or description length). In the [!DNL Adobe Commerce] Admin, configure **Use in Search** and **Search Weight** for product attributes.
- **[Search merchandising rules](rules.md)** such as pin, boost, and bury

Because of this interplay, a product that matches only through the **broadest** layer can sometimes rank above a product with a tighter phrase match — for example, when **search weights** or term frequency in a high-weight field outweighs a weaker phrase match elsewhere.

**Example of weight interplay:** If **red pants** appears as a phrase in **description** with **search weight = 1**, but **red** and **pants** appear separately in **name** and **color** with **search weight = 10**, the product with the phrase in **description** might **not** outrank the split match, depending on the full score.

Manual **pin** and **bury** rules are designed to remain strong; **boost** rules may need tuning if you rely on them to overcome the new phrase and same-field boosts. Validate important queries after you change weights or rules.

### Search weight 1 and combined indexing

Attributes configured with the **minimum search weight** (weight **1**) and **not** configured for special match modes (such as contains or starts-with) may be combined in the search index into a single internal field (`defaultSearchField`) to reduce field mapping overhead. Treat that as one searchable surface for **same-field** matching: tokens that land only in those combined low-weight fields are evaluated together rather than as separate per-attribute fields. Adobe may refine this optimization over time as matching evolves.

## Related topics

- [Indexing](indexing.md)
- [Best practices](best-practice.md)
- [Add search rules](rules-add.md)
- [Synonyms](synonyms.md)
