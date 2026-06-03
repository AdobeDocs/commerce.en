---
title: Search matching and ranking
description: Learn how [!DNL Adobe Commerce Optimizer] prioritizes exact and near matches, same-field matches, and cross-field matches, and how ranking interacts with search weights, intelligent ranking, and merchandising rules.
role: Admin, Leader, User
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
hide: true
---
# Search matching and ranking

>[!IMPORTANT]
>
>The following feature is in [private beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta).

[!DNL Adobe Commerce Optimizer] ranks results so shoppers see the most relevant products first. The service gives the strongest boost to products whose catalog text **closely matches** what the shopper types, then favors matches where query terms appear together in meaningful ways, and finally includes broader matches (including behavior that supports autocomplete-style matching).

## How matches are prioritized

At a high level, relevance uses three layers of matching strength (in addition to other scoring factors described below):

1. **Exact and near phrase match** — The full search phrase matches catalog text, or a **near** match after normalization such as stemming (for example, singular and plural forms resolve to the same root). These matches receive the **highest** relevance boost.

1. **All words in the same field** — Every word in the query appears in **one** searchable attribute (for example, both `red` and `pants` in the product **name**). This layer receives the **next** highest boost.

1. **Words across different fields** — Query terms appear in **different** searchable attributes (for example, `red` in **color** and `pants` in **name**). This is the broadest match behavior and aligns with how [!DNL Adobe Commerce Optimizer] can surface useful alternatives, including partial matches that support **autocomplete** (for example, a query prefix matching products that contain `red` and another token such as in `pentagon`). See [Decompounding (German)](#decompounding-german) for how German compound words behave at this layer only.

### Example

For a query like `red pants`:

- Products with **red pants** (or a stemmed near variant) in catalog text rank **first**.
- Next are products where **red** and **pants** both appear in the **same** field (for example, both in **name**).
- Then products where **red** and **pants** sit in **different** fields (for example, **color** and **name**).

### Decompounding (German) {#decompounding-german}

**Decompounding applies only to the words across different fields layer.** Exact and near phrase matching and same-field matching use the rules described above without decompounding.

German catalogs use many compound words. For example, **spülbecken** can decompose into tokens such as **spul** and **beck** (after stemming) so a shopper who searches **spul beck** can still find **Spülbecken**. At this cross-field layer, **all** decompounded tokens from the query must be present in the product data, but the tokens do **not** need to appear together or in the same attribute—the same behavior as **red** in **color** and **pants** in **name**.

This **AND** requirement filters irrelevant matches where only one subword is present. For example, a search for **Brauseschlauch** no longer returns **Schlauchstück** when only part of the compound matches. A search for **spülbecken** can still match **spülbeckventil** because the longer word contains all expected tokens.

Set **Language** to **German** on the [Language](./settings.md#language) tab in [Settings](./settings.md) so decompounding rules apply. Validate high-value German queries on a staging storefront before you enable changes in production.

Decompounding is rule-based and can add edge cases at this layer. If a subword is missing from the dictionary, tokenization can be incomplete and return broader matches than you expect—for example, **gas** missing from **gaszähler** may emit only **zahl**, or **stat** missing from **thermostat**. The stemmer can also produce unexpected roots (for example, **schrauber** stemming to **schraub**, or **schelle** to **schell**). Adobe updates the dictionary and stemming overrides for known cases as issues are identified.

## What else affects ranking

Relevance is not determined by phrase matching alone. Several signals **interact**:

- Boost from **exact / near** phrase matching
- Boost when **all query terms** appear in the **same** field
- **Intelligent ranking** (when enabled), which blends textual relevance with behavioral signals — see [How intelligent ranking scoring works](./merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[Search weight](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)** on each attribute and other textual relevance factors (for example, how often terms occur and name or description length). In *Settings*, configure which attributes participate in keyword search and their relative **[keyword search weights](./settings.md)**.
- **[Merchandising rules](./merchandising/rules/overview.md)** such as pin, boost, and bury

Because of this interplay, a product that matches only through the **broadest** layer can sometimes rank above a product with a tighter phrase match — for example, when **search weights** or term frequency in a high-weight field outweighs a weaker phrase match elsewhere.

**Example of weight interplay:** If **red pants** appears as a phrase in **description** with **search weight = 1**, but **red** and **pants** appear separately in **name** and **color** with **search weight = 10**, the product with the phrase in **description** might **not** outrank the split match, depending on the full score.

Manual **pin** and **bury** rules are designed to remain strong; **boost** rules may need tuning if you rely on them to overcome the new phrase and same-field boosts. Validate important queries after you change weights or rules.

### Search weight 1 and combined indexing

Attributes configured with the **minimum search weight** (weight **1**) and **not** configured for special match modes (such as contains or starts-with) may be combined in the search index into a single internal field (`defaultSearchField`) to reduce field mapping overhead. Treat that as one searchable surface for **same-field** matching: tokens that land only in those combined low-weight fields are evaluated together rather than as separate per-attribute fields. Adobe may refine this optimization over time as matching evolves.

## Related topics

- [Settings](./settings.md)
- [Search performance](./manage-results/search-performance.md)
- [Merchandising rules overview](./merchandising/rules/overview.md)
- [Add search rules](./merchandising/rules/add.md)
- [Synonyms overview](./merchandising/synonyms/overview.md)
