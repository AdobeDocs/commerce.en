---
title: Review logs and troubleshoot
description: Learn how to troubleshoot [!DNL data export] errors using the data-export and saas-export logs.
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
---
# Review logs and troubleshoot

The [!DNL data export] extension provides logs to track data collection and synchronization processes.

## Logs

Logs are available in the `var/log` directory on the Commerce application server.

| log name | filename | description |
|-----------------| ----------| -------------|
| SaaS data export log |`commerce-data-export.log` | Provides information about data export activities, such as entity events and full resync triggers.  Each log record has a specific structure and provides information about the feed, operation, status, elapsed time, process id, and the caller.|
| SaaS data export error log | `data-export-errors.log` | Provides error messages and stack traces for errors that occur during the data synchronization process.|
| SaaS export log | `saas-export.log` | Provides information about the data sent to Commerce SaaS services.|
| SaaS export error log | `saas-export-errors.log` | Provides information about errors that occur when sending data to Commerce SaaS services.|

If you do not see expected data for an Adobe Commerce Service, use the error logs for the data export extension to determine where the problem occurred. Also, you can extend logs with additional data for tracking and troubleshooting. See [Extended logging](#extended-logging).

### Log format

Each log record has the following structure.

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elapsed from script run>",
   "pid": "<process id that executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>The JSON-based string is beautified for better readability.

The following table describes the operation types that can be recorded in the logs.

| Operation                  | Description                                                                                                                                 | Caller example                                                                       |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| full sync | Collects and sends all data to the SaaS for a given feed. | `bin/magento saas:resync --feed=products`                                              |
| partial reindex            | Collects and sends data to SaaS for only updated entities in a given feed. This log is present only if updated entities exist.              | `bin/magento cron:run --group=index`                                                   |
| retry failed items         | Resend items for a given feed to SaaS if the previous sync operation failed due to a Commerce application or server error. This log is present only if failed items exist.| `bin/magento cron:run --group=saas_data_exporter`  (any "*_data_exporter" cron group)  |
| full sync (legacy)          | Collects and sends all data to SaaS for a given feed in legacy export mode.                                                   | `bin/magento saas:resync --feed=categories`                                            |
| partial reindex (legacy)   | Sends updated entities to SaaS for a given feed in legacy export mode. This log is present only if updated entities exist.             | `bin/magento cron:run --group=index`                                                   |
| partial sync (legacy)      | Sends updated entities to SaaS for a given feed in legacy export mode. This log is present only if updated entities exist.              | `bin/magento cron:run --group=saas_data_exporter` (any "*_data_exporter" cron group)   |


### Logging examples

During a full resync, progress is tracked and logged every 30 seconds by default. Here is an example log entry.

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

In this example, the `status` values provide information about the sync operation:

- **`"Progress 2/5"`** indicates that 2 of 5 iterations have been completed. The number of iterations depends on the number of exported entities.
- **`"processed: 200"`** indicates that 200 items have been processed.
- **`"synced: 100"`** indicates that 100 items were sent to SaaS. It's expected that `"synced"` is not equal to `"processed"`. Here is an example:
    - **`"synced" < "processed"`** means that the feed table didn't detect any changes in the item, compared to the previously synced version. Such items are ignored during the sync operation.
    - **`"synced" > "processed"`** the same entity id (for example, `Product ID`) can have multiple values in different scopes. For example, one product can be assigned to five websites. In this case, you might have "1 processed" item and "5 synced" items.

+++ **Example: Full resync log for the price feed**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## View and troubleshoot logs with New Relic

If you store Adobe Commerce logs in the New Relic, you can add parsing rules to improve the readability and query experience.

1. Log in to New Relic.

1. Go to `Logs => Parsing`.

1. Click `Create parsing rule`.

1. Configure the parsing rule by adding the following values.

   - **Filter logs based on NRQL**

     `filePath LIKE '%commerce-data-export%.log'`

   - **Parsing rule**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel} %{GREEDYDATA:feed:json}`

This example adds a rule that allows you to query New Relic logs by specific feed type, operation, and so on.

**Example query string**—`feed.feed:"products" and feed.status:"Complete"`

## Troubleshooting

If data is missing or incorrect in Commerce Services, check the logs for messages about errors that occurred during the sync from Adobe Commerce to the Commerce Services platform. If needed, use extended logging to add additional information to the logs for troubleshooting.

- The Data Export error log (`commerce-data-export-errors.log`) captures errors that occur during the collection phase.
- The SaaS Export error log (`saas-export-errors.log`) captures errors that occur during the transmission phase.

If you see errors not related to configuration or third-party extensions, submit a [support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) with as much information as possible.

### Resolve catalog sync issues {#resolvesync}

When you trigger a data resync, it can take up to an hour for the data to update and be reflected in UI components such as live search and recommendation units. If you still see discrepancies between your catalog and data on the Commerce storefront, or if the catalog sync failed, refer to the following:

#### Data discrepancy

1. Display the detailed view of the product in question in the search results.
1. Copy the JSON output and verify that the content matches what you have in the [!DNL Commerce] catalog.
1. If the content does not match, make a minor change to the product in your catalog, such as adding a space or a period.
1. Wait for a resync or [trigger a manual resync](#resync).

#### Sync not running

If the sync is not running on a schedule or nothing is synced, see this [KnowledgeBase](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce) article.

#### Sync failed

If the catalog sync has a status of **Failed**, submit a [support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

## Extended logging

Use environment variables to extend logs with additional data for tracking and troubleshooting. Add the environment variable to the command line when you run data export CLI commands as shown in the following examples.

### Check the feed payload

Include the feed payload in the SaaS export log by adding the `EXPORTER_EXTENDED_LOG=1` environment variable when you resync the feed.

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

After the operation completes, the feed payload is available for review in the SaaS export log (`var/.log/saas-export.log`).

### Preserve payload in feed index table

For the Commerce SaaS data export extension (`magento/module-data-exporter`) 103.3.0 and later, immediate export feeds keep only the minimum required data in the index table. The feeds include all catalog and inventory stock status feeds.

Preserving payload data in the index table is not recommended in production environments, but it can be useful in a developer environment. Include the feed payload in the index by adding the `PERSIST_EXPORTED_FEED=1` environment variable when you resync the feed.

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### Run profiler to troubleshoot slow performance

If the reindex process of a specific feed takes an unreasonable amount of time, run the profiler to collect additional data that might be useful for the Support Team.

Run the profiler by adding the `EXPORTER_PROFILER=1` environment variable when you run the reindex command.

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

Profiler data is stored in the data export log (`var/log/commerce-data-export.log`) in the following format:

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
