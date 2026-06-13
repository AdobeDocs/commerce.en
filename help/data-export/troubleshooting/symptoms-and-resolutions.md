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
