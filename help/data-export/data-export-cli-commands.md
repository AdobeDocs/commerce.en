---
title: Sync feeds using the Commerce CLI
description: Learn how to use the command-line interface commands to manage feeds and processes for the [!DNL data export extension] for Adobe Commerce SaaS services.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
---
# Sync feeds using the Commerce CLI

Developers and system administrators can manage synchronization operations for SaaS data export using the [Adobe Commerce command-line tool](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI). The `saas:resync` command is included in the `magento/saas-export` package.

Adobe does not recommend using the `saas:resync` command regularly. Typical scenarios for using the command are:

- Initial sync
- Sync data to new data space after changing the [SaaS Data Space ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Troubleshooting

## Initial Sync

>[!NOTE]
>If Live Search or Product Recommendations are enabled on the Commerce instance, the initial sync runs automatically after connecting the service to your Commerce instance. You do not have to run commands manually.

When you trigger a `saas:resync` from the command line, depending on your catalog size, it can take from a few minutes to a few hours for the data to update.

For the initial sync, Adobe recommends running the commands in the following order:

```shell
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## Resync using CLI commands

Review the following examples to run resync operations using the `bin/magento saas:resync` CLI command. Command options are described in [command options](#command-options).

| Resync operation                                                                | Command example                                                                                   |
|----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| Fully resync an entity feed                             | `bin/magento saas:resync --feed='<FEED_NAME>' 1`                                                  |
| Resync dry run<br>without sending data | `bin/magento saas:resync --feed='products' --dry-run`                                              |
| Clean up data before a full resync                    | `bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed`                                       |
| Partially resync product-related feeds by product SKU  | `bin/magento saas:resync --feed='products' --by-ids='Product 1,Product 2,Product 3'` |
| Resubmit all data to connected Commerce services without reindexing    | `bin/magento saas:resync --feed='FEED_NAME' --no-reindex`                                         |
| List available commands and options with descriptions                | `bin/magento saas:resync --help`                                                                  |
| Dry run of a resync operation to identify issues without submitting feeds to SaaS | `bin/magento saas:resync --feed='products' --dry-run`                                              |

>[!TIP]
>
>Monitor the `var/log/saas-export.log` file during sync operations for real-time progress updates.

## Resync command options

The following options are available for managing sync operations using the saas:resync command.

>[!NOTE]
>
>The `saas:resync` command also supports advanced options to improve data export commands by increasing batch size and adding multi-thread processing. See [Customize export processing](customize-export-processing.md).

| Option       | Description |
|--------------|-------------|
| `--by-ids`     | Partially resync a specified list of entity ids in the `products`, `productAttributes`, or `productOverrides` feeds.<br><br>Specify ids in a comma-separated list. By default, the id value is a product SKU. To use the product id instead, add the `-id-type=ProductID` option.<br><br><strong>Examples:</strong><ul><li><strong>Sync by SKU:</strong> `bin/magento saas:resync --feed='products' --by-ids='Product 1,Product 2,Product 3'`</li><li><strong>Sync by productId:</strong> `bin/magento saas:resync --feed='products' --by-ids=1,2,19 --id-type=productId`</li></ul>|
| `--cleanup-feed`    | Clean up the feed indexer table before starting a reindex and sending data to SaaS. This option is supported only for `products`, `productOverrides`, and `prices` feeds.<br><br>By default, the `bin/magento saas:resync` command performs a [partial sync](data-synchronization.md#partial-sync), only reindexing and sending feed items that were not indexed or were not sent to SaaS for some reason. When you use the `--cleanup-feed` option, all feed records are reindexed and sent to SaaS. See [examples](#common-commands).<br><br><strong>Note:</strong>Adobe recommends only using this option after performing environment cleanup operations. It can cause data sync issues in Adobe Commerce Services. For example, the `delete product event` might not propagate to the Adobe Commerce service if the `--cleanup-feed` option is used. |
| `--continue-resync` | Continue a previous resync operation that was interrupted. This option is supported only for `products`, `productAttributes`, and `productOverrides` feeds.<br><br><strong>Example:</strong> `bin/magento saas:resync --feed='products' --continue-resync` |
| `--dry-run`    | Identify any issues with your data set by running the entire feed reindex process without submitting feeds to SaaS and without saving to the feed table. See [examples](#common-commands).<br><br>To save the payload to log file `var/log/saas-export.log`, run the command with the environment variable `EXPORTER_EXTENDED_LOG=1`.<br><br><strong>Example:</strong> `EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products --dry-run`|
| `--feed`       | Required. Specifies which feed entity to resync, such as `products`. See [examples](#common-commands).<br><br>The `feed` option value can include any of the available entity feeds:<ul> <li>`categories`</li><li>`categoryPermissions`</li><li>`inventoryStockStatus`</li><li>`orders`</li><li>`prices`</li><li>`products`</li><li>`productAttributes`</li><li>`productOverrides`</li><li>`scopesWebsite`</li><li>`scopesCustomerGroup`</li><li>`variants`</li></ul>Depending on which [Commerce Services](../landing/saas.md) are installed, you might have a different set of feeds available for the `saas:resync` command. |
| `--no-reindex` | Resubmit the existing catalog data to [!DNL Commerce Services] without reindexing. See [examples](#common-commands).<br><br>If this option is not specified, the command runs a full reindex before syncing data.<br><br>The behavior of this option depends on whether the feed is exported in [legacy or immediate export mode](data-synchronization.md#synchronization-modes).<ul><li>For legacy export feeds, the synchronization process does not truncate indexed data in the feeds table. Instead, it resubmits all data to the Adobe Commerce service.</li><li>For immediate export feeds, this option is ignored if specified. For these feeds, the resync process does not truncate the index and only resynchronizes updates or items that previously failed.</li></ul><strong>Note:</strong>This option is not supported for product-related feeds (`products`, `productAttributes`, and `productOverrides`).|


## Troubleshooting

If you do not see expected data in connected Commerce Services, troubleshoot issues by checking data export error logs and using the `saas:resync` command with environment variables to review payloads and profiler data. See [Review logs and troubleshoot](troubleshooting-logging.md).
