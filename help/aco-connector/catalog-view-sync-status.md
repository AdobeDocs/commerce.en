---
title: Monitor Catalog View Synchronization for B2B Shared Catalogs
last-update: 2026-09-03
description: "Use the Catalog View Sync Status page to monitor and reconcile B2B shared catalog view, policy, price book, and key configuration data synchronized to Adobe Commerce Optimize."
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
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

# Monitor catalog view synchronization for B2B shared catalogs

[!BADGE Private Beta]{type=Caution tooltip="Requires the Adobe Commerce Optimizer Connector B2B extension, which is currently in private beta."}

Track B2B shared catalog synchronization from [!DNL Adobe Commerce] to [!DNL Adobe Commerce Optimizer] using the [!UICONTROL Catalog View Sync Status] dashboard in the Commerce Admin.

[!UICONTROL Catalog View Sync Status] verifies that the catalog view, policy, price book, and restricted access key configurations for each B2B shared catalog exists in [!DNL Adobe Commerce Optimizer] and matches your [!DNL Adobe Commerce] configuration. To track product, price, and category feed synchronization instead, see [Manage data synchronization](data-sync-status.md#verify-that-the-data-sync-is-working).

## Access the sync status page {#access-the-sync-status-page}

From the Commerce Admin, go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Catalog View Sync Status]**.

![Catalog View Sync Status page to monitor the sync status of the catalog view, policy, price book, and access key configurations in Adobe Commerce Optimizer](assets/catalog-view-sync-status.png){width="600" zoomable="yes"}

## Interpret sync status for your shared catalogs {#interpret-sync-status}

In the dashboard, each row represents one custom shared catalog view projected from a shared catalog and store view combination. Use the status information to determine whether the data delivered to the company's storefront experience is complete and correct. The following table summarizes the most common status values and what they mean for your shared catalog:

| Status | What it means for your shared catalog |
| --- | --- |
| **Degraded** | Something was changed directly in [!DNL Adobe Commerce Optimizer]—for example, the policy or price book. The company may see the wrong assortment or pricing until you resolve the issue. |
| **Failed** | The catalog view does not exist in [!DNL Adobe Commerce Optimizer]. The company cannot access this shared catalog's storefront experience. |
| **Retiring** | You deleted the shared catalog in [!DNL Adobe Commerce]. The catalog view is still accessible during its deletion grace period. |
| **Orphaned** | The catalog view or key was created directly in [!DNL Adobe Commerce Optimizer] Studio, not by the connector. See [Review orphaned and deleted entries](#review-orphaned-and-deleted-entries). |

[!UICONTROL Healthy], [!UICONTROL Pending], and [!UICONTROL Deleted] are informational states that don't require action. See <!--[Sync status values](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status#sync-status-values){target="_blank"} in the *Commerce Admin Guide* for the full list. -->

## Choose monitoring or repair {#choose-monitoring-or-repair}

[!DNL Adobe Commerce] is always the source of truth for the catalog view, policy, price book, and key configurations for B2B shared catalogs. If you or another administrator changed a policy, price book, or key configuration setting directly in [!DNL Adobe Commerce Optimizer] Studio, reconciliation reports the configuration differences as drift.

- Select **[!UICONTROL Reconcile]** to check for drift without changing anything, so you can review differences before acting.
- Select **[!UICONTROL Reconcile & Repair]** to restore the expected configuration for any repairable drift.

To review what changed and why, open a catalog view's detail page and check its drift history.

## Review orphaned and deleted entries {#review-orphaned-and-deleted-entries}

The **[!UICONTROL Orphaned in ACO]** and **[!UICONTROL Deleted]** tabs cover two cases the connector cannot repair automatically because there is no [!DNL Adobe Commerce] shared catalog to reconcile against:

- **[!UICONTROL Orphaned in ACO]**—A catalog view or restricted access key exists in [!DNL Adobe Commerce Optimizer] but was not created by the connector. This is common if a catalog view was created manually in [!DNL Adobe Commerce Optimizer] Studio before the [!DNL Adobe Commerce Optimizer Connector for B2B] extension was enabled, or by a partner integration unrelated to the connector. If the catalog view is not needed, remove it directly from the catalog view configuration in [!DNL Adobe Commerce Optimizer] Studio.

- **[!UICONTROL Deleted]**—You deleted a shared catalog in [!DNL Adobe Commerce], and its catalog view projection was subsequently removed. These rows are kept for 90 days as a record of what was removed.

## Known limitations

- There is no visual indicator in [!DNL Adobe Commerce Optimizer] Studio distinguishing connector-managed catalog views, policies, price books, and keys from ones you create manually.
- There is no deep link from this page directly to the corresponding catalog view in [!DNL Adobe Commerce Optimizer] Studio yet, except through the **[!UICONTROL Open in ACO admin]** row action.

>[!MORELIKETHIS]
>
> - <!-- Uncomment link when Admin Guide changes are published [Catalog View Sync Status monitoring](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status){target="_blank"} — Full documentation reference for the Catalog View Sync Status page, in the *Commerce Admin Guide* -->
> - [Manage data synchronization](data-sync-status.md) — Verify product, price, and category feed sync
> - [Private catalog views](/help/optimizer/setup/private-catalog-view.md) — Learn what a connector-managed private catalog view is
> - [Restricted access keys](/help/optimizer/setup/restricted-access-keys.md) — Learn how connector-managed keys work
> - [Monitor B2B shared catalog changes](get-started.md#monitor-b2b-shared-catalog-changes) — Learn what the connector automates for B2B shared catalogs
