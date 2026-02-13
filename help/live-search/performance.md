---
title: Performance
description: The [!DNL Live Search] Performance workspace provides insight into the search terms that shoppers use.
exl-id: 07a63df8-b981-4913-841a-7e81ec634281
---
# Performance

The *Performance* workspace provides insight into the search terms that shoppers use. The information can be used to identify trends, increase click-through, and improve the conversion rate. The Performance workspace provides a snapshot of search metrics for a specific date range and includes the following reports:

* Unique searches
* Zero results
* Popular results

![Performance](assets/performance-unique-searches.png)

You can also refer to the [Data Management Dashboard](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) for more data about data syncing.

>[!NOTE]
>
>The performance workspace is updated every 12 hours.

## View a report

1. To enter the **Date range**, click the calendar (![Calendar](assets/btn-calendar.png)) and do one of the following:

   * To specify a single date, double-click the date on the calendar.
   * To specify a range of dates, click the first and last date on the calendar.

>[!NOTE]
>
>The range of dates cannot exceed one year.

## Field descriptions

| Snapshot data | Description | Calculation example |
|--- |--- |--- |
| Unique searches | The total number of unique searches for the specified date range. Multiple searches by the same shopper, even if for the same query, are considered unique if submitted more than one hour apart. | **Example:**<br />Searches:<br />- "pants" at 10:00 AM<br />- "pants" at 10:30 AM (within 1 hour → not unique)<br />- "pants" at 12:00 PM (after 1 hour → unique)<br />- "shirt" at 1:00 PM<br /><br />**Total unique searches = 3** |
| Click-through rate | The percentage of searches that conclude with the shopper clicking a product. For example, the click-through rate is 50% if the shopper searches for "pants" and "shirt" and then clicks one result in the "shirt" search. | **Formula:**<br />Click-through rate = Searches with ≥1 click ÷ Total unique searches<br /><br />**Example:**<br />Total unique searches = 4<br />Searches with at least one click = 2<br /><br />CTR = 2 ÷ 4 = **50%** |
| Conversion rate | The percentage of products the shopper purchases versus the number of products the shopper clicks for the specified date range. For example, the conversion rate of the interaction is 100% if the shopper views six products in the popover, clicks one, and makes a purchase. <br /><br />The conversion rate is not affected by the number of views of a given product. For example, the conversion rate remains the same if the shopper uses search, but does not click any products. | **Formula:**<br />Conversion rate = Total products purchased ÷ Total products clicked<br /><br />**Example 1:**<br />Products clicked = 5<br />Products purchased = 2<br /><br />CVR = 2 ÷ 5 = **40%**<br /><br />**Example 2 (5-hour aggregation):**<br />Clicks by hour: 4, 5, 6, 10, 2<br />Purchases by hour: 1, 3, 0, 4, 1<br /><br />Total clicks = 4 + 5 + 6 + 10 + 2 = 27<br />Total purchases = 1 + 3 + 0 + 4 + 1 = 9<br /><br />CVR = 9 ÷ 27 = **33.33%** |
| Zero results rate | The percentage of unique searches that returns no results for the specified date range. For example, the zero results rate is 66.67% if the shopper searches for "fjjajfjfjf" twice (without results) and for "pants" once (with results). | **Formula:**<br />Zero results rate = Unique searches with zero results ÷ Total unique searches<br /><br />**Example:**<br />Total unique searches = 3<br />Searches with zero results = 2<br /><br />Zero results rate = 2 ÷ 3 = **66.67%** |
| Avg. click position | The relative position of the average click-through rate based on unique searches for the specified date range. | **Formula:**<br />Average click position = Sum of click positions ÷ Total clicks<br /><br />**Example:**<br />Clicks at positions: 1, 3, 2<br /><br />Average click position = (1 + 3 + 2) ÷ 3 = **2** |

## Export to Csv Report
| Reports | Description|
|--- |--- |
| Unique searches | Lists the unique search queries used during the specified date range. The report data is calculated the same way as unique search snapshot data. If a shopper types the same search query twice, but more than an hour apart, the search is considered to be two unique searches. <br />**Report limit:** Top 500 terms when generating the CSV file.|
| Zero results | Lists the search queries that return no results and the number of times used during the specified date range. <br />**Report limit:** Top 500 terms when generating the CSV file. |
| Popular results | Lists the names of products that received the most views during the specified date range. Popular results are calculated based on impressions only and are not affected by the number of clicks or revenue generated. <br />**Report limit:** Top 500 terms when generating the CSV file.|
