---
title: Feed Lock Mechanism for SaaS Data Export
description: Learn how [!DNL SaaS Data Export] uses feed locks to prevent conflicting sync operations and protect data integrity during concurrent feed updates.
role: Admin, Developer
feature: Services
---

# Feed lock mechanism for SaaS Data Export

The [!DNL SaaS Data Export] extension uses a feed lock mechanism to prevent race conditions when multiple processes attempt to sync the same feed concurrently. This can happen, for example, when a cron-triggered resync overlaps with a manual `saas:resync` CLI call.

## How the feed lock works

Each feed sync operation—whether triggered by a cron job or a manual `saas:resync` CLI call—follows the same sequence:

1. The process tries to acquire the feed lock. The lock attempt is non-blocking and returns immediately if the lock is already held by another process.
1. If the lock is **not available**, the [operation is skipped and logged].

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
>For general information about log format and operation types recorded in `commerce-data-export.log`, see [Review logs and troubleshoot](troubleshooting-logging.md).

## More help on this topic

- [Synchronize data with SaaS Data Export](sync-overview.md)
- [Sync feeds using the Commerce CLI](data-export-cli-commands.md)
- [Configure the lock provider](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
