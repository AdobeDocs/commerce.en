---
title: "[!Data Export] Log Codes Reference"
description: Reference list for data export log codes, messages, and severity levels to troubleshoot sync issues and decide when a partial or full resync is required.
feature: Services
exl-id: c1341863-1ec4-4d67-8ff2-821ef0a61f33
---

# [!DNL Data Export] log codes reference

<!--
Source of truth: https://github.com/magento-commerce/commerce-data-export (docs/log-codes.md)
When log codes, messages, or log levels change in that repository, update this page to match.
Only columns retained here: Log Code, Message, Level. File paths are intentionally omitted.
-->

This page provides a reference for Data Export log messages to help troubleshoot synchronization issues and determine when a partial or full resync is required. It includes only error, warning, and critical log codes emitted by the [!DNL Data Export] extension.

See [Review logs and troubleshoot](troubleshooting-logging.md) for information about log files and troubleshooting guidance.

## Group 01 - Data Collection Phase

Log codes related to errors or warnings that occur while collecting data from source entities, typically within data providers.
- Affected entities might be processed with partial data or skipped entirely if an error occurs. See the log message for details.
- Warnings can indicate incorrect integration with the Data Export extension by third-party modules; however, sync operations typically continue.

| Log Code  | Level   | Message |
|-----------|---------|---------|
| CDE01-01 | error   | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
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
| CDE01-14 | error   | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` |
| CDE01-15 | error   | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | error   | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |
| CDE01-17 | warning | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE01-18 | warning | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE01-19 | warning | `CDE01-19 GiftCard {sku} does not have shopper input options` |
| CDE01-20 | warning | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` |
| CDE01-21 | error   | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` |
| CDE01-22 | error   | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` |

## Group 02 - Sending Data to SaaS Phase

Log codes related to errors or warnings that occur while submitting feed data to SaaS endpoints.
- Errors typically indicate failures during HTTP requests, response handling, or data validation that prevent data from being accepted.
- Warnings usually indicate transient conditions (such as rate limiting or server errors) where requests are retried automatically.

| Log Code  | Level   | Message |
|-----------|---------|---------|
| CDE02-01 | error   | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | error   | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | warning | `CDE02-03 Cannot parse the API response because the request was not successful.` |
| CDE02-04 | error   | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | error   | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | error   | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | warning | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | warning | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | error   | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | warning | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | warning | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | error   | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |
| CDE02-13 | warning | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |

## Group 03 - Scheduling Sync on Entity Update

Log codes related to errors or warnings that occur when scheduling or triggering synchronization in response to entity changes.
- Errors can prevent incremental synchronization from being scheduled and often require a full or partial resync to recover.
- Warnings indicate that a sync operation was skipped or deferred due to unsupported input, missing identifiers, or configuration issues.

| Log Code  | Level    | Message |
|-----------|----------|---------|
| CDE03-01 | error    | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | warning  | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | error    | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | error    | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | error    | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | error    | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | warning  | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | error    | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | warning  | `CDE03-09 The "{feed_name}" feed does not support partial resync by IDs, or an unsupported identifier type was specified.` |
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

## Group 04 - General Errors Related to Indexation or Configuration

Log codes related to errors during the indexation process or due to misconfiguration.

| Log Code  | Level   | Message |
|-----------|---------|---------|
| CDE04-02 | error   | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE04-03 | warning | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE04-04 | error   | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE04-05 | error   | `CDE04-05 Cannot load feed indexer for feed` |
| CDE04-06 | error   | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE04-07 | error   | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE04-08 | error   | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE04-09 | error   | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE04-10 | error   | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` |
| CDE04-11 | warning | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE04-12 | warning | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE04-13 | error   | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE04-14 | error   | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
| CDE04-15 | warning | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` |
| CDE04-16 | warning | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE04-17 | warning | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` |
| CDE04-18 | warning | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE04-19 | warning | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` |
| CDE04-20 | warning | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |
