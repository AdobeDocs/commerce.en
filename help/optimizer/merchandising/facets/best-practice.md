---
title: Facets Best Practices
description: Learn the best practices for implementing facets in your store.
role: Admin, Developer
---

# Facets Best Practices

Filter and facet functionality is a critical component of your [!DNL Adobe Commerce Optimizer] site, designed to enhance the shopper experience by allowing shoppers to narrow down search results and find products more efficiently. This functionality helps shoppers sort through vast catalogs of items by applying specific criteria, making the shopping process faster, easier, and more satisfying. By implementing effective, shopper-friendly filters and facets, you can help customers find exactly what they need quickly and efficiently, ultimately boosting satisfaction and conversion rates.

To set up a product attribute as a facet, it must have the following [properties set](add.md#step-1-add-a-facet):

- **[!UICONTROL Use in Search]** -  `Yes`
- **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
- **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

## Tips to optimize facets

- Determine the most relevant and useful attributes for your products, such as title, category, brand, price range, color, and size and set them as [dynamic facets](type.md). 
- Set and sort product attributes that are consistent across your catalog and highly relevant for your products to improve relevancy and filtering capabilities for your shoppers.
- Ensure that facet labels are easy to understand and consistently named across the site. For example, use "Price Range" instead of "Cost".
- Avoid overwhelming shoppers by limiting the number of facets to the most important ones. Too many options can cause decision fatigue. By default, [!DNL Adobe Commerce Optimizer] is limited to a maximum of 100 attributes configured as facets and 30 buckets returned within each facet. Learn more about [facet limitations](../../boundaries-limits.md#catalog-views-and-policies). 
- Allow shoppers to select multiple filter criteria simultaneously to refine results. For example, letting shoppers select both "Red" and "Blue" colors.
- Display the number of available products next to each facet option to give shoppers an idea of the search results they can expect.
- Implement collapsible facet sections to keep the interface clean and manageable, especially on mobile devices.
- Allow shoppers to easily reset individual facets or all selected filters to start a new search.
