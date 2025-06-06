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

You can also refer to the [Data Management Dashboard](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) for more data about data syncing.

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

| Snapshot data | Description |
|--- |--- |
| Unique searches | The total number of unique searches for the specified date range. Multiple searches by the same shopper, even if for the same query, are considered unique if submitted more than one hour apart. |
| Click-through rate | The percentage of searches that conclude with the shopper clicking a product. For example, the click-through rate is 50% if the shopper searches for "pants" and "shirt" and then clicks one result in the "shirt" search. |
| Conversion rate | The percentage of products the shopper purchases versus the number of products the shopper clicks for the specified date range. For example, the conversion rate of the interaction is 100% if the shopper views six products in the popover, clicks one, and makes a purchase. <br /><br />The conversion rate is not affected by the number of views of a given product. For example, the conversion rate remains the same if the shopper uses search, but does not click any products. |
| Zero results rate | The percentage of unique searches that returns no results for the specified date range. For example, the zero results rate is 66.67% if the shopper searches for "fjjajfjfjf" twice (without results) and for "pants" once (with results). |
| Avg. click position | The relative position of the average click-through rate based on unique searches for the specified date range. |

| Reports | Description|
|--- |--- |
| Unique searches | Lists the unique search queries used during the specified date range. The report data is calculated the same way as unique search snapshot data. If a shopper types the same search query twice, but more than an hour apart, the search is considered to be two unique searches. Report limit: Top 500 terms |
| Zero results | Lists the search queries that return no results and the number of times used during the specified date range. Report limit: Top 500 terms |
| Popular results | Lists the names of products that received the most views during the specified date range. Popular results are calculated based on impressions only and are not affected by the number of clicks or revenue generated. Report limit: Top 500 terms |
