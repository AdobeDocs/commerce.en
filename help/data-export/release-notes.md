---
title: '[!DNL SaaS Data Export Extension] Release Notes'
description: The latest release information for [!DNL Data Export Extension] for Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
---
# [!DNL SaaS Data Export] Extension Release Notes

These release notes describe the latest versions of the [!DNL SaaS data export] extension. Support is provided for the current major released version. Release notes for older versions are provided for reference.

Updates include:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues


>[!NOTE]
>
>The SaaS data export extension is a collection of modules that is installed automatically with Live Search, Product Recommendations, and the Catalog Service. You can check the version installed on your system using Composer. In some cases, you might want to upgrade the data export extension on your system to pick up fixes or new capabilities without updating the Commerce Service version.

## Current major version

## 103.4.7 Release

![Fix](../assets/fix.svg) Removed obsolete tables that stored category permissions for products. <!--MDEE-1065-->

## 103.4.6 Release

![Fix](../assets/fix.svg) Export Adobe Commerce downloadable product data using the `ac_downloadable` attribute for use with Adobe Commerce Optimizer.. <!--MDEE-1043-->
![Fix](../assets/fix.svg) Critical installation error fix for Adobe Commerce version 2.4.4. <!--MDEE-1074-->

## 103.4.5 Release

![New](../assets/new.svg) SaaS data export now supports the Adobe Commerce `giftcard` product type. In the data feed, Gift card products are exported as simple products with the product attribute type `ac_giftcard`. <!--MDEE-1042-->
![Fix](../assets/fix.svg)  Improved data export error reporting. Logs now include more detailed error messages, including original technical details to make it easier to debug and trace errors. <!--MDEE-1064-->

## 103.4.4 Release

![New](../assets/new.svg) Added a warning message that displays when the `cleanup-feed` argument is added to the `saas:resync` CLI command. The `--cleanup-feed` option should be used cautiously and only in specific scenarios like after environment cleanup or with the `--dry-run` option. Using it in other cases can lead to data loss and sync issues. <!--MDEE-1047-->
![Fix](../assets/fix.svg) Added the `x-request-id` from the server response for improved traceability. <!--MDEE-1041-->
![Fix](../assets/fix.svg) Fixed an issue where the synchronization status was not saved for the entire feed batch, which led to unnecessary resynchronization. <!--MDEE-1049-->
![Fix](../assets/fix.svg) Fixed an issue where all feeds in the feed batch were skipped during synchronization if one feed contained an error. <!--MDEE-976-->
![Fix](../assets/fix.svg) Added support for dimensions in the category permissions indexer. <!--MDEE-654-->

## 103.4.3 Release

![Fix](../assets/fix.svg) Resolved an issue where products were skipped during the data export process due to missing EAV attributes. <!--MDEE-970-->

## 103.4.2 Release

![Fix](../assets/fix.svg) Added the ability to collect entity payloads in the `saas-export.log` when running the test resynchronization using the `saas:resync --dry-run` command with the  `EXPORTER_EXTENDED_LOG=1` environment variable. <!--MDEE-1023-->

## 103.4.1 Release

![Fix](../assets/fix.svg) Added a prefix to QueryXml cache keys to prevent naming conflicts with other modules. <!--MDEE-1019-->

## 103.4.0 Release

![Fix](../assets/fix.svg) The product overrides feed no longer sends permissions if the product is not assigned to a category.<!--MDEE-449-->

## 103.3.21 Release

![Fix](../assets/new.svg) Added functionality to partially synchronize `products`, `productOverrides`, and `productAttributes` feeds  based on a specified list of product SKUs. Use the new functionality by adding the `--by-ids` option to the resync CLI command: <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![Fix](../assets/fix.svg) Reduced potential compatibility issues with PHP 8.4 by addressing deprecated functionality. <!--MDEE-1002-->

## 103.3.20 Release

![Fix](../assets/fix.svg) Fixed untraceable `BulkException` errors in the `cron.log` by improving messaging for errors related to Catalog Data Export cron job failures.<!--MDEE-966-->
![Fix](../assets/fix.svg) Improved performance of the product re-synchronization process on instances with a high number of store views. <!--MDEE-974-->

## 103.3.19 Release

![Fix](../assets/fix.svg) Updated the data export extension to improve feeds extensibility. <!--MDEE-936-->
![Fix](../assets/fix.svg) The data export processor now verifies the indexer status before a full resync to avoid accidental data loss in the feed table.

## 103.3.18 Release

![Fix](../assets/fix.svg) Staging updates for product and category entities are now triggered correctly on Data Export data updates.<!--MDEE-963-->

## 103.3.17 Release

![Fix](../assets/fix.svg) Added compatibility for PHP 8.4. <!--MDEE-941-->

## 103.3.16 Release

![Fix](../assets/fix.svg) Option values can be empty for configurable products for multiple store views. <!--MDEE-926-->

## 103.3.15 Release

![Fix](../assets/fix.svg) Ensured stable operation of integration tests on older configurations. <!--MDEE-869-->
![Fix](../assets/fix.svg) Stop propagating unnecessary attribute options. <!--MDEE-882-->
![Fix](../assets/fix.svg) Fixed the error message sent to the data export log when data serialization fails. <!--MDEE-913-->
![Fix](../assets/fix.svg) Enhanced the reliability of simple product updates with additional test coverage. <!--MDEE-886-->

## 103.3.14 Release

![Fix](../assets/fix.svg)  The exporter indexer now maintains the correct status for dependent indexers. Previously, these indexes were incorrectly invalidated and required additional checks and validation that slowed indexing performance. <!--MDEE-866-->

## 103.3.13 Release

![Fix](../assets/fix.svg) Improved performance of the data synchronization process by adding a local cache for attribute options data.<!--MDEE-864-->

## 103.3.12 Release

![Fix](../assets/fix.svg) Resolved an issue that increased synchronization time for simple and virtual products. <!--MDEE-861-->

## 103.3.11 Release

![Fix](../assets/fix.svg) The data export service now sends special price data for bundle products as a percentage, correcting a previous issue where it was sent as a final price. <!--MDEE-854-->
![Fix](../assets/fix.svg) Updated the monolog implementation for compatibility with Monolog 3. <!--MDEE-858-->

## 103.3.10 Release

![Fix](../assets/fix.svg) Fixed Multiple storeview filtration for the product custom options feed. <!--MDEE-842-->
![Fix](../assets/fix.svg) Invalid feeds are not resubmitted until the feed's hash value has changed.<!--MDEE-848-->

## 103.3.9 Release

![Fix](../assets/fix.svg) When an entity is deleted, the `deleted` flag is now propagated for the scoping service feeds for website (`scopesWebsite`) and customer group (`scopesCustomerGroup`).<!--MDEE-839-->

## 103.3.8 Release

![Fix](../assets/fix.svg) Disabled configuration options are no longer exported as active options.<!--MDEE-812-->
![Fix](../assets/fix.svg) Options and values are now updated on a configurable product when changes are made to a child product. <!--MDEE-835-->
![New](../assets/new.svg) Added the ability to include additional system attribute data in the product attributes feed.

## 103.3.7 Release

![Fix](../assets/fix.svg) Removed unnecessary dependencies from the InventoryDataExporter module.
![Fix](../assets/fix.svg) Changed required versions for inventory modules included in the CatalogInventoryDataExporter module to support Adobe Commerce version 2.4.4.

## 103.3.6 Release

![Fix](../assets/fix.svg) Fixed deadlocks that occurred during feed reindexing in multi-thread mode. Queries are now separated into Insert and Update operations.
![Fix](../assets/fix.svg) Optimized the Prices query for large catalogs with many websites.
![New](../assets/new.svg) Added retry logic to re-run failed transactions when deadlocks occurs.

## 103.3.5 Release

![Fix](../assets/fix.svg) Set dependency for latest compatible data export version for the SaaS common module.

![Fix](../assets/fix.svg) Replaced `ScopeConfig` instance with `ServiceConfigInterface` to support different service configurations.

## 103.3.4 Release

![Fix](../assets/fix.svg) Added support for data transfer audit logging by adding a mechanism to dispatch a `data_sent_outside` event each time data is transmitted from the Commerce instance to a Commerce service  <!--MDEE-785-->

## 103.3.3 Release

![New](../assets/new.svg) SaaS data export now caches Entity-Attribute-Value (EAV) attributes for the attribute metadata query.

![Fix](../assets/fix.svg) Fixed an issue where the `InventoryStockStatus` feed was not saved on retry if product was deleted.

## 103.3.2 Release

![Fix](../assets/fix.svg) Fixed an issue where the `modifiedAt` field was missing from removed entities feeds.

## 103.3.1 Release

![Fix](../assets/fix.svg) Fixed an issue that caused an `Invalid Template File` message to appear during products feed reindexing when Page Builder is installed.

## 103.3.0 Release

![New](../assets/new.svg) Migrated immediate export feed tables to the unified structure:
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![New](../assets/new.svg) Migrated catalog and inventory feeds to the immediate export solution.

![New](../assets/new.svg) Renamed immediate export feed cron-jobs to `*_feed_resend_failed_items`.

![New](../assets/new.svg) Renamed immediate export feeds, indexer view IDs, and change log tables.
- feed tables (and indexer view IDs):
  - `catalog_data_exporter_products` -> `cde_products_feed`
  - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
  - `catalog_data_exporter_categories` -> `cde_categories_feed`
  - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
  - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
  - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- change log table names - Follows the same naming pattern as the feed tables but change log table names add a `_cl` suffix.  For example `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
If you have custom code that references any of these entities, update the references with the new names to ensure that your code continues to function correctly.

![Fix](../assets/fix.svg) Set `modified_at` field in feed data only for feeds that require it.

![Fix](../assets/fix.svg) Modify the `productAttributes` query to retrieve only product attributes.

## 103.2.6 Release

![Fix](../assets/fix.svg) Fixed an issue that prevented feeds from being reindexed when tables have a prefix.

## 103.2.5 Release

![Fix](../assets/fix.svg) Optimized the Price query.

## 103.2.4 Release

![Fix](../assets/fix.svg) Fixed incorrect Stock status that displayed for a product when Commerce Inventory Management is enabled.

## 103.2.3 Release

![Fix](../assets/fix.svg) Fixed website level special pricing.
![Fix](../assets/fix.svg) Added mutex for all feeds that are processed.


## 103.2.2 Release

![Fix](../assets/fix.svg) Improved feeds batching strategy for large catalogs. The batches table is now filled with a limited number of IDs to reduce memory usage.

![Fix](../assets/fix.svg) Eliminated hard dependency of CommerceInventoryDataExporter to MSI modules.

![Fix](../assets/fix.svg) Improved `commerce-data-exporter` logs to collect more information and organize by different exporting stages.

## 103.2.1 Release

- Released updated version.

## 103.2.0 Release

- Added multi-thread data sync for products and prices.
