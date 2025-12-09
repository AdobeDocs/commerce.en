---
title: Create and Manage Rules
description: Learn how to create and manage merchandising rules.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: fd4df2b2-83de-4c5c-b18c-e97aa07ef8f6
---
# Create and Manage Rules

To build a rule, the first step is to use the rule editor to define the conditions in the shopper's query text that trigger the associated events. Then, complete the rule details, test the results, and publish the rule.

## Create a rule

1. In the left rail, go to _Merchandising_ > **Merchandising Rules**.
1. Click **Create rule** to launch the rule editor.

![Create Rule](../../assets/create-rule.png)

In the **Build your rule** section, you define specific search criteria, conditions, and ranking types.

1. In the **[!UICONTROL Name]** field, enter a name for the rule. All rule names must be unique.
1. In the **[!UICONTROL Description]** field, enter a description for the rule.
1. In the **[!UICONTROL Date range]** field, specify the date or range of dates you want the rule to be active.
1. In the **[!UICONTROL Rule applies to]** section, you have two options: **[!UICONTROL All product listings]** or **[!UICONTROL Specific conditions]**.

   - **All product listings** - This is essentially your default rule and is applied to all search queries, unless a more specific search query is defined. You can only create one default rule and it cannot contain any conditions. Choose the Intelligent ranking type and any manual rankings you want applied to all default searches.
   - **Specific conditions** - See the next section to learn about the types of conditions you can set for your rule.

### Conditions

Conditions are the requirements to trigger an event. A rule can have up to ten conditions and 25 events. A default rule cannot have any conditions.

![Select Rule Condition](../../assets/rule-set-condition.png)

#### Single condition

1. Under *Build your rule*, select the **Condition** to be met, and follow the instructions to complete the statement.

   - Search query contains - Enter the string of text that must be in the shopper's query. The Match setting determines the degree to which the shopper's query matches the catalog. Options:<br /> Any - Any part of the shopper's query text can match the condition.<br />All - All of the shopper's query must match the condition.
   - Search query is - Enter a string of text that exactly matches the shopper's query. For example: "yoga pants". Rules with `Search query is` and Match `All` can have only one condition.
   - Search query starts with - Enter a character or string of text that must be at the beginning of the shopper's query.
   - Search query ends with - Enter a character or string of text that must be at the end of the shopper's query.

   The results appear immediately in the *Test your rule* pane and are numbered by priority. You can use the *Results per row* slider in the upper right to change the number of products in each row.

1. To test other queries, change the query text in the *Test your rule* search box and press **Return**.
   Initially, the test pane renders the query from the Conditions search box. But now it is rendering the query from the test query box. The test pane renders only one query at a time.
1. If you like the result, update the text in the *Conditions* search box. Then, click anywhere on the page to update the results in the test pane.

#### Multiple conditions

1. To build a rule with multiple conditions, click **Add condition**.
   A rule can have up to ten conditions. The logical operator that joins two conditions is based on the current *Match* setting. By default, *Match* is `All` and the logical operator is `AND`.

1. Select the second condition and enter the required query text.

1. To change the logic of the rule, change the **Match** setting to determine how closely the shopper's search criteria must match the query condition. Set **Match** to one of the following:

   - Any - (Default) All logical operators in the rule are set to `OR` and the results appear in the test pane.
   - All - All logical operators in the rule are set to `AND` and the results appear in the test pane.

   The *Match* value determines the logical operator that is used to join multiple conditions. Changing the *Match* setting changes all logical operators in the rule. It is not possible to combine `AND` and `OR` in the same rule.

   In this example, rather than searching for "yoga pants", there are two separate queries that search for "yoga" or "pants". This rule is less specific and is triggered more often in the storefront than the other.

1. To add another condition, click **Add condition** and repeat the process.

### Intelligent ranking

Intelligent ranking combines user behaviors and site statistics to determine product ranking.
Store owners can set up the following types of ranking strategies:

![Intelligent Rankings](../../assets/rule-intelligent-ranking.png)

- Most purchased: This ranks products by total purchases per SKU in the previous 7 days.
- Most added to cart - Ranks in order of total "Add to Cart" activities in the previous 7 days.
- Most viewed: Ranks the total views per SKU in the previous 7 days.
- Recommended for you - Uses the `viewed-viewed` data point - Shoppers who viewed this SKU also looked at these other SKUs.
- Trending: Looks back at page view events over the past 72 hours for background events and 24 hours for foreground events.
- None: Products are ordered by Relevance.

Select the type of strategy for the rule. The **Test your rule** window displays the expected results.

#### How intelligent ranking scoring works

Intelligent ranking determines the final product order by combining two key factors: **textual relevance** and **behavioral signals**. Understanding how these factors interact helps you set realistic expectations for your search results.

**Scoring components:**

- **Textual relevance**: The dominant factor in scoring. This measures how well a product's name, description, and attributes match the search query. The text relevance score is unbounded (has no specific upper limit) and is influenced by factors like:

   - Frequency of occurrence of matching words.
   - Length  (in words) of product names/descriptions.

- **Behavioral signals**: A bounded boost applied on top of the text relevance score. When you select an intelligent ranking strategy like "Most viewed" or "Most purchased," products with higher behavioral signals receive a fixed boost to their scores. However, this boost has a defined limit.

**Why the most viewed product might not appear first:**

Textual relevance typically dominates ranking because its score is unbounded, while behavioral boosts are fixed. As a result, products with strong text matches often outrank those with higher engagement signals. Behavioral boosts alone may not compensate for large gaps in text relevance. Intelligent ranking addresses this by factoring in both match quality and shopper interaction, improving overall relevance. However, text match quality remains the primary driver of ranking.

**Example:**

A merchant uses the "Most viewed" intelligent ranking strategy and searches for "candle." They expect product SKU YAN-K-E-512 to appear at the top of results because it has the highest view count. However, other products rank higher:

- **Texas Candle** (1st position): Has a shorter, cleaner product name that creates a very high text relevance score. Even though it has fewer views than YAN-K-E-512, its superior text match outweighs the behavioral boost.

- **YAN-K-E-512** (lower position): Despite having the highest view percentile in the "Most viewed" behavioral data, its complex SKU-based name generates a lower text relevance score. The fixed behavioral boost is not enough to overcome this text relevance gap.

See [search rules](./best-practice.md#tips-to-optimize-search-rules) to learn how to improve product findability using rules.

#### Caveats

- Apostrophes and quotes in queries may lead to some minor issues with ranking and relevance in some languages.
- To ensure the intelligent ranking works correctly, make sure that the **Search Weight** for any attributes that are used for search or filtering (facets) is `5` or less.

For information about setting search weights, see the [Metadata API](https://developer.adobe.com/commerce/services/reference/rest/).

### Manual Ranking

**Manual ranking** are actions that modify the search results when defined conditions are met. A single rule can have up to 25 events.

- Boost - Moves a product higher in the search results.
- Bury - Moves a SKU lower in the search results.
- Pin a product - Product is displayed in the selected "Position" on the page.
- Hide a product - Excludes a SKU from the search results.

The easiest way to pin a product is by drag and drop.

1. Click and drag a product in the Test pane. Drag and drop it at the desired position. The Product and Postion fields are automatically populated in the Events pane.

You may also click the pin icon to pin a product to its current location. Use the ellipsis context menu to "Pin to top" or "Pin to bottom".

>[!NOTE]
>
>You can only pin products that are returned in the query.

Or events can be set manually:

1. Under *Events*, choose the **Event** to take place when the associated conditions are met.

   For example, choose `Hide a product`. Then, enter the name of the product that you want to hide. Products are suggested as you type.

1. For multiple events, choose any other events that you want to trigger when conditions are met.

### Finalizing the rule

1. Examine the results of the rule in the test pane.
1. If the rule has multiple queries, test each one that might be affected by the rule.
1. When complete, click **Save and publish**.

   The rule is added to the list in the *Rules* workspace. 

1. Although active rules go into effect immediately, you might have to wait up to 15 minutes for the cached query results in the storefront to be refreshed.

>[!NOTE]
>
>Rules and manually ranked products are applied to the search results when the default sort order, "Sort by: Most Relevant," is selected. If a shopper changes the sort order to something like sort by name or price, rules and manual rankings are no longer in effect.

## Edit, view, and delete rules

Follow these instructions to update the properties of existing rules.

### Edit rule

1. On the *Merchandising rules* workspace, find the rule in the grid that you want to edit and click **More** (...) options.
1. Click **Edit** to access the rule editor.
1. Update the conditions, operators, and events as needed.
1. Update the name, start and end date, and description fields as needed. All rule names must be unique.
1. Test the rule.
1. Publish the changes.
   The rule is added to the list in the *Rules* workspace. Although active rules go into effect immediately, it might take up to 15 minutes for cached query results in the storefront to be refreshed.

### View details

This option provides a quick way to see all the rule parameters, while staying on the *Rules* table.

1. On the *Merchandising rules* worksapce, find the rule in the grid that you want to edit and click **More** (...) options.
1. Click **View details** to view the rule parameters.
1. Choose **Edit** or **Delete**, or click the X to close the panel.

### Delete rule

1. On the *Rules* workspace, find the rule in the grid that you want to edit and click **More** (...) options.
1. Click **Delete**.

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

### Manual Ranking

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
