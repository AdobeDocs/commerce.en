---
title: Improve product discovery with Adobe Commerce Live Search
description: Learn how to use search performance insights and semantic search to help shoppers find relevant products.
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---

# Improve product discovery with Adobe Commerce Live Search

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Portrait of Sandra Gonzalez Mangana" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em>Senior Product Manager</em></td>
</tr>
</table>

*Help shoppers find the products they need with search performance insights and semantic search.*

Having the right products in your catalog is only part of the shopping experience. Shoppers also need to be able to find those products using the words, phrases, and questions they naturally use.

Adobe Commerce Live Search provides search performance insights that can help you spot discovery problems and refine the experience. Use those insights to investigate where shoppers have difficulty—not just whether search returns results.

## Look for signals in search performance

In the Live Search Performance workspace, review metrics such as unique searches, zero-result searches, popular results, click-through rate, conversion rate, and average click position. Use them to identify trends and decide which queries or products need attention. [Performance](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/performance)

![Live Search Performance workspace showing unique searches, average click position, click-through rate, conversion rate, and zero results rate, with tabs for unique searches, zero results, and popular results](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*The Live Search Performance workspace shows the metrics to review. The values shown are sample data.*

Consider these signals:

- **Zero-result searches:** Queries with no results may point to gaps in your catalog, product information, or search setup. Aim to keep zero-result searches below 5%. A rate above this threshold is a signal worth investigating.
- **Low click-through or weak click position:** Shoppers may be seeing results that do not match their needs, or relevant products may not be prominent enough. To ensure engagement, aim for at least 50% of searches to result in a product click.
- **Low conversion from search:** Review whether search is helping shoppers move from a query to a purchase. Aim for a conversion rate above 3%.

Treat these as a benchmark and diagnostic signals, not universal pass-or-fail. Performance varies by industry, catalog complexity, customer behavior, and how each metric is measured. Establish a baseline for your store and compare performance over time. Results can vary with your catalog, shoppers, and how you measure outcomes.

## Match shopper intent, not just exact words

Shoppers do not always describe products using the terminology in your catalog. Someone searching for "comfortable shoes for standing all day," for example, may be interested in products described as "cushioned walking sneakers."

Semantic search uses meaning and context alongside keyword matching, helping connect natural-language queries to relevant products even when the query does not match catalog wording exactly. Live Search combines keyword and semantic matching in one search experience. [Semantic Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)

Semantic matching can help with exploratory searches, but relevance still depends on the products and information available in your catalog. For searches involving an exact model, specification, or compatibility requirement, check that the results remain precise.

## Check semantic search for your deployment

The setup depends on the Adobe Commerce product you use:

- **Adobe Commerce on cloud infrastructure or on-premises:** Live Search semantic search is available for Adobe Commerce 2.4.4 and later. In the Admin, go to Marketing > SEO & Search > Live Search, open Settings, enable semantic search, and save. It supports English catalogs. [Settings—Semantic search](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service:** The system enables semantic search by default. It supports English catalogs. [Semantic Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer:** The system enables semantic search by default. You can optionally tune controls such as semantic boost and the similarity threshold. The settings also include fuzzy-search options. [Semantic Search](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/semantic-search) · [Settings—Optional tuning](https://experienceleague.adobe.com/en/docs/commerce/optimizer/settings)

## Turn search insights into action

Use a continuous review cycle to improve product discovery:

1. **Find queries to investigate.** Review zero-result searches, popular queries, and searches with low engagement.
2. **Check what the shopper is asking for.** Determine whether the query points to a missing product, a wording mismatch, or unclear product data.
3. **Improve product information.** Make product attributes and descriptions accurate and useful for the terms shoppers use. For Live Search, Adobe recommends setting up the appropriate searchable attributes and weights and ensuring the attribute data is relevant. [Live Search Best Practices](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
4. **Refine the search experience.** Where appropriate, use search rules, synonyms, and facets to help shoppers find and narrow down relevant results. [Live Search Best Practices](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
5. **Review results and repeat.** Monitor the same queries and performance signals after making changes, then adjust based on what shoppers do.

## Make every search count

A search query is a signal of what a shopper wants. By pairing search performance insights with relevant product information and the right search capabilities, you can make it easier for shoppers to discover products that meet their needs.

### Learn more

- [What is Live Search?](../../../live-search/overview.md)
- [Live Search Best Practices](../../../live-search/best-practice.md)
- [Semantic Search](../../../live-search/semantic-search.md) for Adobe Commerce on cloud infrastructure
- [Semantic Search](../../../optimizer/setup/semantic-search.md) for Adobe Commerce Optimizer
