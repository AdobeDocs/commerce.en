---
title: 'Symptoms and Resolutions for the [!DNL Adobe Commerce Optimizer Connector]'
description: "Diagnose and resolve unexpected behavior in [!DNL Adobe Commerce Optimizer Connector] caused by misconfiguration or misinterpretation of sync results."
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
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---

# Symptoms and resolutions for the [!DNL SaaS Data Export]

This page describes behaviors you may observe when working with the [!DNL SaaS Data Export] that are typically caused by misconfiguration or misinterpretation of sync results. Use the descriptions below to identify the root cause and apply the appropriate resolution.

## Configurable or bundle product is enabled in [!DNL Adobe Commerce] but disabled or missing in Adobe Commerce SaaS services

**Symptom:** A configurable or bundle product has **Enabled** status in [!DNL Adobe Commerce] but is either not returned in the storefront or appears with a **Disabled** status in services.

**Likely cause:** The effective status of composite products depends on the status of their child products, not just the parent product status. Adobe Commerce SaaS services reflects this computed status:

- **Configurable products** - at least one product variant must be enabled.
- **Bundle products** - at least one product must be enabled for each required bundle option.

If these conditions are not met, the parent product is treated as disabled even if its own status is set to **Enabled**.

**Resolution:**

- For configurable products, verify that at least one associated simple product variant is enabled and assigned to the correct website and store view.
- For bundle products, check that each required bundle option has at least one enabled child product. A required option with all disabled children causes the entire bundle to be treated as disabled.
- After enabling the appropriate child products, trigger a resync or wait for the next scheduled sync, then confirm the updated status in services.

## Prices not updated after catalog price rule activation

**Symptom:** After activating a catalog price rule using the Scheduled Update feature, prices are not updated. The `commerce-data-export.log` shows `synced: 0` for `prices` feed after scheduled updates are applied.

**Likely cause:** A race condition can occur between cron groups when Scheduled Updates are used for catalog price rules. The `catalog_data_exporter_product_prices` indexer may run before its dependency, the `catalogrule_product` index, has finished rebuilding. As a result, the price exporter reads stale data and exports no changes.

**Resolution:**

Issue will be fixed in `Adobe Commerce` following releases. In the meantime, configure both cron groups to run sequentially to eliminate the race condition:

1. Go to **Stores** > **Configuration** > **Advanced** > **System** > **Cron (Scheduled Tasks)**.
1. Set **Use Separate Process** to **No** for both:
   - Cron configuration options for group: **index**
   - Cron configuration options for group: **staging**
1. Flush the configuration cache after saving.

>[!NOTE]
>
>With both groups running in-process and sequentially, a slow full reindex blocks staging from running until it finishes. On large catalogs, this may delay staging updates.

## Catalog data discrepancy between Adobe Commerce and connected services

**Symptom:** Product data shown in connected Commerce Services (such as [!DNL Live Search] or [!DNL Product Recommendations]) does not match the catalog data in [!DNL Adobe Commerce]. For example, a product name, price, or description appears outdated or incorrect on the storefront.

**Likely cause:** After a resync is triggered, it can take up to an hour for the data to update and be reflected in UI components. If the discrepancy persists beyond that window, the item may not have been picked up by the last sync, or the sync did not detect a change because the feed data was already marked as up to date.

**Resolution:**

1. In the storefront search results, select the product in question to open its detailed view.
1. Copy the JSON output and verify that it matches what you have in the [!DNL Commerce] catalog.
1. If the content does not match, make a minor edit to the product in your catalog, such as adding a space or a period, to force the change to be detected.
1. Wait for a resync or trigger a manual resync from the CLI or the [Data Feed Sync Status dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status).

## Data sync is not running on schedule

**Symptom:** The data sync does not run on schedule, or no items are being synced despite product changes in [!DNL Adobe Commerce].

**Likely cause:** The most common causes are cron jobs not running or indexers not configured in **Update by Schedule** mode.

**Resolution:**

- [Confirm that cron jobs are running](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verify that the indexers for the following feeds are set to **Update by Schedule**: Catalog Attributes, Product, Product Overrides, and Product Variant. Check from [Index Management](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) in the Admin or using the CLI: `bin/magento indexer:show-mode | grep -i feed`.

For additional troubleshooting, see this [KnowledgeBase article](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce).

## Catalog sync has a Failed status

**Symptom:** The catalog sync shows a **Failed** status on the Data Feed Sync Status page.

**Likely cause:** An unrecoverable error occurred during the data collection or submission phase. Common causes include API authentication issues, network errors, or data validation failures.

**Resolution:**

1. Review the data export error logs for details on the failure:
   - `var/log/commerce-data-export-errors.log` for errors during data collection.
   - `var/log/saas-export-errors.log` for errors during data submission.
1. If the error is not related to configuration or a third-party extension, [submit a support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) with the relevant log entries.

## Log shows "operation skipped - process locked" messages

**Symptom:** The `commerce-data-export.log` file contains entries similar to the following:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**Likely cause:** This is expected behavior, not an error. The message appears when a cron-triggered partial sync attempts to run while a full reindex or `saas:resync` is already in progress. The [!DNL SaaS Data Export] extension uses a feed lock mechanism to prevent conflicting concurrent sync operations.

**Resolution:**

No action is required. Once the running process completes and releases the lock, the next cron execution picks up and syncs any pending changes. For details on how the lock mechanism works, see [Feed lock mechanism for SaaS Data Export](../feed-lock-mechanism.md).
