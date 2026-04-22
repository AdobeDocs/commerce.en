---
title: Log code reference
description: Reference list of log codes emitted by the [!DNL data export] extension, with messages and log levels for system integrators.
feature: Services
exl-id: c1341863-1ec4-4d67-8ff2-821ef0a61f33
---
<!--
Source of truth: https://github.com/magento-commerce/commerce-data-export (docs/log-codes.md)
When log codes, messages, or log levels change in that repository, update this page to match.
Only columns retained here: Log Code, Message, Level. File paths are intentionally omitted.
-->

# Log code reference

This page lists log codes emitted by the [!DNL data export] extension. Codes are assigned only to `error`, `warning`, and `critical` level log messages.

See [Review logs and troubleshoot](troubleshooting-logging.md) for information about log files, and troubleshooting guidance.

## Group 01 - Data Collection Phase

Errors or warnings during data collection, typically in data providers.
Affected entities will be processed with partial data or not processed on error. See details in error message.
Warnings may suggest about wrong integration with Data Exporter Extension from 3rd party modules, but sync should not be blocked.

| Log Code  | Level   | Message |
|-----------|---------|---------|
| CDE01-01 | error   | `CDE01-01 Was not able to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-02 | warning | `CDE01-02 Field "{field}" is missing in row {row_data}` |
| CDE01-03 | warning | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` |
| CDE01-04 | error   | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-05 | error   | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` |
| CDE01-06 | error   | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` |
| CDE01-07 | error   | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` |
| CDE01-08 | error   | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` |
| CDE01-09 | error   | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` |
| CDE01-10 | error   | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` |
| CDE01-11 | error   | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` |
| CDE01-12 | warning | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` |
| CDE01-13 | error   | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` |
| CDE01-14 | error   | `CDE01-14 Failed to assign UUID for type: {type}, ids: {ids}` |
| CDE01-15 | error   | `CDE01-15 Failed to assign UUID for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | error   | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |

## Group 02 - Sending Data to SaaS Phase

Errors during HTTP submission of feed data to SaaS endpoints.

| Log Code  | Level   | Message |
|-----------|---------|---------|
| CDE02-01 | error   | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | error   | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | warning | `CDE02-03 Cannot parse response. API request was not successful.` |
| CDE02-04 | error   | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | error   | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | error   | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | warning | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | warning | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | error   | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | warning | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | warning | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | error   | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |

## Group 03 - Scheduling Sync or Triggering Sync on Entity Update

Errors when scheduling or triggering sync in response to entity changes. Usually need to run full resync to recover.

| Log Code  | Level    | Message |
|-----------|----------|---------|
| CDE03-01 | error    | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | warning  | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | error    | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | error    | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | error    | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | error    | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | error    | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | error    | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | warning  | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs or wrong identifier type specified` |
| CDE03-10 | warning  | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` |
| CDE03-11 | error    | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` |
| CDE03-12 | warning  | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` |
| CDE03-13 | error    | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` |
| CDE03-14 | error    | `CDE03-14 Failed to read config values. Indexer invalidation for event "{event_name}" skipped. Error: {error_message}` |
| CDE03-15 | error    | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` |
| CDE03-16 | error    | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` |
| CDE03-17 | critical | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` |
| CDE03-18 | critical | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` |
| CDE03-19 | error    | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` |
| CDE03-20 | error    | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` |

## Group 04 - Status Admin Grid UI Related Errors

Errors occurring in the Feed Status admin grid UI components.

| Log Code  | Level | Message |
|-----------|-------|---------|
| CDE04-01 | error | `CDE04-01 Error on getting indexer status for feed "{feed_name}". Error: {error_message}` |

## Group 05 - Unexpected Error, Functionality Not Impacted

Unexpected errors that do not block the main sync flow.

| Log Code  | Level   | Message |
|-----------|---------|---------|
| CDE05-01 | warning | `CDE05-01 Was not able to serialize metadata after sync. Error: {message}` |
| CDE05-02 | error   | `CDE05-02 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE05-03 | warning | `CDE05-03 Failed to check indexer type when setting schedule mode: {message}` |
| CDE05-04 | warning | `CDE05-04 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE05-05 | warning | `CDE05-05 Identifier for feed item is empty. Skip sync for entity` |
| CDE05-06 | warning | `CDE05-06 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE05-07 | warning | `CDE05-07 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE05-08 | warning | `CDE05-08 GiftCard {sku} does not have shopper input options` |
| CDE05-09 | warning | `CDE05-09 GiftCard {sku} doesn't have valid options: {options}` |
| CDE05-10 | warning | `CDE05-10 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |
| CDE05-11 | warning | `CDE05-11 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |

## Group 06 - General Errors Related to Indexation or Configuration

Errors during the indexation process or due to misconfiguration.

| Log Code  | Level   | Message |
|-----------|---------|---------|
| CDE06-01 | error   | `CDE06-01 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE06-02 | warning | `CDE06-02 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE06-03 | error   | `CDE06-03 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE06-04 | error   | `CDE06-04 Cannot load feed indexer for feed` |
| CDE06-05 | error   | `CDE06-05 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE06-06 | error   | `CDE06-06 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE06-07 | error   | `CDE06-07 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE06-08 | error   | `CDE06-08 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE06-09 | error   | `CDE06-09 Error during full sync. Message: "{message}". Skipped IDs: [{ids}]` |
| CDE06-10 | warning | `CDE06-10 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE06-11 | warning | `CDE06-11 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE06-12 | error   | `CDE06-12 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE06-13 | error   | `CDE06-13 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
