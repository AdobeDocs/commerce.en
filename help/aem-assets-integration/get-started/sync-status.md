---
title: View AEM Assets sync status
description: Review synchronized assets in an asset-centric list in the Commerce Admin.
feature: CMS, Media, Integration
---

# View AEM Assets sync status

The [!UICONTROL Sync Status] view provides an asset-centric list of assets synchronized through the AEM Assets integration. Use it to find, review, and troubleshoot assets by their own attributes instead of navigating product-by-product in the catalog.

>[!NOTE]
>
> [!UICONTROL Sync Status] is available in the Adobe Commerce Admin for Adobe Commerce as a Cloud Service and Adobe Commerce on Cloud infrastructure projects. It is not available for [!DNL Adobe Commerce Optimizer].

## Open Sync Status

On the _Admin_ sidebar, navigate to **[!UICONTROL System]** > **[!UICONTROL AEM Assets]** > **[!UICONTROL Sync Status]**.

![AEM Assets Sync Status in the System menu](../assets/aem-assets-sync-status-system-menu.png){width="600" zoomable="yes"}

Integration settings remain under **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL AEM Assets Configuration]**.

![AEM Assets Configuration in the Configuration tree](../assets/aem-assets-configuration-admin-menu.png){width="600" zoomable="yes"}

## Asset list

The grid lists synchronized assets from AEM Assets. Each row represents one asset and its sync state in Commerce.

Typical columns include:

| Column | Description |
|--------|-------------|
| **Asset** | Asset identifier or display name from AEM Assets. |
| **Asset path** | Path or reference to the asset in AEM Assets. |
| **Sync status** | Current synchronization state (for example, success, failed, or in progress). |
| **Last sync date** | Date and time of the most recent sync attempt for the asset. |
| **Linked products** | Product SKUs associated with the asset through matching rules or metadata. |
| **Error details** | Short error summary when **Sync status** is failed. |

Use the grid controls to show or hide columns supported in your environment.

### Search and filter

Use the list toolbar to narrow results **by asset**, not by product:

* **Search** — Find assets by name, path, SKU association, or other indexed asset fields.
* **Filters** — Limit the list by **Sync status**, date range, or other asset attributes exposed in the filter panel.

Filters apply to `asset-level` data so you can isolate failed syncs or recently updated assets without opening individual products.

## Failed synchronizations

When **Sync status** is **Failed**, the **Error details** column shows a short error summary in the list.

1. Open the asset row to view the detail panel or detail view.

1. Review the full error message and last sync attempt details to diagnose the failure.

For additional troubleshooting, see [Default automatic matching](../synchronize/default-match.md). Integration log files are available at `/var/log/aem-assets-integration.log` and `/var/log/aem-assets-integration-errors.log` on your Commerce instance.
