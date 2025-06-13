---
title: Recommendations Best Practices
description: Learn where you can place recommendations on various pages on your site and suggestions for frequently used labels for each recommendation type.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Recommendations Best Practices

Adobe recommends the following guidelines when using recommendations:

- Diversify your recommendation types. Customers start ignoring recommendations if they suggest the same products over and over again.

- Do not deploy the same recommendations to your cart page and order confirmation page. Consider using `Most Added to Cart` for the cart page and `Bought This, Bought That` for the order confirmation page.

- Keep your site tidy. Do not deploy more than three recommendation units on the same page.

- If your store sells clothing, the `More like this` recommendation can suggest gender-specific products that do not match the gender of the product being viewed. Consider using this recommendation type only for non-clothing categories.

## Placement

With so many recommendation types to choose from, which should you use on each page? If you are not sure where to begin, try the following:

|Page|Recommendation Type|
|---|---|
|Home page|`Recommended for you`|
|Product page|`Viewed this, viewed that`|
|Cart|`Bought this, bought that`|

You can track the [metrics](../../manage-results/recommendation-performance.md) and adjust if needed. Remember that experimentation is key.

Some storefront pages restrict where you can place the recommendations. You can place the recommendations in one of the following page locations. Refer to the [table below](#supported-recommendations-by-page) for more information.

- At the top of main content - Recommendations appear above the main content area just below the top navigation bar.
- At the bottom of main content (default) - Recommendations appear below the main content area and before any other content blocks on the page, such as _Related Products_.

![Recommendation placement](../../assets/storefront-home-page-top.png)
_Recommendation at top of home page_

## Recommendation labels

The label that is assigned to a recommendation in the storefront affects how shoppers interpret its relevancy to them. The following labels are frequently used for each type of recommendation.

![Recommendation placement](../../assets/storefront-search-results-top.png)
_Recommendation at top of search results_

|Recommendation Type|Recommended Labels|
|---|---|
|Most viewed<br> Most added to cart<br>Most purchased<br>Conversion (view to cart)<br>Conversion (view to purchase)|Most popular<br>Popular items<br>Trending<br>Popular right now<br>Recently popular<br>Popular items inspired by this item (PDP)<br>Top sellers<br>You might be interested in|
|Recommended for you|Just for you<br>Recommended for you<br>Inspired by your shopping trends|
|Viewed This, Viewed That|Customers who viewed this item also viewed<br>Customers also viewed<br>Related items|
|Viewed This, Bought That|Customers who viewed this ultimately bought<br>Customers ultimately purchased<br>What do others buy after viewing this item?|
|Bought This, Bought That|Get everything you need<br>Don't forget these<br>Frequently bought together|
|More Like This|More items like this<br>Similar to this|
|Generic|You may also like<br>Shoppers also liked<br>Similar options<br>Related items|
|Trending|Trending<br>Trending now<br>Recently trending<br>Hot items<br>Trending related products (PDP)|
|Recently viewed|Recently viewed<br>Take another look|

## Supported recommendations by page

The following table lists the storefront pages where you can place recommendations and the recommendation types allowed on each page.

|Page|Placement Recommendations|Types|
|---|---|---|
|Home page|At the top of main content<br>At the bottom of main content (default)|Most viewed<br>Most purchased<br>Most added to cart<br>Recommended for you<br>Trending|
|Category|At the top of main content<br>At the bottom of main content (default)|Most viewed<br>Most purchased<br>Most added to cart<br>Recommended for you<br>Trending|
|Product Detail|At the bottom of main content (default)|Most viewed<br>Most purchased<br>Most added to cart<br>Viewed this, viewed that<br>Viewed this, bought that<br>Bought this, bought that<br>More like this<br>Trending<br>Visual similarity|
|Cart|At the bottom of main content (default)|Most viewed<br>Most purchased<br>Most added to cart<br>Viewed this, viewed that<br>Viewed this, bought that<br>Bought this, bought that<br>More like this<br>Trending|
|Confirmation|At the bottom of main content (default)|Most viewed<br>Most purchased<br>Most added to cart<br>Viewed this, viewed that<br>Viewed this, bought that<br>Bought this, bought that<br>More like this<br>Trending|
