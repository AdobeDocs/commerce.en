---
title: SaaS Data Export Modules
description: Learn about the Magento module packages included in [!DNL SaaS Data Export] and their roles in data collection, transformation, and submission to Adobe SaaS services.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
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
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---

# SaaS Data Export modules

[!DNL SaaS Data Export] consists of two module groups: first for data collection and indexing, and second for HTTP transport and submission.

These modules handle entity change detection, feed indexing, data extraction, and schema definition.
The following table provides only framework-level modules; the full list of available modules depends on the installed packages.

| Module | Purpose | Key Classes |
| --- | --- |--- |
| `DataExporter` | Core framework: indexer, feed table, hash, retry, locking | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | XML-based query DSL for data collection | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | Shared HTTP transport, retry, CLI (`saas:resync`), resync orchestration | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

To learn how these modules work together during synchronization, see [SaaS data export pipeline](../sync-overview.md).

>[!MORELIKETHIS]
>
>- [How synchronization works](../sync-overview.md)
>- [Feed table schema](feed-table-reference.md)
>- [Manage the SaaS data export extension](../manage-extension.md)
