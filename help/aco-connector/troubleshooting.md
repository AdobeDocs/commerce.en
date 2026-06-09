---
title: Troubleshoot the Adobe Commerce Optimizer Connector
description: Learn how to troubleshoot [!DNL Adobe Commerce Optimizer Connector] credential, catalog sync, and scope export issues for Adobe Commerce PaaS integrations.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
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
# Troubleshoot the Adobe Commerce Optimizer Connector

Use this guide to diagnose and resolve common issues with the Adobe Commerce Optimizer Connector during initial setup, catalog feed synchronization, and scope export configuration. The sections below cover credential and tenant validation, data sync failures, and related SaaS Data Export diagnostics.

## Credentials or tenant validation fails

If `aco:config:init` fails during credential validation:

- Run the `bin/magento aco:config:show` Commerce CLI command to verify the stored values.
- Confirm that the tenant ID belongs to the IMS organization used to obtain the credentials.
- Confirm that the OAuth client has the necessary scopes for the Adobe Commerce Optimizer ingestion service (see [Obtain IMS Credentials](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)).

## Data not syncing

**Check item-level error details:**

1. From the Commerce Admin, go to **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.
2. Select the failing feed to view per-item error details.

Key points about error handling:

- **400 errors** are not retried. Inspect the payload for malformed or missing required fields. See [Field mapping for Adobe Commerce Optimizer Connector feeds](reference/field-mapping.md) for the expected format.
- **5xx errors** are automatically retried by the `*_resend_failed_items` cron job (runs every 5 minutes).

**Check scope configuration:**

If the problem affects only a specific catalog source (store view code) or price book, check whether the corresponding website or store view has sync disabled. See [Customize the data export configuration](./get-started.md#customize-the-commerce-scopes-export-configuration).

## SaaS Data Export diagnostics

For lower-level SaaS Data Export diagnostics including log locations and feed resync commands, see the [SaaS Data Export troubleshooting guide](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/logs-troubleshooting/troubleshooting-logging){target="_blank"}.
