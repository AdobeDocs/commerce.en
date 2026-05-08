---
title: Connect [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer]
description: Enable required Commerce services, configure the LLM Optimizer connection, validate catalog access, and confirm tenant readiness before reviewing opportunities or deploying updates.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Connect [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>Access to this integration is restricted. Contact your Technical Account Manager for details.

This article explains how to connect your [!DNL Adobe Commerce] catalog available to LLM Optimizer.

>[!NOTE]
>
>This article focuses on the Commerce side of the integration. For general information about LLM Optimizer, see the [LLM Optimizer product documentation](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/home).

## Enable required Commerce services {#enable-commerce-services}

Work with your Commerce administrator or implementation partner to ensure the following:

- Catalog data that LLM Optimizer must read is **exported or synchronized** according to your architecture (including any SaaS data exporter or connector in your deployment).
- API access, credentials, and environment URLs (sandbox vs production) match the **tenant** you intend to use in LLM Optimizer.

## Configure the Commerce connection in LLM Optimizer {#configure-commerce-connection}

**To configure the Commerce connection:**

1. In the [!DNL Adobe LLM Optimizer] UI, open **Customer Configuration**, then select the **[!UICONTROL Commerce]** tab.

   ![Commerce configuration on the Customer Configuration tab](../assets/llmo-commerce-config.png)

1. Click **[!UICONTROL Add Store View]** to create a new row, or expand an existing store view entry to edit it.
1. Enter the **[!UICONTROL Store View URL]** (required).

    Use the storefront URL for that store view, including any locale or path prefix (for example, `https://brand.example.com/` or `https://brand.example.com/fr/`).

1. Enter the **[!UICONTROL Environment ID]** (required)—the identifier for the Adobe Commerce environment that LLM Optimizer should connect to.
1. Enter **[!UICONTROL Website Code]**, **[!UICONTROL Store Code]**, and **[!UICONTROL Store View Code]** (required).

    These values must match the codes in your Commerce Admin for the website, store, and store view you connect.

1. Optional: Enter **[!UICONTROL Host Name]** with the hostname of your Commerce instance (for example, `www.example.com`) if that value is different from the URL.
1. Enter the **[!UICONTROL Adobe Commerce Endpoint]**—the base URL of your Adobe Commerce instance used for API access.
1. Enter or paste the **[!UICONTROL API Key]** used to authenticate requests to Commerce APIs.

    Click **[!UICONTROL Copy]** next to the field if you need to copy the key elsewhere securely.

1. Click **[!UICONTROL Save]** to store the configuration.

After you save, wait for any **initial sync** or validation job to complete before relying on catalog or audit results for that store view.

To remove a store view configuration, open that entry and click **[!UICONTROL Delete]**.

### Field descriptions {#commerce-connection-fields}

| Field | Description |
| --- | --- |
| Store View URL | Public URL of the store view LLM Optimizer should treat as in scope for catalog and audit workflows. |
| Environment ID | Commerce environment identifier (from your cloud or deployment documentation, or Admin where applicable). |
| Website code | Commerce **[!UICONTROL Website Code]** for the website that owns the catalog. |
| Store code | Commerce **[!UICONTROL Store Code]** for the store under that website. |
| Store view code | Commerce **[!UICONTROL Store View Code]** for the store view (for example, `default`). |
| Host name | Hostname of the Commerce storefront or instance when the form asks for it in addition to other URLs. |
| Adobe Commerce Endpoint | Instance URL LLM Optimizer uses to reach Commerce APIs. |
| API key | Secret key for API authentication; treat it like any production credential. |

## Confirm tenant and environment readiness {#confirm-tenant-readiness}

- Verify that connected **sandbox** projects are not mixed with **production** Commerce data, unless  this is intentional.
- Align **user roles** in Experience Cloud and Commerce so the people who approve deploy actions have the right permissions on both sides.

## Next steps {#next-steps}

[Use LLM Optimizer with Adobe Commerce](use-llmo-with-commerce.md) to review opportunities, deploy catalog updates, and understand override behavior.
