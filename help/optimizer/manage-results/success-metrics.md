---
title: Success metrics report
description: The Success metrics report page provides insight into the key performance metrics for your [!DNL Adobe Commerce Optimizer] store.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 7202a531-fec3-4698-89b9-6bdbcc37015e
---
# Success metrics report

This page provides an overview of the key performance metrics for your [!DNL Adobe Commerce Optimizer] store. The goal is for you to quickly understand the results of implementing [!DNL Adobe Commerce Optimizer] then help you and your team identify opportunities for growth, and highlight areas for optimization.

![Success metrics report](../assets/success-metrics.png)

The metrics in the report are pulled from storefront event data. [Learn more](../setup/events/overview.md) about the event data collected.

## Understanding your metrics

The success metrics report provides insights into five key performance areas that directly impact your business success. Each metric tells a story about your customers' behavior and your store's performance. Use these insights to make data-driven decisions and optimize your commerce experience.

### Key performance indicators

- **Revenue** - Your primary financial metric showing total sales performance.
- **Conversion** - The percentage of visitors who complete purchases.
- **Engagement** - How actively users interact with your site.
- **Acquisition** - The effectiveness of your customer acquisition efforts.
- **Bounce Rate** - The percentage of visitors who leave after viewing only one page.

## Generate a report

1. From the left rail, select **Success Metrics**.
1. Under **Report Configuration** specify the **Date range**, **Catalog source**, based on your locale setting, and **Currency**.
1. Click **[!UICONTROL Apply]**.

    The **Top Highlights**, **Revenue**, **Conversion**, **Engagement**, **Acquisition**, and **Bounce rate** all update based on your report configuration.

1. Click **[!UICONTROL Export]** to save the report as a PDF.

## Next steps and optimization strategies

Use your success metrics data to identify opportunities for improvement and implement targeted optimization strategies. The following sections provide specific, actionable guidance for each metric area.

### Revenue optimization

For revenue, your goal is to increase total sales and average order value.

![Success metrics revenue](../assets/revenue.png)

#### Strategies

- **Implement AI-powered recommendations**: Use the optimizer's recommendation engine to surface relevant products that drive higher conversion rates. Deploy "Customers who viewed this also viewed" and "Bought this, bought that" recommendation types to increase cross-selling opportunities.

- **Create merchandising rules**: Boost high-margin products in search results using [merchandising rules](../merchandising/rules/overview.md). Pin best-selling items to the top of search results for high-traffic queries.

- **Optimize product discovery**: Use [intelligent facets](../merchandising/facets/overview.md) to help customers find products more efficiently, leading to higher conversion rates and increased revenue.

- **Leverage seasonal opportunities**: Create time-based merchandising rules to promote seasonal or promotional items during peak shopping periods.

### Conversion rate improvement

To improve your conversion rate, your goal is to convert more visitors into customers.

![Success metrics conversion rate](../assets/conversion-rate.png)

#### Strategies

- **Optimize search relevance**: Implement [synonyms](../merchandising/synonyms/overview.md) to ensure customers find what they're looking for, even with different search terms. Use dynamic faceting to provide relevant filtering options.

- **Strategic recommendation placement**: Deploy recommendation units on high-traffic pages like product detail pages and category pages. Use "Most viewed" and "Most purchased" recommendations to build trust and urgency.

- **Improve product visibility**: Use merchandising rules to ensure best-selling and high-converting products appear prominently in search results.

- **A/B test recommendation types**: Experiment with different recommendation types and placements to find what works best for your audience.

### Engagement enhancement

To enhance engagement, your goal is to increase customer interaction and time on site.

![Success metrics engagement](../assets/engagement.png)

#### Strategies

- **Diversify recommendation types**: Avoid showing the same recommendations repeatedly. Use a mix of "Recommended for you", "Trending", and "Recently viewed" to keep content fresh and engaging.

- **Implement intelligent search**: Use AI-driven dynamic faceting and result re-ranking to adapt search results in real-time based on shopper behavior.

- **Create personalized experiences**: Deploy "Recommended for you" units on the homepage and throughout the customer journey to provide personalized product suggestions.

- **Optimize search experience**: Use synonyms to improve search relevance and ensure customers find what they're looking for quickly.

### Acquisition growth

To acquire more growth, your goal is to attract more new customers and improve acquisition efficiency.

![Success metrics acquisition](../assets/acquisition.png)

#### Strategies

- **Leverage search performance data**: Use the [search performance](../manage-results/search-performance.md) report to identify trending products and popular search terms. Create merchandising rules to highlight these items.

- **Optimize recommendation performance**: Monitor [recommendation performance](../manage-results/recommendation-performance.md) metrics to identify which recommendation types drive the most traffic and conversions.

- **Highlight new and promotional items**: Use merchandising rules to boost new products or promotional items in search results to attract attention from new visitors.

- **Track traffic sources**: Use event data to understand which channels bring the most valuable traffic and optimize your marketing efforts accordingly.

### Bounce rate reduction

To reduce the bounce rate, your goal is to keep visitors engaged and reduce single-page visits.

![Success metrics bounce rate](../assets/bounce-rate.png)

#### Strategies

- **Improve search relevance**: Use synonyms and intelligent faceting to ensure customers find relevant products quickly. Poor search results are a major cause of high bounce rates.

- **Implement recommendation units**: Deploy recommendation units on category and search results pages to provide additional product options and keep visitors engaged.

- **Optimize product discovery**: Use merchandising rules to ensure the most relevant and popular products appear first in search results.

- **Create engaging homepage experiences**: Use "Recommended for you" and "Trending" recommendation types on your homepage to immediately engage visitors with relevant content.

## Troubleshooting and optimization

### When metrics are declining

**Revenue declining**:

- Check if recommendation units are still active and performing well
- Review merchandising rules to ensure high-margin products are being promoted
- Analyze search performance to identify if popular products are still ranking well

**Conversion rate dropping**:

- Verify that search relevance is maintained (check synonyms and facets)
- Ensure recommendation units are displaying correctly
- Review merchandising rules for any conflicts or issues

**High bounce rates**:

- Check search result relevance and implement synonyms if needed
- Ensure recommendation units are loading properly
- Review product data quality and availability

**Low engagement**:

- Diversify recommendation types to prevent customer fatigue
- Implement more personalized recommendation strategies
- Optimize search experience with better facets and synonyms

## Field descriptions

### Report configuration

|Field|Description|
|---|---|
|Date range|Options include **Past 3 months**, **Past 7 days**, **Past 30 days**, **Past 6 months**, **Past 12 months**, and **Year to date**. Use shorter ranges for immediate optimization insights and longer ranges for trend analysis. |
|Country|Based on the catalog source specified for your [catalog view](../setup/catalog-view.md). Select the appropriate market for accurate performance analysis.|
|Currency|The currency specified for your catalog view. Ensure this matches your target market for accurate revenue reporting.|
|Export|Saves the report as a PDF for sharing with stakeholders or offline analysis.|

### Performance metrics

|Field|Description|Optimization focus|
|---|---|---|
|Top Highlights|Summarizes key metrics from each performance area. Use this section to quickly identify your biggest opportunities for improvement.|Focus on the metric with the most room for improvement first.|
|Revenue|The total amount of money generated from sales transactions. This is the primary financial metric that shows how much money your business is making from customer purchases.|Implement [recommendations](../merchandising/recommendations/overview.md) and [merchandising rules](../merchandising/rules/overview.md) to boost high-margin products and increase average order value.|
|Conversion|The percentage of visitors to your site who complete a purchase. This metric indicates how effectively your site converts browsers into buyers.|Optimize [search relevance](../merchandising/synonyms/overview.md), implement strategic [recommendation placement](../merchandising/recommendations/best-practice.md), and use [merchandising rules](../merchandising/rules/overview.md) to surface best-converting products.|
|Engagement|Measures how actively users interact with your site, including metrics like time on site, pages per session, click-through rates, and social interactions. Higher engagement typically indicates users find your content valuable and are more likely to convert.|Diversify [recommendation types](../merchandising/recommendations/types.md), implement [intelligent search](../merchandising/facets/overview.md), and create personalized experiences with "Recommended for you" units.|
|Acquisition|Refers to the process and cost of acquiring new customers. This includes metrics like customer acquisition cost (CAC), traffic sources, and the effectiveness of marketing channels in bringing new visitors to your site.|Use [search performance data](../manage-results/search-performance.md) to identify trending products, optimize [recommendation performance](../manage-results/recommendation-performance.md), and highlight new/promotional items with [merchandising rules](../merchandising/rules/overview.md).|
|Bounce Rate|The percentage of visitors who leave your site after viewing only one page. A high bounce rate (typically above 50-60%) suggests users aren't finding what they're looking for or the page doesn't meet their expectations, which can negatively impact conversions and revenue.|Improve [search relevance](../merchandising/synonyms/overview.md), implement [recommendation units](../merchandising/recommendations/overview.md) on key pages, and optimize [product discovery](../merchandising/facets/overview.md) with better faceting.|

## Related topics

- [Search Performance](../manage-results/search-performance.md) - Analyze search terms and optimize search relevance
- [Recommendation Performance](../manage-results/recommendation-performance.md) - Monitor and optimize recommendation effectiveness
- [Recommendations Overview](../merchandising/recommendations/overview.md) - Learn about AI-powered product recommendations
- [Merchandising Rules](../merchandising/rules/overview.md) - Boost, bury, pin, or hide products in search results
- [Facets](../merchandising/facets/overview.md) - Enhance search with intelligent filtering
- [Synonyms](../merchandising/synonyms/overview.md) - Improve search relevance and customer experience
- [Events Overview](../setup/events/overview.md) - Understand the data that powers your metrics
