---
title: Improve SaaS Data Export Performance
description: Learn how to improve SaaS data export performance for Commerce Services by using a multi-thread data export mode.
role: Admin, Developer
exl-id: 7151118c-5e30-44d0-b515-5801a73e44ec
---
# Improve SaaS Data Export Performance

**Multi-thread data export mode** accelerates the export process by dividing feed data into batches and processing them concurrently.

Developers or system integrators can improve performance by using the multi-thread data export mode instead of the default single-thread mode. In single-thread mode, there is no parallelization of the feed submission process. Additionally, due to the default limits set, all clients are restricted to using only one thread. In most cases, customizing the configuration is not required.

## Considerations for using multi-thread mode

When working with data export services, you want to optimize performance while ensuring accurate synchronization.
Adobe recommends using the default configuration for data ingestion, which typically meets the synchronization requirements for Commerce merchants. However, there are scenarios where customization can speed up processing time.

Consider the following key factors when deciding whether to customize the data export configuration:

- **Initial Synchronization**–Evaluate the number of products and [estimate the data volume and transmission time](estimate-data-volume-sync-time.md) based on the default configuration. Ask yourself: Can you wait for this initial data synchronization after onboarding a Commerce service?

- **Adding New Store Views or Websites**–If you plan to add store views or websites with the same product count after going live, estimate the data volume and transmission time. Determine whether the synchronization time is acceptable with the default configuration or if multi-thread processing is necessary.

- **Regular Imports**–Anticipate regular imports, such as price updates or stock status changes. Assess whether these updates can be applied within an acceptable time frame or if faster processing is needed.

- **Product Weight**–Consider whether your products are lightweight or heavy. Adjust the batch size accordingly if product descriptions or attributes inflate the product size.

Remember that thoughtful planning, including estimating data volume and synchronization time, can often eliminate the need for customization. Schedule feed ingestion operations based on these estimates to achieve optimal results.

>[!NOTE]
>
>Adobe recommends exercising caution when using multi-thread processing. If you configure multi-threading for faster performance, you can trigger Adobe Commerce Services guardrails included to prevent system misuse during data ingestion. These guardrails also restrict users from triggering synchronization changes that can overload the system. When the guardrails are triggered, requests are blocked and the system returns 429 errors. If you encounter these errors, adjust your configuration, and submit a support ticket for assistance.

## Configure multi-threading

Multi-thread mode is supported for all [synchronization methods](data-synchronization.md#synchronization-process)—full sync, partial sync, and failed items sync. To configure multi-threading, you specify the number of threads and batch size to use during synchronization.

- `thread-count` is the number of threads that are activated to process entities. The default `thread-count` is `1`.
- `batch-size` is the number of entities that are processed in one iteration. The default `batch-size` is `100` records for all feeds except the price feed. For the price feed, the default value is `500` records.

You can configure multi-threading as a temporary option when running a resync command, or by adding the multi-thread configuration to the Adobe Commerce application configuration.

>[!NOTE]
>
>Ensure that you align the performance of SaaS data export with the rate limit that is defined for a client on the consumer side.

### Configure multi-threading at runtime

When you run a full sync command from the command line, specify multi-thread processing by adding the `thread-count` and `batch-size` options to the CLI command.

```
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

Options specified on the command line override the data export configuration specified in the Adobe Commerce application `config.php` file.

### Add multi-threading to the Commerce configuration

To process all data export operations using multi-threading, system integrators or developers can modify the number of threads and batch size for each feed in the Commerce application configuration.

These changes can be applied by adding custom values to the [system section](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system) of the configuration file, `app/etc/config.php`.

**Example: Configuring multithreading for products and prices**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```
