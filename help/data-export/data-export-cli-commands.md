---
title: Sync feeds using the Commerce CLI
description: Learn how to use Commerce CLI commands to manage feeds and sync processes for the [!DNL data export extension] in Adobe Commerce SaaS services.
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Sync feeds using the Commerce CLI

The `saas:resync` command in the `magento/saas-export` package lets you manage data synchronization for [!DNL Adobe Commerce] SaaS services.

>[!NOTE]
>
>The `saas:resync` command also applies to [!DNL Adobe Commerce Optimizer Connector] feeds such as `products`, `categories`, and `priceBooks`. See [Supported feeds](../aco-connector/reference/connector-reference.md#supported-feeds) for the full list of connector feeds and indexer names.

Adobe does not recommend using the `saas:resync` command regularly. Typical scenarios for using the command are:

- Initial sync
- Sync data to a new data space after changing the [SaaS Data Space ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Troubleshooting

Monitor sync operations in the `var/log/saas-export.log` file.

## Initial sync

>[!NOTE]
>
>Initial sync runs automatically when Live Search or Product Recommendations are enabled. Manual commands are not needed.
>
>For [!DNL Adobe Commerce Optimizer Connector] deployments, the `aco:config:init` command schedules the initial full sync by invalidating all connector feed indexers. See [Enable the [!DNL Commerce Optimizer] integration](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration) and [Manage synchronization to [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md).

When you trigger a `saas:resync` from the command line, depending on your catalog size, it can take from a few minutes to a few hours for the data to update.

Feed syncs can be run in any order - there are no hard dependencies between them. The following sequence starts with scope data first, which is a logical starting point since scopes define the store views that other feeds reference.

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>Your environment may not include every feed in this sequence. See [Supported feeds](reference/feed-table-reference.md#supported-feeds) for the full feed list, CLI feed names, and module requirements.

## Command options

The `saas:resync` command supports various sync operations:

- Partial sync by SKU
- Resume interrupted syncs
- Validate data without syncing

View all command options and flags:

```shell
bin/magento saas:resync --help
```

See the following sections for option descriptions with examples.

>[!NOTE]
>
>For advanced options to manage export processing, see [Customize export processing](customize-export-processing.md).

## `--feed`

Required. Specifies the feed entity to resync.

`bin/magento saas:resync --help` documents command options and flags. It does not list every feed available in your environment. For the full feed list with CLI feed names, indexer IDs, and feed tables, see [Supported feeds](reference/feed-table-reference.md#supported-feeds).

>[!NOTE]
>
>Installed modules determine which feeds you can resync. For example, `productOverrides` requires [!DNL Adobe Commerce] on cloud, on premises, or Commerce as a Cloud Service, and `orders` requires the Sales Orders module.

>[!NOTE]
>
>The `saas:resync` command only transmits new items, updated items, and items that previously failed to export. Items whose content hash has not changed since the last export are skipped.

**Example:**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

Partially resync specific entities by their IDs. Supports `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants`, and `categoryPermissions` feeds.

By default, when you use the `--by-ids` option you specify values using product SKU values. To use product IDs instead, add the `--id-type=productId` option.

>[!NOTE]
>
>Unlike a standard resync, `--by-ids` bypasses hash verification and forces the specified entities to be submitted to connected Commerce services regardless of whether their content has changed since the last export.

**Examples:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

Clean up the feed indexer table before reindexing and sending data to SaaS. Only supported for `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants`, and `categoryPermissions`.

If used with the `--dry-run` option, the operation performs a dry-run resync operation for all items.

>[!WARNING]
>
>Using the resync command with the `cleanup-feed` option clears the local feed export state and can lead to incomplete synchronization. For example, entity deletions in [!DNL Adobe Commerce] may not be reflected in connected Commerce Services, or stale entities may remain in the remote Commerce Services indexes even though they were deleted or updated in [!DNL Adobe Commerce]. Use this option only for full environment rebuilds, such as after a SaaS data space cleanup.

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

**Example:**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

Resubmits existing catalog data to [!DNL Commerce Services] without reindexing. Not supported for product-related feeds.

Behavior varies by [export mode](sync-overview.md#synchronization-modes):

- Legacy mode: Resubmits all data without truncating.
- Immediate mode: Option is ignored, only syncs updates/failures.

**Example:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [Review logs and troubleshoot](troubleshooting/logging.md) — Diagnose data export and SaaS export errors.
> - [Troubleshooting scenarios](troubleshooting/troubleshooting-scenarios.md) — Resolve misconfiguration and unexpected sync results.
> - [How synchronization works](sync-overview.md) — Learn about sync modes and retry behavior.
