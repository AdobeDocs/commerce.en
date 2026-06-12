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

# Symptoms and resolutions for the Adobe Commerce Optimizer Connector

This page describes behaviors you may observe when working with the [!DNL Adobe Commerce Optimizer Connector] that are typically caused by misconfiguration or misinterpretation of sync results. Use the descriptions below to identify the root cause and apply the appropriate resolution.

## Feed status shows "Success" but data is not visible in [!DNL Adobe Commerce Optimizer]

**Symptom:** The **[!UICONTROL Data Feed Sync Status]** page reports a successful sync, but products, prices, etc. are not appearing as expected in [!DNL Adobe Commerce Optimizer].

**Likely cause:** A successful feed status means the data was accepted by the ingestion endpoint, not that it has finished propagating through [!DNL Adobe Commerce Optimizer]. Propagation can take several minutes after ingestion.

**Resolution:**

- Wait a few minutes and refresh the [!DNL Adobe Commerce Optimizer] view.
- Confirm that the tenant ID configured in [!DNL Adobe Commerce] matches the [!DNL Commerce Optimizer] environment you are checking.
- Verify that the correct [catalog source](../../optimizer/setup/catalog-source.md) (store view code) or price book is selected in [!DNL Commerce Optimizer].

## Products are missing from the exported catalog

**Symptom:** Some products do not appear in [!DNL Adobe Commerce Optimizer] after a full catalog sync.

**Resolution:**

- Confirm that the affected products are assigned to the website and store view used as the catalog source.
- Check that the products are enabled and set to a visibility that includes catalog listings.
- Review per-item error details for the catalog feed in **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

## Configurable or bundle product is enabled in [!DNL Adobe Commerce] but disabled or missing in [!DNL Adobe Commerce Optimizer]

**Symptom:** A configurable or bundle product has **Enabled** status in [!DNL Adobe Commerce] but is either not returned in the storefront or appears with a **Disabled** status in [!DNL Adobe Commerce Optimizer].

**Likely cause:** The effective status of composite products depends on the status of their child products, not just the parent product status. [!DNL Adobe Commerce Optimizer] reflects this computed status:

- **Configurable products** - at least one product variant must be enabled.
- **Bundle products** - at least one product must be enabled for each required bundle option.

If these conditions are not met, the parent product is treated as disabled even if its own status is set to **Enabled**.

**Resolution:**

- For configurable products, verify that at least one associated simple product variant is enabled and assigned to the correct website and store view.
- For bundle products, check that each required bundle option has at least one enabled child product. A required option with all disabled children causes the entire bundle to be treated as disabled.
- After enabling the appropriate child products, trigger a resync or wait for the next scheduled sync, then confirm the updated status in [!DNL Adobe Commerce Optimizer].

## Prices are incorrect or missing in [!DNL Adobe Commerce Optimizer]

**Symptom:** Products appear in [!DNL Adobe Commerce Optimizer] but display no price returned with [products GraphQL query](https://developer.adobe.com/commerce/services/reference/graphql/#products), or the price does not match what is configured in [!DNL Adobe Commerce] w

**Resolution:**

The price book feed uses a scope that maps to a specific website and customer group. A wrong [catalog view](../../optimizer/setup/catalog-view.md) configuration can lead to missing or incorrect prices.

- Verify that the website is configured for sync in the connector's export configuration. See [Customize the data export configuration](../get-started.md#customize-the-commerce-scopes-export-configuration).
- Confirm that the price book ID used in [!DNL Commerce Optimizer] present in [catalog view](../../optimizer/setup/catalog-view.md) configuration used to perform the products query.

