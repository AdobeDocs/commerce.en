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

1. **Words across different fields** — Query terms appear in **different** searchable attributes (for example, `red` in **color** and `pants` in **name**). This is the broadest match behavior and aligns with how [!DNL Adobe Commerce Optimizer] can surface useful alternatives, including partial matches that support **autocomplete** (for example, a query prefix matching products that contain `red` and another token such as in `pentagon`).

### Example

For a query like `red pants`:

- Products with **red pants** (or a stemmed near variant) in catalog text rank **first**.
- Next are products where **red** and **pants** both appear in the **same** field (for example, both in **name**).
- Then products where **red** and **pants** sit in **different** fields (for example, **color** and **name**).

## Decompounding (German) {#decompounding-german}

German catalogs use many **compound words**—single terms built from multiple subwords. Without decompounding, a shopper who searches **spul beck** might not find **Spülbecken** because the index stores only the full compound form.

[!DNL Adobe Commerce Optimizer] uses a hyphenation-based decompounder and stemming rules for German. For example, **spülbecken** can decompose into tokens such as **spul** and **beck**. That lets shoppers find products whether they type the compound word or its parts.

### How matching works

When a shopper searches for a compound term, [!DNL Adobe Commerce Optimizer] requires **all** decompounded tokens from the query to be present in the product data. This **AND** behavior filters out irrelevant matches where only one subword is present. For example, a search for **Brauseschlauch** no longer returns **Schlauchstück** when only part of the compound matches.

Decompounded tokens do **not** need to appear together as a phrase or in the same attribute. This extends the cross-field behavior described above:

- A search for **red pants** can match a product with **red** in **color** and **pants** in **name**.
- A search for **spülbecken** can still match **spülbeckventil** because the longer word contains all expected tokens.

### Exact and near match boosting

The same three-layer prioritization applies to German queries, with these nuances:

1. **Exact and near phrase match (highest boost)** — The search phrase matches catalog text when **word order** is preserved. For example, **tool box** matches **set of 8 tool box** but not **box with a set of 8 tools** when word position is considered. Stemming applies, so singular and plural forms can count as near matches. **Schlauchbox** and **Schlauchboxen** are near matches; **Schlauch box** or **Schlauch boxen** are not exact matches for **Schlauchboxen**. **spülbeckventil** is not treated as an exact match for **spülbeck** even though it contains the expected tokens.

1. **All tokens in the same field (next boost)** — Every decompounded token appears in one searchable attribute, but not necessarily in order. **box with a set of 8 tools** can match **tool box** at this layer.

1. **Tokens across different fields (lowest boost)** — Decompounded tokens appear in different searchable attributes, with little or no phrase boost.

### Before you enable

- Set **Language** to **German** on the [Language](./settings.md#language) tab in [Settings](./settings.md) so decompounding and stemming rules apply to the index.
- Validate high-value German queries on a **staging** storefront before you enable changes in production.
- Confirm which store views use German so you apply the correct catalog language.

### Limitations and edge cases

**Missing dictionary subwords** — If a subword is missing from the decompounding dictionary, tokenization can be incomplete and return broader matches than you expect. For example, if **gas** is missing from **gaszähler**, only **zahl** might be emitted, so any product containing **zahl** could match. Similarly, **stat** may be missing for **thermostat**. Adobe updates the dictionary as missing subwords are identified.

**Incorrect stemming** — The stemmer is rule-based and can produce unexpected roots. For example, **schrauber** (screwdriver) may stem to **schraub** (screw), and **schelle** (clamp) may stem to **schell** (a proper noun in some catalogs). Adobe overrides stemming for known cases, but other issues may remain.

**Ranking interactions** — [Intelligent ranking](./merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search) strategies (for example, most purchased or most viewed) can rank an exact match lower than a broader match when behavioral signals outweigh phrase boosts. Sorting by attributes such as **price** does not boost exact or near matches. A high term frequency in the same field can sometimes outscore a tighter phrase match even with the new boosts.

**Combined low-weight fields** — Attributes with **search weight = 1** may be indexed together in `defaultSearchField`, so they behave as one searchable surface for same-field matching. See [Search weight 1 and combined indexing](#search-weight-1-and-combined-indexing).

### Autocomplete behavior

Prefix tokens are generated during indexing to support autocomplete-style retrieval (for example, **pan**, **pant**, and **pants** for **pants**). Autocomplete tokens are used for retrieval, not for exact-match boosting.

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

### Search weight 1 and combined indexing {#search-weight-1-and-combined-indexing}

Attributes configured with the **minimum search weight** (weight **1**) and **not** configured for special match modes (such as contains or starts-with) may be combined in the search index into a single internal field (`defaultSearchField`) to reduce field mapping overhead. Treat that as one searchable surface for **same-field** matching: tokens that land only in those combined low-weight fields are evaluated together rather than as separate per-attribute fields. Adobe may refine this optimization over time as matching evolves.

## Related topics

- [Settings](./settings.md)
- [Search performance](./manage-results/search-performance.md)
- [Merchandising rules overview](./merchandising/rules/overview.md)
- [Add search rules](./merchandising/rules/add.md)
- [Synonyms overview](./merchandising/synonyms/overview.md)
