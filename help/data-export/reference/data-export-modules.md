---
title: SaaS Data Export Modules
description: Learn about the Magento module packages included in [!DNL SaaS Data Export] and their roles in data collection, transformation, and submission to Adobe SaaS services.
role: Developer
feature: Services
---

# SaaS Data Export modules

[!DNL SaaS Data Export] consists of two module groups: first for data collection and indexing, and second for HTTP transport and submission.

These modules handle entity change detection, feed indexing, data extraction, and schema definition.
The following table provides only framework-level modules, the full list of available modules depends on installed package.

| Module | Purpose | Key Classes |
|---|---|---|
| `DataExporter` | Core framework: indexer, feed table, hash, retry, locking | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager`|
| `QueryXml` | XML-based query DSL for data collection | `QueryBuilder`, `QueryXmlFactory` |
| `SaaSCommon` | Shared HTTP transport, retry, CLI (`saas:resync`), progress bar | |

To learn how these modules work together during synchronization, see [SaaS data export pipeline](../sync-overview.md).

>[!MORELIKETHIS]
>
>- [Synchronize data with SaaS Data Export](../sync-overview.md)
>- [Feed table schema](feed-table-reference.md)
>- [Manage the SaaS data export extension](../manage-extension.md)
