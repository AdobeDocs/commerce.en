---
title: Opportunities
description: The Opportunities page helps you identify and implement optimizations to improve site traffic, user engagement, and conversion rates through integration with Adobe Sites Optimizer.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Opportunities

The **Opportunities** page helps you identify and implement optimizations to improve site traffic, user engagement, and conversion rates through integration with Adobe Sites Optimizer.

![Opportunities](../assets/opportunities.png)

## What are Opportunities?

[Opportunities](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/documentation/opportunities/overview) are AI-powered recommendations that help merchandisers identify and address issues impacting their commerce site performance. These recommendations are powered by [Adobe Experience Manager Sites Optimizer](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/home), a cloud-based service that analyzes and improves website performance.

## Key capabilities

- **Automated issue detection**—Sites Optimizer continuously scans product catalogs, search logs, and recommendation data to identify problems affecting discovery.
- **AI-driven recommendations**—Receive intelligent suggestions to resolve detected issues.
- **Impact categorization**—Issues are categorized by business impact (Search, Recommendations, Browse/Navigation, Product Data Quality).
- **Dashboard reporting**—View issue trends, top impacted products/queries, and improvements over time.

## Get started

To enable Opportunities in Commerce Optimizer, contact your customer success manager (CSM). Opportunites are available with the Ultimate subscription.

## Quick tour

The Opportunities page is organized into three tabs that help you manage optimization recommendations:

- **Current (Active)**—Displays newly detected opportunities that require review and action. These are active issues that may be impacting your site performance.
- **Skipped**—Contains opportunities that you have chosen to dismiss or postpone. You can move opportunities here if they are not relevant to your current business objectives.
- **Optimized (Done)**—Shows opportunities that have been successfully addressed, either through auto-fix deployment or manual implementation. This tab helps you track your optimization progress over time.

![Current Opportunities](../assets/current-opportunities.png)

## Auto-detect workflow

The auto-detect workflow uses AI-powered analysis to automatically identify optimization opportunities across your product catalog. This automated scanning process continuously monitors your product data, search logs, and recommendation performance to detect issues that could impact site performance, SEO, and customer engagement.

### How it works

Auto-detect leverages Adobe Experience Manager Sites Optimizer to:

- **Analyze product pages**—The system examines the top 200 pages and filters for product detail pages to identify optimization targets.
- **Extract metadata**—Meta tags (titles, descriptions, H1 headers) are extracted from each page for analysis.
- **Generate AI recommendations**—Extracted data is processed through Adobe's AI workflow to create actionable optimization suggestions.
- **Populate opportunities**—Auto-detected suggestions appear in the **Current (Active)** tab for your review.

### Prerequisite

Before auto-detect can generate recommendations, your catalog data must be synchronized and up-to-date to ensure accurate recommendations.

>[!IMPORTANT]
>
>Merchants without their catalog in Commerce Optimizer can still view opportunities but will need to implement fixes manually. The auto-fix feature requires a fully ingested catalog to function.

### What happens next

Once auto-detect identifies optimization opportunities, you can:

- Review suggested optimizations in the **Current (Active)** tab.
- Deploy fixes automatically using the [auto-fix workflow](#auto-fix-workflow) (for supported opportunity types).
- Implement changes manually in your Commerce Admin.
- Ignore opportunities that do not align with your business objectives.

## Auto-fix workflow

The auto-fix workflow allows you to quickly deploy AI-generated optimizations with a single click. When you apply an auto-fix, the system creates a catalog optimization layer that overrides specific product attributes without modifying the original product data. This approach ensures that optimizations are non-destructive and can be easily managed or reverted if needed.

### Prerequisites

Before using auto-fix, ensure:

- Your product catalog is fully ingested into Commerce Optimizer.
- The opportunity type supports auto-fix (some optimization types require manual implementation).
- You have appropriate permissions to create and manage catalog layers.

### Deploy an auto-fix optimization

Follow these steps to implement an AI-suggested optimization:

1. Navigate to **Manage Results** > **Opportunities**.

1. In the **Current (Active)** tab, review available optimization suggestions.

1. Select an opportunity.

    ![Select Opportunity](../assets/autofix-opportunity.png)

   >[!NOTE]
   >
   >Only supported suggestion types display the **Deploy optimization** button. Other types are marked for manual action and require implementation through your Commerce Admin.

1. Click **Deploy optimization** then click **Deploy** to trigger the auto-fix process.

    ![Deploy Optimization](../assets/deploy-autofix.png)

   The system performs the following actions in the background:
   
   - Creates a new catalog layer for the product (if one does not already exist).
   - Updates the relevant attribute (such as meta title, description, or H1) based on the AI recommendation.
   - Assigns the new layer as the highest priority (order 1) in the catalog view.
   - Validates the change through the catalog storefront service.

1. Monitor the deployment status. The system updates the suggestion status automatically once validation is complete.

1. Once optimized, the suggestion moves to the **Optimized (Done)** tab with a status indicator:
   
   - **Green checkmark**—The optimization layer is set as the first priority and is actively applied to your storefront.
   - **Warning icon**—The layer exists but is not the top priority, meaning it may be overridden by another layer.

   ![Completed Opportunities](../assets/done-opportunities.png)

### How catalog layers work with auto-fix

Understanding catalog layers helps you manage optimizations effectively:

- **Non-destructive changes**—Auto-fix creates optimization layers that override product attributes without modifying the original product data.
- **Priority ordering**—Layers are prioritized by order number. Order 1 (highest priority) takes precedence over lower-priority layers.
- **Layer updates**—If you apply additional suggestions to the same product, the existing layer is updated with new attributes rather than creating duplicate layers.
- **Manual management**—You can manually adjust layer priorities through your catalog view settings, though this may affect which optimizations are applied.

### Important considerations

Keep the following in mind when using auto-fix:

- The status shown for each suggestion reflects the state at the time the auto-fix worker ran. The status does not update dynamically if you manually reorder catalog layers afterward.

- To ensure your optimizations remain active, avoid manually changing catalog layer priorities after deploying auto-fix recommendations.

### Troubleshooting

If an optimization does not appear to be applied on your storefront:

1. Check the status indicator in the **Optimized (Done)** tab.
1. If you see a warning icon, verify the catalog layer priority settings.
1. Ensure the optimization layer is set as order 1 (highest priority) in your catalog view.
1. Confirm that catalog data synchronization is active and up-to-date.

## How Sites Optimizer and success metrics work together

Success metrics monitors key performance indicators, such as product discovery and catalog business efficiency, while opportunities within Sites Optimizer lets you know how you can boost SEO, load speed, accessibility, and engagement. Together, merchandisers and marketers can improve operational efficiency, bringing faster end-to-end performance and conversion gains with minimal IT support. To learn how you can take advantage of these two technologies to improve your storefront performance and experience, see [Using Success Metrics and Sites Optimizer together](./success-metrics.md#using-success-metrics-and-sites-optimizer-together).

## Learn more about Sites Optimizer

For detailed information about Sites Optimizer capabilities and features, see the [Adobe Experience Manager Sites Optimizer documentation](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/home).

Additional resources:

- [Opportunity types](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/opportunities) - Learn about available optimization opportunities.
- [Sites Optimizer capabilities](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/capabilities) - Explore what Sites Optimizer can do.

## More like this

- [Success Metrics](success-metrics.md) - Monitor key performance indicators.
- [Search Performance](search-performance.md) - Analyze search terms and optimize relevance.
- [Recommendation Performance](recommendation-performance.md) - Monitor recommendation effectiveness.
