---
title: Feed Lock Mechanism for SaaS Data Export
description: Learn how [!DNL SaaS Data Export] uses feed locks to prevent conflicting sync operations and protect data integrity during concurrent feed updates.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
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
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---

# Feed lock mechanism for SaaS Data Export

The [!DNL SaaS Data Export] extension uses a feed lock mechanism to prevent race conditions when multiple processes attempt to sync the same feed concurrently. This can happen, for example, when a cron-triggered resync overlaps with a manual `saas:resync` CLI call.

## How the feed lock works

Each feed sync operation—whether triggered by a cron job or a manual `saas:resync` CLI call—follows the same sequence:

1. The process tries to acquire the feed lock. The lock attempt is non-blocking and returns immediately if the lock is already held by another process.
1. If the lock is **not available**, the operation is skipped and logged.

   No data is lost. The next cron run picks up pending changes after the current process completes.
1. If the lock is **acquired**, the process records its name and PID for diagnostic purposes, then runs the sync.
1. When the sync completes or fails, the lock is released unconditionally so the next scheduled cron job can proceed normally.

Only one sync operation can hold the feed lock at a time, regardless of whether it was started by cron or the CLI. The feed lock is implemented through [!DNL Adobe Commerce]'s `LockManagerInterface`. The default backend is MySQL, which uses `GET_LOCK` and `RELEASE_LOCK` functions. To configure a different lock provider, see [Configure the lock provider](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}.

## Expected log messages

The following message in `commerce-data-export.log` is normal and does not indicate a problem:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

This message appears when a cron-triggered partial sync attempts to run while a full reindex or `saas:resync` is already in progress. The skipped operation is not lost. Once the running process completes and releases the lock, the next cron execution picks up and syncs any pending changes.

>[!NOTE]
>
>For general information about log format and operation types recorded in `commerce-data-export.log`, see [Review logs and troubleshoot](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Synchronize data with SaaS Data Export](sync-overview.md)
> - [Sync feeds using the Commerce CLI](data-export-cli-commands.md)
> - [Connector sync pipeline](../aco-connector/connector-sync-pipeline.md)
> - [Configure the lock provider](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
