---
title: Troubleshoot the Adobe Commerce Optimizer Connector
description: Diagnose and fix common issues with the Adobe Commerce Optimizer Connector, including credential failures, data sync problems, and scope configuration issues.
feature: Integration, Configuration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---

# Troubleshoot the Adobe Commerce Optimizer Connector

## Credentials or tenant validation fails

If `aco:config:init` fails during credential validation:

- Run `bin/magento aco:config:show` to verify the stored values
- Confirm that the tenant ID belongs to the IMS organization used to obtain the credentials
- Confirm that the OAuth client has the necessary scopes for the Adobe Commerce Optimizer Ingestion service (see [Obtain IMS Credentials](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials))

## Data not syncing

**Check item-level error details:**

1. In the Commerce Admin, go to **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.
2. Select the failing feed to view per-item error details.

Key points about error handling:

- **400 errors** are not retried. Inspect the payload for malformed or missing required fields. See [Field Mappings](reference/field-mappings.md) for the expected format.
- **5xx errors** are automatically retried by the `*_resend_failed_items` cron job (runs every 5 minutes).

**Check scope configuration:**

If the problem affects only a specific catalog source (store view code) or price book, check whether the corresponding website or store view has sync disabled. See [Customize the data export configuration](./get-started.md#customize-the-commerce-scopes-export-configuration).


## SaaS Data Export diagnostics

For lower-level SaaS Data Export diagnostics, including log locations and feed resync commands, see the [SaaS Data Export troubleshooting guide](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/logs-troubleshooting/troubleshooting-logging){target="_blank"}.
