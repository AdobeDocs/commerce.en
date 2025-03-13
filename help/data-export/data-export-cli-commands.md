---
title: Sync feeds using the Commerce CLI
description: Learn how to use the command-line interface commands to manage feeds and processes for the [!DNL data export extension] for Adobe Commerce SaaS services.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
---
# Sync feeds using the Commerce CLI

The `saas:resync` command in the `magento/saas-export` package lets you manage data synchronization for Adobe Commerce SaaS services.

Adobe does not recommend using the `saas:resync` command regularly. Typical scenarios for using the command are:

- Initial sync
- Sync data to new data space after changing the [SaaS Data Space ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Troubleshooting

Monitor sync operations in the `var/log/saas-export.log` file.

## Initial Sync

>[!NOTE]
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
>For advanced options like batch size and multi-threading, see [Customize export processing](customize-export-processing.md).

## --by-ids

Partially resync specific entities by their IDs. Supports `products`, `productAttributes`, and `productOverrides` feeds.

By default, entities are specified by product SKU. Use `--id-type=ProductID` to use product IDs instead.

**Examples:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## --cleanup-feed

Cleans the feed indexer table before reindexing and sending data to SaaS. Only supported for `products`, `productOverrides`, and `prices` feeds.

>[!IMPORTANT]
>Use only after environment cleanup. Can cause data sync issues in Commerce Services.

**Example:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## --continue-resync

Resumes an interrupted resync operation. Only supported for `products`, `productAttributes`, and `productOverrides` feeds.

**Example:**

```shell
bin/magento saas:resync --feed='products' --continue-resync
```

## --dry-run

Runs the feed reindex process without submitting to SaaS or saving to the feed table. Use to validate data.

Add the`EXPORTER_EXTENDED_LOG=1` environment variable to save payload to `var/log/saas-export.log`.

**Example:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## --feed

Required. Specifies the feed entity to resync.

Available feeds:

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**Example:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' 1
```

## --no-reindex

Resubmits existing catalog data to [!DNL Commerce Services] without reindexing. Not supported for product-related feeds.

Behavior varies by export mode:

- Legacy mode: Resubmits all data without truncating
- Immediate mode: Option is ignored, only syncs updates/failures

**Example:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## Troubleshooting

If you do not see expected data in connected Commerce Services, troubleshoot issues by checking data export error logs and using the `saas:resync` command with environment variables to review payloads and profiler data. See [Review logs and troubleshoot](troubleshooting-logging.md).
