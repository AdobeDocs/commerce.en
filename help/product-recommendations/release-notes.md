---
title: "[!DNL Product Recommendations] Release Notes"
description: "The latest release information for [!DNL Product Recommendations] from Adobe Commerce."
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
---
# [!DNL Product Recommendations] Release Notes

The release notes contain updates to the following [!DNL Product Recommendations] modules:

* [!DNL Product Recommendations] metapackage: `magento/product-recommendations`
* Page Builder support in [!DNL Product Recommendations] (optional) module: `magento/module-page-builder-product-recommendations`
* Visual similarity recommendation type support for [!DNL Product Recommendations] (optional) module: `magento/module-visual-product-recommendations`

Support is provided for the current major released version. Release notes for older versions are provided for reference.
The release notes include:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues

See the developer documentation to [learn about product support](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Hosted service updates

These notes describe updates or known issues that were published or discovered outside of a versioned release or improvements to the hosted service.

_January 31, 2025_

![New](../assets/new.svg) There is a new data retention policy for unqueried catalog data in your testing envionment. [Learn more](overview.md#catalog-data-retention-policy).

_June 28, 2024_

![Bug](../assets/bug.svg) Products added to the cart from a [!DNL Product Recommendations] unit on the cart page are not removed from the list of recommended products when the cart page reloads.
![Bug](../assets/bug.svg) Products removed from the cart continue to persist in the `cartSkus` array until the cart page reloads.

_July 18, 2023_

![New](../assets/new.svg) [!DNL Product Recommendations] now has a GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) query.

_April 25, 2023_

![New](../assets/new.svg) [!DNL Product Recommendations] customers can now take advantage of [SaaS price indexing](../price-index/price-indexing.md).

## Current major version

### 6.2.1 of magento/product-recommendations

_July 14, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Made improvments to the [preview recommendations](./create.md#preview-recommendations) panel.

### Previous versions

### 6.2.0 of magento/product-recommendations

_April 4, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Updated the CDN URLs for the `recommendations-admin-ui` to  the `adobe.io` domain.

### 6.1.0 of magento/product-recommendations

_March 11, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added PHP 8.4 support.

### 6.0.3 of magento/product-recommendations

_November 6, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Fixed an issue where the [category filter](filters.md#category) included categories that did not belong to the current storeview.
![Fix](../assets/fix.svg) Fixed a dependency issue in the `magento/product-recommendations` metapackage.

### 6.0.2 of magento/product-recommendations

_May 9, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Fixed an issue where clicking the **[!DNL Add to Cart]** button on a simple product inside a Product Recommendations unit redirected the shopper to the home page rather than staying on the current page.
![Bug](../assets/bug.svg) There is a validation error caused by the `referenceBlock` element in the `ProductRecommendations Layout` XML file.

### 6.0.1 of magento/product-recommendations

_March 19, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added PHP 8.3 support.

### 6.0.0 of magento/product-recommendations

_February 22, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) The [!DNL Catalog Sync Dashboard] is now the [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). This revamped dashboard provides insights into data streams for [!DNL Product Recommendations], [!DNL Live Search], and [!DNL Catalog Service].
![Fix](../assets/fix.svg) Fixed an issue that caused checkout errors for [!DNL Product Recommendations].

+++5.0.0 and prior

### 5.0.1 of magento/product-recommendations

_September 15, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added new modules to support the [Saas Price Indexer](../price-index/price-indexing.md).
![New](../assets/new.svg) Added new data export modules to support exporting more product types including bundled products and gift cards.
![Fix](../assets/fix.svg) The table size of the Products and Price feeds have been greatly reduced. Tables `catalog_data_exporter_products` and `catalog_data_exporter_product_prices` should see a substantial size reduction.

#### Known limitations

* The `websiteCode` value is incorrectly returned if it contains an underscore (_).

### 5.0.0 of magento/product-recommendations

_March 20,2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Updated [!DNL Product Recommendations] to support Adobe Commerce 2.4.6.
![New](../assets/new.svg) This is a major version release. [Edit](install-configure.md#update) the root `composer.json` file for your project. 
![New](../assets/new.svg) [!DNL Product Recommendations] now supports full [Inventory Management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) capabilities in Commerce (formerly knows as Multi-Source Inventory, or MSI). To enable full support, you must [update](install-configure.md#update) the dependency module `commerce-data-export` to version 102.2.0+.

### 4.0.1 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg) Previously, [!DNL Product Recommendations] would show an error when the display currency was switched to a non-default currency. Switching currencies now works properly.

### 4.0.0 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg) Added [readiness indicators](create.md) to help you visualize the training progress of each recommendation type.
![New](../assets/new.svg) This is a major version release. [Edit](install-configure.md#update) the root `composer.json` file for your project. This release also requires you to provide two API keys when installing and configuring [!DNL Product Recommendations]: [a production key and a sandbox key](../landing/saas.md).

#### Known limitations

* The `websiteCode` value is incorrectly returned if it contains an underscore (_).

### 3.3.7 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added PHP 8.1 support
![New](../assets/new.svg) Improved image resizing so that images sizing is handled more consistently in the reference display template

### 3.3.6 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Optimized [!DNL Product Recommendations] metapackage by explicitly listing the dependencies

### 3.3.5 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added [B2B support](onboarding.md#b2bsupport) in [!DNL Product Recommendations]
![New](../assets/new.svg) Added new feeds to [sync catalog data](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) to Commerce Services via the command line

### 3.3.3 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added new [recommendation types](type.md): Conversion (view to cart), Conversion (view to purchase), and Recently viewed. These new recommendation types are available in the `magento/product-recommendations` module 3.2.2 and later.
![Fix](../assets/fix.svg) Fixed an issue where Fastly's Web Application Firewall (WAF) was incorrectly blocking a cookie
![Fix](../assets/fix.svg) Fixed issue where products assigned to the non-default Store View were not being displayed in the _Recommendations Product Preview_ panel when creating a recommendation for that specific Store View
![Fix](../assets/fix.svg) Fixed issue where certain recommendation unit names in Page Builder prevented the recommendation unit to display on the storefront

### 3.3.2 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Fixed missing dependency for B2B support

### 3.3.1 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added support for B2B customer group pricing. When you set a [price filter](filters.md) on a recommendation unit, B2B customers who are logged in see the customer group pricing set for the products displayed.

### 3.3.0 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added support for Adobe Client Data Layer to standardize behavioral data collection across Adobe Commerce features and services. See the [readme](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md) to learn more.

### 3.2.6 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Fixed a JavaScript modal error
![Fix](../assets/fix.svg) Fixed an issue where Fastly's Web Application Firewall (WAF) was incorrectly blocking a cookie

### 3.2.5 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Renamed Magento Services to [Commerce Services](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) and improved usability in the Admin

### 3.2.4 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Fixed the "Unable to retrieve configurable product options data" error when indexing product attributes

### 3.2.3 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Fixed the "Unable to retrieve configurable product options data" error during Catalog Sync
![Fix](../assets/fix.svg) Fixed an issue where the store code was not being set correctly when you enabled the "Add store code to URL" configuration
![Fix](../assets/fix.svg) Improved detection of Admin Panel configuration changes to ensure that these changes are reflected in Catalog Sync data

### 3.2.2 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added the ability to [preview recommendation results](create.md) at creation time. This might require that you update your module to the latest version.
![New](../assets/new.svg) Added the ability to [monitor and manage](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) the catalog sync process from the Admin.
![New](../assets/new.svg) Added [filters](filters.md) to control which products are displayed in recommendations.
![New](../assets/new.svg) Added the [Visual similarity](type.md#visualsim) recommendation type.

### 1.2.1 of magento/module-page-builder-product-recommendations for Page Builder

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added support for the 3.2.0+ version of the `magento/product-recommendations` module

### 3.1.0 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added the ability to [resync](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) your catalog to SaaS services via command line.
![New](../assets/new.svg) Added support for database table prefixes
![Fix](../assets/fix.svg) Removed PHP 7.1 support

### 3.0.8 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Fixed an issue where events were sent for data collection before the module was configured, causing invalid traffic

### 3.0.6 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) **(Beta)** Includes support for new [Visual similarity](type.md#visualsim) recommendation type.

### 1.0.0 of magento/module-visual-product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) **(Beta)** [Visual similarity](type.md#visualsim). With the _Visual similarity_ recommendation type, you can deploy a recommendation unit to your product detail page that displays products that are visually similar to the product being viewed.

### 3.0.5 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Fixed the "Unable to retrieve product options data" error that could occur during catalog export.
![Fix](../assets/fix.svg) The currency symbol in the _Revenue_ column on the _[!DNL Product Recommendations]_ dashboard now correctly reflects the configured base currency.

### 3.0.4 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Added support for Adobe Commerce 2.4.0

### 3.0.3 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![Fix](../assets/fix.svg) Improved symbol implementation in storefront template

### 1.0.4 of magento/module-page-builder-product-recommendations for Page Builder

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added Product Recommendation name when editing the Page Builder content type

### 3.0.2 magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Added a status column on the grid when selecting Recommendation units in Page Builder
![Fix](../assets/fix.svg) Fixed an issue with incorrect http/https protocols in product and image URLs

### 3.0.1 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

This is a major version release. [Edit](install-configure.md#update) your project's root composer.json file.

![New](../assets/new.svg) Fetch [!DNL Product Recommendations] from alternate SaaS Data Spaces. This allows you to use [!DNL Product Recommendations] computed in your product environment on other, non-production environments. [Switching SaaS Data Spaces](settings.md) further describes this feature.

![Fix](../assets/fix.svg) Fixed an issue where checkout was inhibited for shoppers using uBlock Origin
![Fix](../assets/fix.svg) Fixed an issue sending extraneous add-to-cart events

### 1.0.3 of magento/module-page-builder-product-recommendations for Page Builder

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) Page Builder support. With the Page Builder integration, you can accurately and granularly place Recommendation units in any arbitrary location on Page Builder-authored content. You can also style the headings and recommendation units themselves. Go to [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) for more information.

### 2.0.0 of magento/product-recommendations

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.x and newer

![New](../assets/new.svg) General availability release!

+++

## Documentation

To learn more about [!DNL Product Recommendations] and [!DNL Product Recommendations] development:

* [User Guide](overview.md)
* [Developer Documentation](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
