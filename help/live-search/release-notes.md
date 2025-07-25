---
title: "[!DNL Live Search] Release Notes"
description: "The latest release information for [!DNL Live Search] from Adobe Commerce."
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
---
# [!DNL Live Search] Release Notes

These release notes describe the latest versions of [!DNL Live Search].
Support is provided for the current major released version. Release notes for older versions are provided for reference.
Updates include:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues

## Hosted service updates

These notes describe updates that were published outside of a versioned release or improvements to the hosted service.

_April 29, 2025_

![Fix](../assets/fix.svg) Fixed an issue where the **Export to CSV** report on the [**Performance**](./performance.md) tab was not including all data specified in the date range.
![Fix](../assets/fix.svg) Fixed an issue where you could not save a [merchandising rule](./rules.md) if the search query filter was used.
![Fix](../assets/fix.svg) Fixed an issue where [pinned products](./facets-manage.md#pinunpin-facet) were not listed at the top of the results page.

_April 21, 2025_

![Fix](../assets/fix.svg) Fixed an issue with the range filter for prices so that products that are equal to the upper range are not included in the results. This change aligns with how price ranges are defined for facets.

_April 3, 2025_

![Fix](../assets/fix.svg) Updated the SaaS Data Export extension to remove the "Products must be assigned to the root category" [limitation](boundaries-limits.md#b2b-and-category-permissions) for B2B merchants. See [Manage the data export extension](../data-export/manage-extension.md) to learn how to update the SaaS Data Export extension to version 103.4.0+.

_February 20, 2025_

![New](../assets/new.svg) Commerce supports multi-word synonyms. [Learn more](synonyms-type.md#multi-word-synonym-behavior). Support for multi-word synonyms is only available after this February 20 release date. Any existing multi-word synonyms require a full reindex to work, which you can request by [creating a support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

_January 31, 2025_

![New](../assets/new.svg) There is a new data retention policy for unqueried catalog data in your testing environment. [Learn more](overview.md#catalog-data-retention-policy).

_September 19, 2024_

![New](../assets/new.svg) Released a beta version that supports three new search capabilities: layered, starts with, and contains. [Learn more](install.md#install-the-live-search-beta).

_September 4, 2024_

![Fix](../assets/fix.svg) Increased the maximum number of buckets that can be returned [within a facet](boundaries-limits.md#facets) to 100.

_August 7, 2024_

![Fix](../assets/fix.svg) Increased the maximum interval value, or price range for [price faceting](settings.md#price-faceting) from 10,000 to 40,000,000.

_February 13, 2024_

![New](../assets/new.svg) [!DNL Live Search] now supports setting a default rule for [Search Merchandising](rules.md).

_October 12, 2023_

![New](../assets/new.svg) Commerce administrators can now specify the language of the index for [!DNL Live Search]. See [Settings](settings.md).
![Fix](../assets/fix.svg) The "Search Rules" tab has been renamed to "Search Merchandising".

_June 13, 2023_

![Fix](../assets/fix.svg) Fixed an issue where some characters such as quotes or apostrophes caused ranking issues. Reindexing solves these issues.

_April 25, 2023_

![New](../assets/new.svg) [!DNL Live Search] customers can now take advantage of the new [SaaS price indexer](../price-index/price-indexing.md).

### PLP widget

_May 22, 2025_

![Fix](../assets/fix.svg) Fixed an issue where the Add to Cart button remained in English when the locale was changed to French, German, Italian or Spanish.
![Fix](../assets/fix.svg) Fixed an issue where the Add to Cart button was displayed for out-of-stock products.

_May 31, 2024_

![New](../assets/new.svg) Released version 2.0.0 of the PLP widget, which adds support for the following features:

- Add to Cart buttons - Available only for simple products.
- Multiple images per product - Image can change when a different color is chosen for a configurable product.

_October 27, 2023_

![New](../assets/new.svg) The [!DNL Live Search] PLP widget now supports color swatches.

## [!DNL Live Search] 4.4.0

_July 14, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Increased the [price grouping](./settings.md#price-faceting) limit from 50 to 100.

## [!DNL Live Search] 4.3.0

_March 11, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) [!DNL Live Search] now supports PHP 8.4 for installations running Adobe Commerce 2.4.8-beta2.
![Fix](../assets/fix.svg) Fixed an issue where the Search Adapter was not compatible with `psr/http-message:2.0`.

## [!DNL Live Search] 4.2.3

_February 13, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Fixed an issue where the order detail page was missing the order number, date, and the **[!UICONTROL Reorder]** button.

## [!DNL Live Search] 4.2.2

_January 6, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Fixed an issue that was causing an error with the `categoryList` GraphqL query on Adobe Commerce version 2.4.5 and earlier.

## [!DNL Live Search] 4.2.1

_July 31, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Fixed an issue where certain scripts were not loading on the checkout page.
![Fix](../assets/fix.svg) Fixed a dependency version in the `composer.json` file.

## [!DNL Live Search] 4.2.0

_May 31, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Updated Live Search extension to use PLP widgets version 2.0.0.

## [!DNL Live Search] 4.1.2

_May 16, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

### Updates

![Fix](../assets/fix.svg) Fixed the [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) GraphQL query to correctly filter based on the `categoryPath` and `categoryList` for categories.

## [!DNL Live Search] 4.1.1

_March 19, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

### New Features

![New](../assets/new.svg) Added language support for Polish.
![New](../assets/new.svg) [!DNL Live Search] now supports PHP 8.3 for installations running Adobe Commerce 2.4.4.

## [!DNL Live Search] 4.1.0

_February 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

### New Features

![New](../assets/new.svg) The [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) is now available. This revamped dashboard provides insights into data streams for [!DNL Product Recommendations], [!DNL Live Search], and [!DNL Catalog Service].

### Updates

![Fix](../assets/fix.svg) Fixed an issue that caused an error when guest users added products to a cart in non-default store views.
![Fix](../assets/fix.svg) Fixed an issue that caused the search popover to always display the currency symbol in front of the price value regardless of locale settings.
![Fix](../assets/fix.svg) Removed unnecessary type definitions for disabled core plugins to fix compatibility issues on installation.

## [!DNL Live Search] 4.0.0

_November 13, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

### New Features

![New](../assets/new.svg) [!DNL Live Search] now supports color swatches in the PLP widget.
![New](../assets/new.svg) [!DNL Live Search] now displays the category name rather than the category Id.
![New](../assets/new.svg) [!DNL Live Search] now supports strikethrough prices in the PLP widget.
![New](../assets/new.svg) Introduced the "Hide Filters" button to hide the filters panel.


### Updates

![Fix](../assets/fix.svg) The [!DNL Live Search] PLP widget is now enabled by default for new installations.
![Fix](../assets/fix.svg) The Search Adapter is deprecated. Going forward, the Search Adapter will only be updated to address security issues.
![Fix](../assets/fix.svg) Reconfigured CSS styles to better isolate widget classes.
![Fix](../assets/fix.svg) Minor bug fixes

After installing version 3.1.1 or higher, enable the new indexers: 

- Product Prices Feed
- Scopes website data feed
- Scopes customer groups data feed

After upgrading, test the updated configuration in QA or Staging before pushing the changes to production. 

+++3.1.1 and prior

### [!DNL Live Search] 3.1.1

_September 15, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) New Category Merchandising tab has been added. Users can now add Intelligent Rankings and Manual Rankings (pin, boost, bury, hide) per category
![New](../assets/new.svg) Users can add a single category rule with intelligent or manual ranking
![New](../assets/new.svg) Users can now add Intelligent Ranking rules to subcategories
![New](../assets/new.svg) Detailed information is provided when deleting subcategories with intelligent ranking
![New](../assets/new.svg) Added the ability to delete rules for inherited ranking strategies
![New](../assets/new.svg) Added the ability to delete rules for a single category
![New](../assets/new.svg) Users can now search by category name when adding a rule
![New](../assets/new.svg) With the Category Tree View, users can now view which category has rules applied.
![New](../assets/new.svg) Category Preview only shows the selected category.
![New](../assets/new.svg) AEM CIF [Popover widget](https://github.com/adobe/aem-cif-guides-venia/pull/319) and [PLP widget](https://github.com/adobe/aem-cif-guides-venia/pull/320) components allow AEM sites to take advantage of [!DNL Live Search].

#### Updates

![Fix](../assets/fix.svg) The table size of the Products and Price feeds have been greatly reduced. Tables `catalog_data_exporter_products` and `catalog_data_exporter_product_prices` should see a substantial size reduction.
![Fix](../assets/fix.svg) The 'Rules' tab is renamed to 'Search Rules'
![Fix](../assets/fix.svg) When ranking by 'trending', you can now choose between:
    - 3 days (default)
    - 14 days
    - 30 days
![Fix](../assets/fix.svg) 'Events' (Boost/Pin/Bury/Hide) has been renamed to 'Manual Ranking'
![Fix](../assets/fix.svg) 'Ranking Type' has been renamed to 'Intelligent ranking'
![Fix](../assets/fix.svg) Minor bug fixes

### [!DNL Live Search] 3.1.0

_September 1, 2023_

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

#### Updates

![Fix](../assets/fix.svg) The Product Listing widget has been updated to use the [Catalog Service API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).

### [!DNL Live Search] 3.0.2

_August 7, 2023_

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

#### New Features

![New](../assets/new.svg) The following values have been added to the `storeDetails` object:

- "Allow All Products per Page"
- Currency rate
- "Products per Page on Grid Allowed Values"
- "Products per Page on Grid Default Value"
- Store language

#### Updates

![Fix](../assets/fix.svg) Catalog Service modules have been added to the metapackage to support advanced data retrieval.
![Fix](../assets/fix.svg) The **My Account** page navigation no longer disappears when using the Product Listing Page widget.

Merchants must upgrade the [!DNL Live Search] extension version >= 3.0.2 to access these features.

It is recommended to upgrade and test before pushing to production. Consider upgrading the production environment during off-peak hours after verifying their testing environment results.

#### Limitations

Using the Live Search Product Listing Page widget causes Google Tag Manager to fail. Use the default Search Adapter if Google Tag Manager is needed.

### [!DNL Live Search] 3.0.1

_March 14, 2023_

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

#### New Features

![New](../assets/new.svg) Product Item Card in Rules preview 
![New](../assets/new.svg) [Product Listing Page widget](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![New](../assets/new.svg) [Category filtering options](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![New](../assets/new.svg) Added the ability to drag and drop to create Pin events
![New](../assets/new.svg) New Pin actions:
    - Pin to spot - Pin button to create Pin event with one click
    - Pin to top - Places product in the first position
    - Pin to bottom - Places the product at the bottom of the results
    - Unpin an event with one click
![New](../assets/new.svg) [Intelligent Ranking for rules](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
![New](../assets/new.svg) [!DNL Live Search] now supports full [Inventory Management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) capabilities in Commerce (formerly knows as Multi-Source Inventory, or MSI). To enable full support, you must [update](install.md#update) the dependency module `commerce-data-export` to version 102.2.0+.

#### Updates

![Fix](../assets/fix.svg) Configure Rules now automatically sorts positions uniquely
![Fix](../assets/fix.svg) Deleting an existing event now updates preview
![Fix](../assets/fix.svg) Rules with no events can be saved
![Fix](../assets/fix.svg) Remove faceting "Select Type" selector
![Fix](../assets/fix.svg) Added new "Editing" status for unsaved rules

#### Fixes

![Fix](../assets/fix.svg) Fixed server error when there is an unfinished event during save
![Fix](../assets/fix.svg) Fixed correctly deleting specific event when there are multiple events
![Fix](../assets/fix.svg) Fixed existing rule event not updating when new event has been added
![Fix](../assets/fix.svg) Fixed on second "Edit" click from details, [!DNL Live Search] page requiring reload
![Fix](../assets/fix.svg) Synonyms: Fixed an issue when a user clicked out of input, they could not return the focus to the field
![Fix](../assets/fix.svg) Other minor bug fixes and performance updates
![Bug](../assets/bug.svg) - Ranking by "Recommended for you" is only supported within the Live Search widgets. It is not supported with the default Luma and PWA search functionality.
![Bug](../assets/bug.svg) - Custom price attribute facets do not render correctly in Luma, but the API properly filters on them.

Merchants must upgrade the [!DNL Live Search] extension version >= 3.0.1 to access these features.

It is recommended to upgrade and test before pushing to production. Consider upgrading the production environment during off-peak hours after verifying their testing environment results.

### [!DNL Live Search] 2.0.5

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) - Live Search would throw an error when SDK resources were not available due to network issues. This bug is fixed.

Merchants must upgrade the Live Search extension version >= 2.0.5 to access these features.

It is recommended to upgrade and test before pushing to production. Consider upgrading the production environment during off-peak hours after verifying their testing environment results.

### [!DNL Live Search] 2.0.4

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Live Search now supports filtering by the 'Display Out of Stock Products' setting in the admin. If 'Display Out of Stock Products' is set to false, `inStock = true` is added to the filter.
![Fix](../assets/fix.svg) To improve performance, the 'Suggestions' block has been removed from the Live Search popup. The data is still passed through GraphQL, in case you want to replace the feature.
![Fix](../assets/fix.svg) `categories` and `categoryPath` have replaced `categoryIds` for category filtering. Read more in the [productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) topic.
![Fix](../assets/fix.svg) Previously, a user tied to a B2B company would receive an incorrect Customer Group Code when doing searches. Live Search now returns the correct value.
![Fix](../assets/fix.svg) Previously, when searching for a term that does not exist, Live Search would return an error. That bug is now fixed.

Merchants must upgrade the [!DNL Live Search] extension version >= 2.0.4 to access these features.

Users are advised to upgrade and test before pushing to production. Consider upgrading the production environment during off-peak hours after verifying their testing environment results.

### [!DNL Live Search] 2.0.3

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Live Search now supports B2B features by honoring category permissions, shared catalogs, and customer group-specific pricing.

Merchants must upgrade the [!DNL Live Search] extension version >= 2.0.3 to access these features.

Users are advised to upgrade and test before pushing to production. Consider upgrading the production environment during off-peak hours after verifying their testing environment results.

### [!DNL Live Search] 2.0

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

Existing [!DNL Live Search] installations must be upgraded to [!DNL Live Search] 2.0.0 to take advantage of the following new features, fixes, and improvements:

![New](../assets/new.svg) [!DNL Live Search] now supports PHP 8.1 for installations running Adobe Commerce 2.4.4.
![New](../assets/new.svg) The `Magento_ElasticsearchCatalogPermissionsGraphQl` module is added to the list of modules that are disabled during the installation.
![New](../assets/new.svg) The number of available lines in the [[!DNL storefront popover]](overview.md) can be configured from the *Admin*.
![New](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/) supported for [!DNL Live Search].
![New](../assets/new.svg) The [!DNL Live Search] installation process is updated with advanced process changes.
![Fix](../assets/fix.svg) [Advanced Search](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) link removed from the storefront footer.
![Bug](../assets/bug.svg) The following product attributes are not supported by [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) when used in relation to the beta release of PWA: `description`, `name`, `short_description`
![Bug](../assets/bug.svg) The beta release of PWA for [!DNL Live Search] does not support [event handling](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/).

### [!DNL Live Search] 1.3.1

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) [Custom price attribute](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) no longer returns an error when configured as a [facet](facets-add.md).
![Fix](../assets/fix.svg) Fixed issue that caused an error to occur when no [currency symbol](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`) is available.
![Fix](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) now shows the [Special Price](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) (minimum final price) when available.

### [!DNL Live Search] 1.3.0

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) [Performance](performance.md) reporting dashboard provides insight into search terms that shoppers use.
![New](../assets/new.svg) [!DNL Live Search] [Storefront Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) provides access to a common data layer with event publishing and subscription services, and metrics.
![Fix](../assets/fix.svg) The [[!DNL Storefront popover]](storefront-popover.md) has a new `active` class for the `.search-autocomplete` container that controls visibility.
![Fix](../assets/fix.svg) In the storefront, the [Search Terms](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) footer link is removed and its cache disabled for [!DNL Live Search] installations.
![Bug](../assets/bug.svg) Patch for Search Adapter handles duplicate products.
![Bug](../assets/bug.svg) [!DNL Live Search] supports [single-source](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage) (physical) inventory locations with multiple (virtual) [stocks](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage). Multiple inventory sources are not supported now.

### [!DNL Live Search] 1.2.0

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) displays suggested products and thumbnail images of top search results as shoppers type queries into the Search box.
![New](../assets/new.svg) Commerce *Admin* session stays open during extended periods of keyboard inactivity
![New](../assets/new.svg) [!DNL Live Search] is automatically enabled after onboarding
![Fix](../assets/fix.svg) Initial indexing time is less than an hour
![Fix](../assets/fix.svg) Incremental product updates near real time (after install and setup)
![Fix](../assets/fix.svg) Sortable columns in Synonym editor
![Fix](../assets/fix.svg) [!DNL Live Search] no longer throws an error if search criteria contains empty sort order value
![Fix](../assets/fix.svg) Range filtering no longer breaks if attribute codes contain strings "to" or "from"

### [!DNL Live Search] 1.1.0

[!BADGE Supported]{type="Informative" tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Bug](../assets/bug.svg) The [!DNL Live Search] service supports only the [base currency](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) of the Adobe Commerce installation.
![Bug](../assets/bug.svg) When adding a facet, the Product Attributes Feed does not update correctly when set to `Update on Save`. To avoid this problem, go to [Index Management](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) and set Product Attributes Feed to `Update by Schedule`.
![Bug](../assets/bug.svg) [!DNL Live Search] synonyms are defined per store view, but are currently stored per website and identified with a combination of `environmentId` and `storeViewCode`. As a result, all websites and store views within the Adobe Commerce installation share synonyms. The most recently created set of synonyms for the store view takes precedence.
![Bug](../assets/bug.svg) If a synonym term contains multiple words, each word is treated as a separate synonym. For example, if you define "time piece" as a synonym of "watch", both "time" and "piece" are treated as synonyms of watch.

+++

## Documentation

To learn more:

- [Adobe Commerce Developer Documentation](https://developer.adobe.com/commerce/docs)
- [Adobe Commerce User Guide](https://experienceleague.adobe.com/en/docs/commerce)
- [[!DNL Live Search] on Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)
