---
title: Search performance
description: The Search performance page provides insight into the search terms that shoppers use.
---
# Search performance

The *Search performance* page provides insight into the search terms that shoppers use. The information can be used to identify trends, increase click-through, and improve the conversion rate. The Search performance page provides a snapshot of search metrics for a specific date range and includes the following reports:

- Unique searches
- Zero results
- Popular results

!!!ADD WORKSPACE SCREENSHOT!!!

You can also refer to the [Data Sync Dashboard](../setup/data-sync.md) for more information about data syncing.

>[!NOTE]
>
>The Search performance page is updated every 12 hours.

## View a report

1. To enter the **Date range**, click the calendar and do one of the following:

   - To specify a single date, double-click the date on the calendar.
   - To specify a range of dates, click the first and last date on the calendar.

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

## Ways to improve search performance

This article helps merchandisers enhance their site search functionality, ensuring a seamless and efficient shopper experience that maximizes conversion rates. By following the strategies outlined, you learn how to implement advanced search features, and continuously refine your search tool for optimal performance with Adobe Commerce [!DNL Adobe Commerce Optimizer].

There are several key factors that determine the relevance and effectiveness of search results:

- Well-structured product data ensures that search algorithms can effectively match products to queries. Low quality product data leads to low relevant search results. To directly impact the success of your merchandising strategy:
    - Set up the correct attributes as searchable with their corresponding weight.
    - Make sure that data within those attributes is relevant.
- A well-designed search experience builds trust with customers and instills confidence that they will find what they need.
- Search rules are critical as they can elevate the visibility of certain products based on popularity, new arrivals, promotional criteria or any other merchandising strategy to meet your business requirements.
- Faceted navigation allows shoppers to refine their search and get relevant results quickly.

To manage [!DNL Adobe Commerce Optimizer], go to **Marketing** > *SEO & Search* > **[!DNL Adobe Commerce Optimizer]** in the Adobe [!DNL Adobe Commerce Optimizer] Admin. 

## Optimize your search functionality

In this section, you learn how to optimize your search functionality by using features such as autocomplete to provide real-time suggestions as shoppers type, synonyms and spellings to ensure that shoppers find products even if they use different words, facets to allow shoppers to narrow down search results, and search redirects to automatically redirect shoppers from a search query to a specific page.

### Autocomplete

Autocomplete, also known as type-ahead or autosuggest, is an interactive search feature that dynamically displays suggestions to shoppers as they enter their search terms. This helps shoppers quickly and easily find products by offering real-time suggestions based on their input.

The [!DNL Adobe Commerce Optimizer] [[!DNL popover]](storefront-popover.md) widget enables autocomplete search options to suggest popular products. With each character typed by the shopper, the popover updates with suggested products and thumbnail images of the top search results.

[!DNL Adobe Commerce Optimizer] starts returning results when the user has typed in two characters. For a partial match, the maximum number of characters per word is 20. The number of characters in a "search as you type" query is not configurable.

Learn more about the [popover](storefront-popover.md) widget.

### Search redirects

A search redirect allows you to automatically redirect shoppers from a search query to a specific page. Search redirects can improve shopper experience and guide customers to the most relevant content, such as a product page, category, landing page, or a tailored set of search results. Search redirects help streamline the shopping experience and ensure that shoppers find what they are looking for quickly and efficiently.

Recommended use cases for setting up search redirects:

- **Popular Products or Categories** - Redirect shoppers to a specific product page or category when they search for common or popular terms. For example, searching for "iPhone" might redirect directly to the iPhone category page or a specific model page.
    
- **Promotional Campaigns** - During promotional events or sales, redirect relevant search terms to landing pages that highlight special offers or featured products.
    
- **Brand Searches** - When shoppers search for a brand name, redirect them to the brand's dedicated page where all products from that brand are listed.
    
- **Product Discontinuation** - If a product is discontinued, you can redirect searches for that product to similar products or the new version of the product.

Always test search redirects to ensure they are working correctly and are leading to the most relevant pages. Continuously monitor their performance and make adjustments as needed.

Learn how to [manage search redirects](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms).

## Improve search result relevance

This section discusses how to improve search result relevance by implementing effective search rules and using product metadata to ensure accurate and detailed attributes are searchable.

### Images

Make sure that configurable products' child products have images with the correct roles. Having parent or child products might result in the search result not having images.

>[!NOTE]
>
>Images in search results might be different depending on the search term. If the search term determines that a child product is more relevant, images from the child product will be used instead of images from the parent product.


### Leverage Product Metadata

Ensure that accurate and detailed product attributes are [set up as searchable](workspace.md#set-attributes-as-searchable). Note that SKU, name, and category attributes are searchable by default and cannot be excluded from search. For best results, do not use spaces in your SKUs.

To increase search relevance, assign a weight to each searchable attribute. Attributes with a higher weight should appear higher within the search results. Sorting by relevance is affected by multiple criteria, such as search weight. This means that sometimes attributes with lower search weight can still have more relevance than attributes with higher search weight. Other criteria can include the number of matches in any given attribute, position of found search term, and overall text structure before and after a search term.

Ensure that each product has relevant content within each searchable attribute. It is not recommended to set an attribute as searchable if it has large amounts of content as that can reduce search result relevance.

Learn more about product attributes for search:

- [Set attributes as searchable](workspace.md#set-attributes-as-searchable)
- [Assign weight to attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results#weighted-search)

## Monitoring Search Results

To optimize search results with [!DNL Adobe Commerce Optimizer], monitor relevant Key Performance Indicators (KPIs) such as unique queries, average click position, click-through rates, conversion rate, and zero results rate to understand how shoppers interact with your search functionality. This data guides you to regularly update and refine your search rules.

You can monitor these KPIs within the [!DNL Adobe Commerce Optimizer] [Performance workspace](performance.md) where you find the following metrics: 

- **Unique Searches** - The count of distinct search queries performed on your [!DNL Adobe Commerce Optimizer] site. Each unique search is counted only once, even if it is repeated multiple times by the same shopper or different shoppers. This metric helps you understand the diversity of search terms used by customers and provides insights into what products or information shoppers are seeking. Tracking unique searches allows you to:

    - Identify popular search trends and frequently searched items.
    - Detect potential gaps in your product catalog or content.
    - Optimize your search functionality by adding [synonyms](synonyms.md), creating, or updating search rules.

- **Average Click Position** - Indicates that the average position of search results clicked by shoppers after performing a search query on your site. This metric provides insights into the relevance and effectiveness of your search results.

    A lower average click position (closer to 1) suggests that shoppers find relevant results quickly, indicating that your search strategy is effective. It helps you understand shopper behavior and how far they are willing to scroll to find the desired product. If the average click position is high, it may indicate that the most relevant results are not appearing at the top, which necessitates a review and optimization of your search strategy.

- **Click-Through Rate (CTR)** - Measures the percentage of shoppers who click on a search result after performing a search query. A high CTR indicates that the search results are relevant and appealing to shoppers, as they are clicking on the results they find. Monitoring CTR can help identify areas for improvement. Low CTR may suggest that search results are not matching shopper intent, prompting a need to refine search rules, enhance product data, or improve result presentation.

- **Conversion Rate** - Indicates the effectiveness of your search feature in driving sales and achieving business goals. It reflects the overall effectiveness of your search functionality in meeting shopper needs and facilitating a smooth shopping experience. A high conversion rate indicates that your search results are highly relevant and persuasive, leading shoppers to complete purchases. If the conversion rate is low, it may suggest issues with search relevance, product availability, or the overall shopper journey from search to purchase.

- **Zero Results** - Measures the percentage of search queries on your [!DNL Adobe Commerce Optimizer] site that return no results. This metric is crucial for understanding how often shoppers' searches are unsuccessful and can provide insights into potential gaps in your product catalog or search setup. A high zero results rate can frustrate shoppers, leading to a poor shopping experience and potential loss of customers. It can indicate missing products or categories in your catalog that shoppers are searching for, guiding inventory and product listing decisions.

    To reduce the zero results rate, you can:

    - Offer alternative or related search terms, such as [synonyms](synonyms.md) when no exact matches are found.
    - Provide shoppers with related or alternative suggestions when their search yields no results by setting search redirects.
    - Regularly review zero result queries to identify patterns and make necessary adjustments to your product catalog and search settings.

- **Popular Results** - Can significantly enhance your search results by aligning them with shopper preferences and behaviors.

You can use this metric data to optimize your search functionality in the following ways:

- Implement rules to automatically rank popular products higher in search results. Products frequently clicked on or purchased can be given priority to appear at the top. Manually curate lists of popular products for specific search queries and ensure that these items are prominently displayed.
- Highlight products that are currently trending or have recently seen a spike in popularity. This can be particularly effective during seasonal events, holidays, or promotional periods. To achieve this use the intelligent ranking that better suits your use case and business need when setting up a search rule.
- Highlight popular filters or facets, if shoppers frequently filter by certain brands or price ranges, make those options more prominent by pinning those facets and sort them accordingly.
- When a search yields zero results, use popular results data to suggest alternative products or related categories that have high shopper engagement.
- Analyze popular search terms and product data to identify important keywords. Optimize your product searchable attributes with these keywords to improve search relevance.
- Regularly analyze your results data to understand changing trends, shopper preferences and behavior, identify top search terms, and detect issues. Use this feedback loop to continuously refine and improve your search rules and product offerings
