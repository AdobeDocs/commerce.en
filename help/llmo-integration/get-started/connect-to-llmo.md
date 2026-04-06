---
title: Connect [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer]
description: Enable Commerce catalog services, configure the LLMO connection, validate catalog access, and confirm tenant readiness before you review opportunities or deploy updates.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Connect [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer]

Use this task-based guide after your organization has access to [!DNL Adobe LLM Optimizer]. The goal is to make your [!DNL Adobe Commerce] catalog available to LLMO and to confirm that tenant and environment context is correct before you review opportunities or deploy catalog updates.

>[!NOTE]
>
>This guide does not replace LLMO product documentation for the Experience Cloud UI. Use it together with in-product guidance and your Adobe account team for org-specific settings.

## Before you begin

- **No storefront migration** is required solely to connect the catalog for LLMO; you are enabling services and integration points, not replatforming the storefront.
- **No AEM dependency** exists for core LLMO functionality tied to Commerce catalog analysis and deploy workflows described in this integration guide.
- Complete **catalog-related Commerce services** setup (for example, data export or SaaS catalog services your project uses) *before* or in parallel with the LLMO connection step, so LLMO does not point at an empty or stale catalog feed.

## Step 1. Enable required Commerce services

Work with your Commerce administrator or implementation partner to ensure that:

- Catalog data that LLMO must read is **exported or synchronized** according to your architecture (including any SaaS data exporter or connector your deployment uses).
- API access, credentials, and environment URLs (sandbox vs production) match the **tenant** you intend to use in LLMO.

If you are unsure which services apply, confirm with Adobe support or your solution architect for your Commerce edition and hosting model.

## Step 2. Configure the connection in LLMO

In the [!DNL Adobe LLM Optimizer] UI:

1. Open the integration or connection settings for **[!DNL Adobe Commerce]** (exact navigation and control labels depend on your LLMO release).
1. Provide the identifiers and credentials your onboarding materials specify—typically tied to your **Experience Cloud organization**, **Commerce environment**, and catalog feed or API configuration.
1. Save the connection and wait for any **initial sync** or validation job to complete.

Configure this step **after** catalog services are available so validation succeeds on first connect.

## Step 3. Validate catalog access

Confirm that LLMO can see your catalog:

- **Spot-check** categories or sample SKUs that you know exist in Commerce.
- Resolve **authentication or scope** errors before you rely on opportunities or deploy actions in production.

## Step 4. Confirm tenant and environment readiness

- Verify that connected **sandbox** projects are not mixed with **production** Commerce data unless intentional.
- Align **user roles** in Experience Cloud and Commerce so the people who approve deploy actions have the right permissions on both sides.

## Next steps

- [Use LLM Optimizer with Adobe Commerce](use-llmo-with-commerce.md) — review opportunities, deploy catalog updates, and understand override behavior.
- [Integration overview](../overview.md) — architecture and Commerce vs third-party catalogs.
