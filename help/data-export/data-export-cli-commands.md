---
title: Sync feeds using the Commerce CLI
description: Learn how to use the command-line interface commands to manage feeds and processes for the [!DNL data export extension] for Adobe Commerce SaaS services.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
---
# Sync feeds using the Commerce CLI

The `saas:resync` command in the `magento/saas-export` package lets you manage data synchronization for Adobe Commerce SaaS services.

Adobe does not recommend using the `saas:resync` command regularly. Typical scenarios for using the command are:

- Initial sync
- Sync data to a new data space after changing the [SaaS Data Space ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Troubleshooting

Monitor sync operations in the `var/log/saas-export.log` file.

## Initial sync

>[!NOTE]
>
>Initial sync runs automatically when Live Search or Product Recommendations are enabled. Manual commands are not needed.

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

## Sync using CLI commands

The `saas:resync` command supports various sync operations:

- Partial sync by SKU
- Resume interrupted syncs
- Validate data without syncing

View all available options:

```shell
bin/magento saas:resync --help
```

See the following sections for option descriptions with examples.


>[!NOTE]
>
>For advanced options to manage export processing, see [Customize export processing](customize-export-processing.md).

## `--by-ids`

Partially resync specific entities by their IDs. Supports `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants`, and `categoryPermissions` feeds.

By default, when you use the `--by-ids` option you specify values using product SKU values. To use product IDs instead, add the `--id-type=ProductID` option.

**Examples:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

Clean up the feed indexer table before reindexing and sending data to SaaS. Only supported for `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants`, and `categoryPermissions`.

If used with the `--dry-run` option, the operation performs a dry-run resync operation for all items.

>[!IMPORTANT]
>
>Use only after environment cleanup, or with the `--dry-run` option. If used in other cases, the cleanup operation can cause data loss and data sync issues.

**Example:**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

Resumes an interrupted resync operation. Only supported for `products`, `productAttributes`, and `productOverrides` feeds.

**Example:**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

Runs the feed reindex process without submitting the feed to SaaS and without saving to the feed table. This option is useful to identify any issues with your data set.

Add the `EXPORTER_EXTENDED_LOG=1` environment variable to save payload to `var/log/saas-export.log`.

**Example:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### Test specific feed items

Test specific feed items by adding the `--by-ids` option with the extended logs collection to see the generated payload in the `var/log/saas-export.log` file.

**Example:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### Test all feed items

By default, the feed submitted during a `resync --dry-run` operation includes only new items, or items that failed to be exported previously. To include all items in the feed to be processed, use the `--cleanup-feed` option.

**Example**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

Required. Specifies the feed entity to resync.

Available feeds:

- `categories`
- `categoryPermissions`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

>[!NOTE]
>
>The feeds available in your environment might be different depending on which modules are installed in your Adobe Commerce environment.

**Example:**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

Resubmits existing catalog data to [!DNL Commerce Services] without reindexing. Not supported for product-related feeds.

Behavior varies by [export mode](data-synchronization.md#synchronization-modes):

- Legacy mode: Resubmits all data without truncating.
- Immediate mode: Option is ignored, only syncs updates/failures.

**Example:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

By default, the entities specified when you use the `saas:resync feed` command with the `--by-ids` option are specified by product SKU. Use the `--id-type=ProductId` option, to specify entities by product ID.

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**Example:**

## Troubleshooting

If you do not see expected data in connected Commerce Services, troubleshoot issues by checking data export error logs and using the `saas:resync` command with environment variables to review payloads and profiler data. See [Review logs and troubleshoot](troubleshooting-logging.md).
