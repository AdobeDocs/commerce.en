---
title: Use [!DNL Adobe LLM Optimizer] with [!DNL Adobe Commerce]
description: Review catalog opportunities in LLM Optimizer, deploy product name and description updates to [!DNL Adobe Commerce], and learn how overrides and ingestion mark opportunities stale.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Use [!DNL Adobe LLM Optimizer] with [!DNL Adobe Commerce]

After [connecting Commerce to LLM Optimizer](connect-to-llmo.md), merchandisers and admins work primarily in the **[!DNL Adobe LLM Optimizer]** UI to review opportunities and, when ready, push approved changes into the catalog. This topic describes Commerce-relevant optimization types, the **[!UICONTROL Product Catalog Enrichment]** workflow, deploy behavior in [!DNL Adobe Commerce], and how external updates interact with LLM Optimizer suggestions.

## Understand Commerce optimizations in LLM Optimizer

LLM Optimizer surfaces more than one kind of improvement. At a high level:

| Focus | What it addresses |
| --- | --- |
| **PDP enrichment** | Page- and URL-level improvements so product detail content is clearer or more complete for LLM-oriented consumption (behavior and deploy path depend on your LLM Optimizer configuration). |
| **[!UICONTROL Product Catalog Enrichment]** | **Human-visible** catalog fields such as **product name** and **product description**, with suggestions tied to specific SKUs or URLs. |

Use the **[!UICONTROL Opportunities]** experience to see which type applies to a given URL or SKU. Agent-visible or structured metadata recommendations may appear as separate guidance; follow in-product labels for those workflows.

## Review the Product Catalog Enrichment opportunity

In the **[!UICONTROL Opportunities]** area, open the optimization card for **[!UICONTROL Product Catalog Enrichment]** (name may vary slightly by release). The detail experience follows standard LLM Optimizer patterns and typically includes:

1. **[!UICONTROL Overview]** — what the optimization does and why it matters.
1. **[!UICONTROL Guidance]** — Adobe's point of view on how the change helps discovery and accuracy in LLM contexts.
1. **[!UICONTROL Opportunity Plan]** — recommended steps to evaluate and roll out the change.
1. **[!UICONTROL URLs with Suggestions]** — storefront URLs where an opportunity was identified.

For each suggestion you can:

- Compare **current** versus **proposed** product name and description.
- **Edit** the proposed text before deployment if you want a hybrid version.
- Choose to deploy **name only**, **description only**, or **both**.
- Read the **justification** that explains why LLM Optimizer proposed the change.

## Deploy catalog updates to Adobe Commerce

When you choose **[!UICONTROL Deploy optimization]** for product name or description:

- LLM Optimizer sends an update request to **[!DNL Adobe Commerce]** for the affected **SKU**.
- **Name and description are updated in the main catalog tables** used by the Admin. After a successful deploy, workflows that read those attributes—such as the product grid—should show the **LLM Optimizer-approved** values without extra manual steps in Commerce.

>[!IMPORTANT]
>
>Treat deploy as a **production catalog change**. Use your normal change-control, staging, and QA practices. Deploy only after merchandising and SEO stakeholders agree on the final copy.

### PDP enrichment deploy and rollback

If your project includes **PDP enrichment** opportunities, deploy and **rollback** behavior may support **bulk** or **per-URL** actions depending on the capability. Follow LLM Optimizer UI options for rollback; Commerce core name/description rollback for **[!UICONTROL Product Catalog Enrichment]** is effectively a new catalog edit or a follow-up opportunity, not a separate "undo" button in Commerce unless your team implements one.

## Overrides, ingestion, and stale opportunities

After LLM Optimizer updates a product's name or description, other systems may change the same fields. Behavior distinguishes *Admin* edits from **automated ingestion** (REST API, CSV import, PIM feed, and similar).

### Ingestion sends the original catalog value again

If an external process writes the **original** name or description (the value that existed before LLM Optimizer's deploy), **Commerce continues to honor the LLM Optimizer-deployed value** for that field according to the integration rules. The opportunity may not revert automatically based on that ingestion alone.

### Ingestion sends a genuinely new value

If the external process sends a **new** value that is not merely a repeat of the pre-LLM Optimizer text—for example, renaming "Red Shoes" to "Iconic Red Shoes"—that **new** catalog value is **honored**, and the related LLM Optimizer opportunity is typically marked **stale** because the live catalog no longer matches the suggestion context.

### Manual override in the Admin

If a user **manually** edits the product name or description in the [!DNL Adobe Commerce] *Admin* UI:

- The *Admin* value **wins** as the system of record for that manual change.
- The LLM Optimizer opportunity is marked **stale**.
- In LLM Optimizer, the UI returns toward showing the **original** state relative to that opportunity so you can re-baseline or accept a new suggestion if analysis runs again.

These rules help teams know whether LLM Optimizer, feeds, or *Admin* edits are authoritative when multiple channels touch the same SKU.

## Best practices

- **Coordinate with SEO and brand** before bulk deploy of titles or descriptions.
- **Document** which systems own name and description so PIM or feed jobs do not unintentionally conflict with LLM Optimizer expectations.
- **Re-sync** or re-analyze after major catalog imports so opportunities reflect the current catalog.

## Related topics

- [Connect Adobe Commerce to LLM Optimizer](connect-to-llmo.md)
- [Integration overview](../overview.md)
- [Integration limits and boundaries](../boundaries-limits.md)
