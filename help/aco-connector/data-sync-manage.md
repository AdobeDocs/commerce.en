---
title: 'Manage [!DNL Adobe Commerce Optimizer Connector] Synchronization'
description: "Learn how to verify catalog data sync and manually resync connector feeds between [!DNL Adobe Commerce] and [!DNL Adobe Commerce Optimizer]."
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Manage synchronization to [!DNL Commerce Optimizer]

After you set up the [!DNL Adobe Commerce Optimizer Connector], most catalog updates sync automatically through scheduled cron jobs. For details on how automated synchronization works, see [Connector sync pipeline](connector-sync-pipeline.md). Use the tools in this topic to verify that data reaches [!DNL Adobe Commerce Optimizer] and to manually resync feeds when needed.

## Verify that the data sync is working {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Manually resync data {#manually-resync-data}

When partial sync and automatic retry do not resolve synchronization issues, you can manually resync catalog data. The option you choose depends on where the problem originates and how much control you need.

| Task | Option | Notes |
| --- | --- | --- |
| Verify sync status and resync from the upstream system when products are missing | **Upstream-system resync** | Use the [!UICONTROL Data Sync] page in [!DNL Commerce Optimizer] to verify the data delivered to [!DNL Commerce Optimizer]; when products are missing, resync from the upstream system. See [Resync catalog data](../optimizer/setup/data-sync.md#resync-catalog-data) in the *[!DNL Commerce Optimizer] User Guide*. |
| Resync selected failed or problematic connector feed items | **[!UICONTROL Data Feed Sync Status] page in the Commerce Admin** | Monitor export status and resync selected connector feed items from the Commerce Admin. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working). |
| Targeted connector feed resync with operational control | **Commerce CLI** | Run `saas:resync` from the Adobe Commerce instance for connector feeds. See [Sync feeds using the Commerce CLI](../data-export/data-export-cli-commands.md) and [Supported feeds](reference/connector-reference.md#supported-feeds). |
| Force a full repopulation for a catalog source scope | **Disable and re-enable scope** | Clear and reselect the data sync checkbox for a store view in **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]** to trigger a full repopulation. See [Customize the Commerce scopes export configuration](get-started.md#customize-the-commerce-scopes-export-configuration). |

>[!NOTE]
>
>The [!UICONTROL Data Sync] page in [!DNL Commerce Optimizer] does not provide a resync-selected-items control. For connector-backed implementations, use the Commerce Admin [!UICONTROL Data Feed Sync Status] page and/or the Commerce CLI. See [Verify that the data sync is working](#verify-that-the-data-sync-is-working).

>[!MORELIKETHIS]
>
> - [Connector sync pipeline](connector-sync-pipeline.md) — Learn how automated synchronization, cron schedules, and error handling work
> - [Troubleshooting](troubleshooting.md) — Diagnose credential, sync, and scope export issues
> - [Connector modules and feed endpoints](reference/connector-reference.md) — Review modules, API endpoints, and supported feeds
