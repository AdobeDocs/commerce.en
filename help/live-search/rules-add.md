---
title: Add Rules
description: Learn how to create Search Merchandising rules.
exl-id: 7175ccf7-d838-43b0-a176-957e7db040e0
TQID: https://experienceleague.adobe.com/QnJ-q-Y-ccQ7HKEt2RgPYQFeWcBnhjwSDOtKjlF7Rp0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
---
# Add Rules

To build a rule, the first step is to use the rule editor to define the conditions in the shopper's query text that trigger the associated events. Then, complete the rule details, test the results, and publish the rule.

## Add a rule

1. In the Admin, go to **Marketing** > SEO & Search > **[!DNL Live Search]**.
1. Set the **Scope** to identify the [store view](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) where the rule applies.
1. Click the **Search Merchandising** workspace.
1. Click **Add rule** to launch the rule editor.

## Rule type

A Search query is where you define a specific search term, conditions and ranking types.

A Default rule can be set which is applied to all queries, unless a more specific search query is defined. Only one default rule can be set and it cannot contain any conditions. If you select Default, the Conditions interface is not displayed.
Choose the default Intelligent ranking type and any manual rankings you want applied to all default searches. Manual rankings are always applied.

## Conditions

Conditions are the requirements to trigger an event. A rule can have up to ten conditions and 25 events. A default rule cannot have any conditions.

   ![Rule - Build your rule](assets/rules-add-workspace.png)

>[!NOTE]
>
>Currently, it is not possible to target rules to a specific customer group.

### Single condition

1. Under *Build your rule*, select the **Condition** to be met, and follow the instructions to complete the statement.

   * Search query contains - Enter the string of text that must be in the shopper's query. The Match setting determines the degree to which the shopper's query matches the catalog. Options:<br /> Any - Any part of the shopper's query text can match the condition.<br />All - All of the shopper's query must match the condition.
   * Search query is - Enter a string of text that exactly matches the shopper's query. For example: "yoga pants". Rules with `Search query is` and Match `All` can have only one condition.
   * Search query starts with - Enter a character or string of text that must be at the beginning of the shopper's query.
   * Search query ends with - Enter a character or string of text that must be at the end of the shopper's query.

   The results appear immediately in the *Test your rule* pane and are numbered by priority. You can use the *Results per row* slider in the upper    right to change the number of products in each row.

   ![Rule - simple](assets/rule-simple-test.png)

1. To test other queries, change the query text in the *Test your rule* search box and press **Return**.
   Initially, the test pane renders the query from the Conditions search box. But now it is rendering the query from the test query box. The test pane renders only one query at a time.
1. If you like the result, update the text in the *Conditions* search box. Then, click anywhere on the page to update the results in the test pane.
1. To build a simple rule with one condition, go to Step 3: [Add events](#manual-ranking).

### Multiple conditions

1. To build a rule with multiple conditions, click **Add condition**.
   A rule can have up to ten conditions. The logical operator that joins two conditions is based on the current *Match* setting. By default, *Match* is `All` and the logical operator is `AND`.

1. Select the second condition and enter the required query text.

1. To change the logic of the rule, change the **Match** setting to determine how closely the shopper's search criteria must match the query condition. Set **Match** to one of the following:

   * Any - (Default) All logical operators in the rule are set to `OR` and the results appear in the test pane.
   * All - All logical operators in the rule are set to `AND` and the results appear in the test pane.

   The *Match* value determines the logical operator that is used to join multiple conditions. Changing the *Match* setting changes all logical operators in the rule. It is not possible to combine `AND` and `OR` in the same rule.

   In this example, rather than searching for "yoga pants", there are two separate queries that search for "yoga" or "pants". This rule is less specific and is triggered more often in the storefront than the other.

   ![Rules - Match](assets/rules-match.png)

1. To add another condition, click **Add condition** and repeat the process.

## Intelligent ranking {#intelligent-ranking}

Intelligent ranking combines user behaviors and site statistics to determine product ranking.
Store owners can set up the following types of ranking strategies:

![Rules - Match](assets/rules-ranking-type.png)

* Most purchased: This ranks products by total purchases per SKU in the previous 7 days.
* Most added to cart - Ranks in order of total "Add to Cart" activities in the previous 7 days.
* Most viewed: Ranks the total views per SKU in the previous 7 days.
* Recommended for you - Uses the `viewed-viewed` data point - Shoppers who viewed this SKU also looked at these other SKUs.
* Trending: Looks back at page view events over the past 72 hours for background events and 24 hours for foreground events.
* None: Products are ordered by Relevance.

Select the type of strategy for the rule. The **[!UICONTROL Test your rule]** window displays the expected results.

### Intelligent ranking boost {#intelligent-ranking-boost}

For **Recommended for you**, **Most viewed**, **Most purchased**, **Most added to cart**, and **Trending**, the editor shows **[!UICONTROL Intelligent Ranking Boost]** (the boost factor). It is not used when you select **None**.

Use this control to balance how strongly **behavioral signals** influence ordering relative to **textual relevance** on search, and relative to other ranking signals on **category pages** and **default listings**. The boost is available for **search query rules**, **default rules**, and **category merchandising rules**; each rule stores its own value.

| Behavior | Detail |
| --- | --- |
| Default | `5` (equivalent to the previous fixed behavioral multiplier). |
| Range | From `1` (gentler behavioral influence) through `100` (stronger influence). |
| Scope | Applies only to queries or listings that the rule targets. Other rules keep their own boost values. |
| Preview | The rule preview uses the same boost as live results for that rule. |
| Indexing | Applied at **query time**; you do not need a catalog resync or full reindex solely because you changed this setting. |

**When to raise or lower the boost**

* **Raise** the boost when strategies such as **Most viewed** should surface high-engagement SKUs more aggressively for ambiguous or broad queries, without hand-pinning every slot.
* **Lower** the boost when you want textual match quality to drive the list more strictly and behavioral data should nudge order only slightly.

**When to use manual ranking instead**

Use **pin**, **boost**, or **bury** when you need specific products in exact positions or guaranteed visibility regardless of catalog-wide signals. **[!UICONTROL Intelligent Ranking Boost]** tunes a **global** behavioral weight for that rule; it does not replace SKU-level control.

>[!NOTE]
>
> A high **[!UICONTROL Intelligent Ranking Boost]** can outweigh a **manual boost** on the same product. If a boosted SKU ranks lower than you expect in **[!UICONTROL Test your rule]** or on the storefront, lower **[!UICONTROL Intelligent Ranking Boost]** or **pin** the product to a specific position. Either change moves the manually ranked product higher in the results.

### How intelligent ranking scoring works (search)

For **search rules** (and the test query in the rule editor), intelligent ranking determines the final product order by combining two key factors: **textual relevance** and **behavioral signals**. Understanding how these factors interact helps you set realistic expectations for your search results.

**Scoring components:**

* **Textual relevance**: The dominant factor in scoring. This measures how well a product's name, description, and attributes match the search query. The text relevance score is unbounded (has no specific upper limit) and is influenced by factors like:

   * Frequency of occurrence of matching words.
   * Length (in words) of product names/descriptions.

* **Behavioral signals**: A bounded boost applied on top of the text relevance score. When you select an intelligent ranking strategy like "Most viewed" or "Most purchased," products with higher behavioral signals receive a larger relative weight. The strength of that weight is controlled by **[!UICONTROL Intelligent Ranking Boost]** (see [Intelligent ranking boost](#intelligent-ranking-boost)); the boost remains bounded, but you can increase how much it shifts ordering.

**Why the most viewed product might not appear first:**

Textual relevance often dominates ranking because its score is unbounded, while behavioral influence is capped by the boost model. Products with very strong text matches can still outrank SKUs with higher engagement unless you increase **[!UICONTROL Intelligent Ranking Boost]** for that rule. Even at higher boost values, an extreme text relevance gap may not fully invert the list, as text match quality remains a primary driver. Always validate results in **[!UICONTROL Test your rule]** for your target queries.

**Example:**

A merchant uses the "Most viewed" intelligent ranking strategy and searches for **candle**. They expect product SKU YAN-K-E-512 to appear at the top of results because it has the highest view count. However, other products rank higher:

* **Texas Candle** (1st position): Has a shorter, cleaner product name that creates a very high text relevance score. Even though it has fewer views than **YAN-K-E-512**, its superior text match outweighs the behavioral boost.

* **YAN-K-E-512** (lower position): Despite having the highest view percentile in the "Most viewed" behavioral data, its complex SKU-based name generates a lower text relevance score. At the default **[!UICONTROL Intelligent Ranking Boost]** (`5`), behavioral influence may not be enough to overcome that text gap. Increasing the boost can move **YAN-K-E-512** higher among products that already match the query. **YAN-K-E-512** must also match the query: at least one searchable attribute for that SKU must include **candle**, or it will not appear in results and the boost cannot apply.

**Example (broad query):**

For a query such as **wood**, several products can share similar textual relevance while view counts differ. With **Most viewed** selected, increasing **[!UICONTROL Intelligent Ranking Boost]** makes the historically most-viewed relevant SKU more likely to surface above lighter matches. Lowering the boost keeps results closer to pure textual ordering.

See [search rules](./best-practice.md#search-rules) to learn how to improve product findability using rules.

### Caveats

* Apostrophes and quotes in queries may lead to some minor issues with ranking and relevance in some languages.
* To ensure the intelligent ranking works correctly, make sure that the **Search Weight** for any product attributes that are used for search or filtering (facets) is `5` or less. To find this setting in the [!DNL Commerce] Admin:

   1. Select **Stores** > _Attributes_ > **Product**.
   1. Search for the attribute, such as "name".
   1. In the **Attribute Information** > **Storefront Properties** page, set the search weight to be less than or equal to `5`.

      ![Product - Search Weight](assets/set-search-weight.png)

>[!NOTE]
>
>The storefront search experience is affected by multiple configurations working together, such as facets, synonyms, and search / category merchandising rules, which can lead to results that differ from those seen when testing individual configurations in the Admin. While Admin testing isolates specific configuration areas, the storefront applies all relevant configurations together, resulting in a more complex and realistic search output.

## Manual ranking

Manual Ranking (formerly referred to as Events) are actions that modify the search results when defined conditions are met. A single rule can have up to 25 events.

* Boost - Moves a product higher in the search results.
* Bury - Moves a SKU lower in the search results.
* Pin a product - Product is displayed in the selected "Position" on the page.
* Hide a product - Excludes a SKU from the search results.

The easiest way to pin a product is by drag and drop.

1. Click and drag a product in the Test pane. Drag and drop it at the desired position. The Product and Position fields are automatically populated in the Events pane.

   ![Rules - Match](assets/rule-event-pin-product.png)

You may also click the pin icon to pin a product to its current location. Use the ellipsis context menu to "Pin to top" or "Pin to bottom".

>[!NOTE]
>
>You can only pin products that are returned in the query.

Or events can be set manually:

1. Under *Events*, choose the **Event** to take place when the associated conditions are met.

   For example, choose `Hide a product`. Then, enter the name of the product that you want to hide. Products are suggested as you type.

1. For multiple events, choose any other events that you want to trigger when conditions are met.

## Additional details

The information that is entered here appears in the [Rule Details](rules-workspace.md) panel.

1. Under *Details*, enter a **Name** for the rule. All rule names must be unique.
1. Enter a brief **Description** of the rule.
1. Enter the **Start Date** and **End Date** for the rule to be active or choose the dates from the calendar.

   To select a range of dates, click the first date and drag to select the range.

   ![Rule - Complete](assets/rule-add-details.png)

## Finalizing the rule

1. Examine the results of the rule in the test pane.
1. If the rule has multiple queries, test each one that might be affected by the rule.
1. When complete, click **Save and publish**.

   The rule is added to the list in the *Rules* workspace.

   >[!IMPORTANT]
   >
   >If the **[!UICONTROL Save and publish]** button is greyed out, make sure you have entered all required information for the rule, including the rule name.

1. Although active rules go into effect immediately, you might have to wait up to 15 minutes for the cached query results in the storefront to be refreshed.

>[!NOTE]
>
>Rules and manually ranked products are applied to the search results when the default sort order, "Sort by: Most Relevant," is selected. If a shopper changes the sort order to something like sort by name or price, rules and manual rankings are no longer in effect.

## Field descriptions

### Conditions (if)

| Condition | Description |
|--- |--- |
| Search query contains | A character or string of text that is included in the shopper's query. The shopper's query needs to match only a single character to meet this condition. |
| Search query is | A character or string of text that exactly matches the shopper's query. Complex queries with multiple conditions cannot be composed when this condition is used. |
| Search query starts with | The shopper's query begins with this character or string of text. |
| Search query ends with | The shopper's query ends with this character or string of text. |

### Logical operators

| Operator | Description |
|--- |--- |
| OR | (Default) The logical operator `OR` compares two conditions and meets the requirements to trigger an event if at least one condition is true. |
| AND | The logical operator `AND` compares two conditions and meets the requirements to trigger an event if both conditions are true. |

### Match operators

| Operator | Description |
|--- |--- |
| Any | Changes all logical operators in the rule to `OR` and returns the set of matching products. |
| All | Changes all logical operators in the rule to `AND` and returns the set of matching products. |

### Manual ranking

|Event |Description |
|--- |--- |
| Boost | Moves a SKU or range of SKUs higher in the search results. Each is marked with a "boosted" preview badge in the test search results. |
| Bury | Moves a SKU or range of SKUs lower in the search results. Each is marked with a "buried" preview badge in the test search results. |
| Pin a product | Attaches a single SKU to a specific position in the search results. The product is marked with a "pinned" preview badge in the test search results. |
| Hide a product | Excludes a SKU, or range of SKUs, from the search results. |

### Details

|Field |Description |
|--- |--- |
| Name | The name of the rule. Rule names must be unique. |
| Rule Type | Default or Query. Default is applied to all rules, unless a more specific Query rule is defined.|
| Start date | The start date of the rule, if scheduled. |
| End date | The end date of the rule, if scheduled. |
| Description | A brief description of the rule. |

### Intelligent ranking controls

| Field | Description |
| --- | --- |
| [!UICONTROL Intelligent Ranking Boost] | When an intelligent strategy other than **None** is selected, this setting controls how strongly behavioral signals influence ranking for that rule. Default `5`; allowed range `1`–`100`. Applied at query time; rule preview matches live behavior for the configured rule. |
