---
title: Recommendations Performance
description: The Recommendations performance page provides insight into how well your product recommendations are performing.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 1b77e2ea-412b-4c78-9d38-390bd8fda87e
---
# Recommendations Performance

The Recommendations Performance page displays a list of configured recommendations along with key metrics to help you evaluate their effectiveness. You can configure the view to display metrics for the past day, week, or month. These insights show how often each recommendation unit is viewed or clicked, helping you assess performance and identify opportunities for optimization.

>[!INFO]
>
>A recommendation unit is a widget that contains the recommended product _items_.

![Recommendations Performance](../assets/rec-performance.png){zoomable="yes"}

## Choose the **Catalog view**

Select the [catalog view](../setup/catalog-view.md) where your recommendations apply.

![Catalog View](../assets/catalog-view.png)

## View a report

Click the calendar and do one of the following:

- To specify a single date, double-click the date on the calendar.
- To specify a range of dates, click the first and last date on the calendar.

>[!NOTE]
>
>The range of dates cannot exceed one year.

## Customize table

1. In the upper-left corner, click the ![Column selector](../assets/icon-show-hide-columns.png) icon to customize the table.

   The visible columns have a check mark.

1. In the menu, do either of the following:

   - To show a hidden column, click any column name without a check mark.
   - To hide a visible column, click any column name with a check mark.

   The table is refreshed to include only the selected columns.

## Set filters

Click the filter icon to filter the metrics on the recommendations performance workspace.

![Filter Metrics](../assets/rec-filters.png)

You can configure multiple values for each of the filters. See the [table below](#column-descriptions) for descriptions of each filter.

## View details

1. In the table, click the (![More selector](../assets/btn-more.png)) icon next to the recommendation that you want to examine.

1. To change the status of the recommendation, click **Activate** or **Deactivate**.

## Create or manage recommendations

Learn how you can [create a new or manage an existing](../merchandising/recommendations/create.md) recommendation.

## Workspace Controls

|Control|Description|
|---|---|
|![Calendar selector](../assets/icon-calendar.png)|Determines the range of time that is used for metrics calculations.|
|![Column selector](../assets/icon-show-hide-columns.png)|Determines the columns that appear in the Recommendations table.|
|Create recommendation|Opens the [Create New Recommendation](../merchandising/recommendations/create.md) page.|

## Column Descriptions

|Column|Description|
|---|---|
|Name|The name of the recommendation.|
|Page|The page where the recommendation appears.|
|Type|The recommendation type.|
|Status|The recommendation status. Options: Inactive/Active/Draft|
|Created|The date the recommendation was created.|
|Last Edited|The date the recommendation was last edited.|
|Impressions|The number of times a recommendation unit is loaded and rendered on a page. A recommendation unit that is below the fold of the browser's viewport is rendered on the page, even if it is not viewed by the shopper. In this case, the rendered unit is counted as an impression, but a view is counted only if the shopper scrolls the unit into view.|
|vImpressions|(Viewable Impressions) The number of recommendation units that register at least one view. For example, if the recommendation unit has two lines, each with two products, and the last two products are not seen by the shopper but the first two are, the activity will still count as an impression.|
|Views|The number of recommendation units that appear in the viewport of the shopper's browser. If the shopper scrolls the page up or down several times, the event fires multiple times, each time the unit is viewable.|
|Clicks|The sum of the number of times a shopper clicks an item in the recommendation unit and the number of times the shopper clicks the **Add to cart** button in the recommendation unit|
|Revenue|The revenue driven by the recommendation for the current time range.|
|Lt Revenue|(Lifetime Revenue) The lifetime revenue driven by a recommendation.|
|Viewability|The percentage of recommendation units that register for the view.|
|CTR|(Click-Through Rate) The percentage of unit impressions for the recommendation that register a click. CTR counts all impressions even if the unit does not enter the shopper's view. If the recommendation unit is not viewed, it is unlikely to get clicked. However, those unseen impressions count toward the CTR score and reduce the overall CTR percentage.|
|vCTR|(Viewable Click-Through Rate) measures clicks based only on viewable impressions (recommendations that actually appeared in the visible part of the shopper's screen), providing a more accurate gauge of shopper engagement.|
