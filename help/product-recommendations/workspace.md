---
title: '[!DNL Product Recommendations] Workspace'
description: Learn how to configure, manage, and monitor product recommendation performance.
exl-id: eaf1f0b2-9d9d-4069-8269-06f30166f788
---
# [!DNL Product Recommendations] Workspace

The [!DNL Product Recommendations] workspace displays a list of previously configured recommendations with metrics that help you track the success of each recommendation. The list can be configured to calculate metrics for the last day, week, or month. You can use the metrics to create actionable insights based on how frequently a recommendation unit is viewed or clicked, or to analyze how well your recommendations perform.

>[!INFO]
>
>A recommendation unit is a widget that contains the recommended product _items_.

![Recommendations workspace](assets/workspace.png)
_Recommendations Workspace_

## Data collection

To ensure that each functional area on the workspace contains the correct data, you need to configure data collection based on the selected storefront implementation:

1. Luma - Data collection is available out-of-the-box.
1. Headless - Data collection must be configured manually, depending on storefront implementation.

If you are using a headless storefront, refer to the following documentation to get more information about the required events that you need to add:

- [Required events](events.md) for Product Recommendations dashboard.
- [Storefront events collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) that needs to be added as a prerequisite.
- [Examples](https://github.com/adobe/commerce-events/tree/main/examples) of the events structure.

## Set the scope

Initially the [scope](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) of all recommendation settings is set to `Default Store View`. If your Commerce installation includes multiple store views, set **Scope** to the [store view](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) where your recommendations apply.

## Set metrics date range

1. Click the **Calendar** ![Calendar selector](assets/icon-calendar.png) control.

1. Choose one of the following:

   - Last 24 hours
   - Last 7 days
   - Last 30 days

   The calculated values in the metrics columns change to reflect the current date range.

   >[!NOTE]
   >
   >Product Recommendation metrics are optimized for Luma storefronts. If your storefront is non-Luma based, how the metrics track data depends on how you [implement the event collection](events.md).

## Show/hide columns

1. In the upper-left corner, click **Show/hide** ![Column selector](assets/icon-show-hide-columns.png) columns.

   The visible columns have a blue check mark.

1. In the menu, do either of the following:

   - To show a hidden column, click any column name without a check mark.
   - To hide a visible column, click any column name with a check mark.

   The table is refreshed to include only the selected columns.

   ![Recommendations workspace](assets/workspace-select-columns.png)
   _Show/hide columns_

## Settings

The settings determine the SaaS data space that provides the recommendation-behavioral data.

- To change where recommendation-behavioral data originates, choose a different SaaS data space.

- To configure a new SaaS data space, click **Edit Configuration**. To learn more, see [Settings](settings.md).

![Recommendations settings](assets/settings.png)
_Recommendations Settings_

## View details

1. In the table, click the recommendation that you want to examine.

   ![Recommendations workspace](assets/recommendation-detail.png)
   _Home Page Conversion Rate Detail_

1. To change the status of the recommendation, click **Activate** or **Deactivate**.

## Edit recommendation

From the recommendation details page, click **Edit**. To learn more, go to [Edit Recommendations](edit.md).

## Create recommendation

From the recommendation details page, click **Create**. To learn more, go to [Create Recommendations](create.md).

## Workspace Controls

|Control|Description|
|---|---|
|![Calendar selector](assets/icon-calendar.png)|Determines the range of time that is used for metrics calculations. Options: 24 hours / 7 days / 30 days|
|![Column selector](assets/icon-show-hide-columns.png)|Determines the columns that appear in the [!DNL Product Recommendations] table.|
|Settings|Determines the SaaS data space where recommendation-behavioral data is fetched, and also enables visual similarity recommendation type.|
|Create Recommendation|Opens the [Create New Recommendation](create.md) page.|

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
