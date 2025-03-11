---
title: SaaS Data Export Command-line Interface
description: Learn how to use the command-line interface commands to manage feeds and processes for the [!DNL data export extension] for Adobe Commerce SaaS services.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
---
# SaaS Data Export Command-line Interface Reference

Developers and system administrators can manage synchronization operations for SaaS data export using the [Adobe Commerce command-line tool](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI). The `saas:resync` command is included in the `magento/saas-export` package.

Adobe does not recommend using the `saas:resync` command regularly. Typical scenarios for using the command are:

- The initial sync
- The [SaaS Data Space ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) was changed, and you need to synchronize data to the new data space.
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

## Command examples

Before using `saas:resync` commands, review the [option descriptions](#command-options).

| Task                                                                 | Example Command                                                                                   |
|----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| Fully resync an entity feed                             | `bin/magento saas:resync --feed='<FEED_NAME>' 1`                                                  |
| Resync dry run<br>without sending data | `bin/magento saas:resync --feed='products' --dry-run`                                              |
| Clean up data before a full resync                    | `bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed`                                       |
| Partially resync product-related feeds by product SKU  | `bin/magento saas:resync --feed='products' --by-ids='Product 1,Product 2,Product 3'` |
| Resubmit all data to connected Commerce services without reindexing    | `bin/magento saas:resync --feed='FEED_NAME' --no-reindex`                                         |
| List available commands and options with descriptions                | `bin/magento saas:resync --help`                                                                  |
| Dry run of a resync operation to identify issues without submitting feeds to SaaS | `bin/magento saas:resync --feed='products' --dry-run`                                              |

## Command options

The following options are available for managing `saas:resync` operations.

>[!NOTE]
>
>The `saas:resync` command also supports advanced options to improve data export commands by increasing batch size and adding multi-thread processing. See [Customize export processing](customize-export-processing.md).

| Option       | Description |
|--------------|-------------|
| `--by-ids`     | Partially resync a specified list of entity ids in the `products`, `productAttributes`, or `productOverrides` feeds.<br><br>Specify ids in a comma-separated list. By default, the id value is a product SKU. To use the product id instead, add the `-id-type=ProductID` option. See [examples](#common-commands). |
| `--cleanup`    |Clean up the feed indexer table before a sync.<br><br>When specified, SaaS data export runs a full resync for the specified feed and cleans up all existing data in the feed table.  See [examples](#common-commands).<br><br>**Do not use this option regularly**. Adobe recommends only using this command after performing the [!DNL Data Space ID Cleanup] operation. It can cause data sync issues in Adobe Commerce Services. For example, the `delete product event` might not propagate to the Adobe Commerce service if the `cleanup` option is used. |
| `--continue-resync` | Continue a previous resync operation that was interrupted. This option is available only for product-related feeds (`products`, `productAttributes`, and `productOverrides`).</p><p><strong>Example:</strong> `bin/magento saas:resync --feed='products' --continue-resync` |
| `--dry-run`    | Identify any issues with your data set by running the entire feed reindex process without submitting feeds to SaaS and without saving to the feed table. See [examples](#common-commands).<br><br>Save the payload to log file `var/log/saas-export.log`, run the command with the env variable `EXPORTER_EXTENDED_LOG=1`. |
| `--feed`       | This required option specifies which feed entity to resync, such as `products`. The `feed` option value can include any of the available entity feeds:<ul> <li>`categories`</li><li>`categoryPermissions`</li><li>`inventoryStockStatus`</li><li>`orders`</li><li>`prices`</li><li>`products`</li><li>`productAttributes`</li><li>`productOverrides`</li><li>`scopesWebsite`</li><li>`scopesCustomerGroup`</li><li>`variants`</li></ul>See [examples](#common-commands).<br><br>Depending on which [Commerce Services](../landing/saas.md) are installed, you might have a different set of feeds available for the `saas:resync` command. |
| `--no-reindex` | <p>Resubmit the existing catalog data to [!DNL Commerce Services] without reindexing. See [examples](#common-commands).</p><p>If this option is not specified, the command runs a full reindex before syncing data.</p><p>The behavior of this option depends on whether the feed is exported in [legacy or immediate export mode](data-synchronization.md#synchronization-modes).<ul><li>For legacy export feeds, the synchronization process does not truncate indexed data in the feeds table. Instead, it resubmits all data to the Adobe Commerce service.</li><li>For immediate export feeds, this option is ignored if specified. For these feeds, the resync process does not truncate the index and only resynchronizes updates or items that previously failed.</li></ul> <p><p><strong>Note:</strong>This option is not available for product-related feeds (`products`, `productAttributes`, and `productOverrides`).|


## Troubleshooting

If you do not see expected data in connected Commerce Services, troubleshoot issues by checking data export error logs and using the `saas:resync` command with environment variables to review payloads and profiler data. See [Review logs and troubleshoot](troubleshooting-logging.md).
