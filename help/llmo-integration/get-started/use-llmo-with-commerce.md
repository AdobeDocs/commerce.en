---
title: Use [!DNL Adobe LLM Optimizer] with [!DNL Adobe Commerce]
description: Navigate Commerce opportunities in LLM Optimizer, review PDP and catalog enrichment, deploy updates to [!DNL Adobe Commerce], verify in the Admin and storefront, and learn how overrides and ingestion mark opportunities stale.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Use [!DNL Adobe LLM Optimizer] with [!DNL Adobe Commerce]

After [connecting Commerce to LLM Optimizer](connect-to-llmo.md), merchandisers and admins work primarily in the **[!DNL Adobe LLM Optimizer]** UI to review opportunities and, when ready, push approved changes into the catalog. This topic describes Commerce-relevant optimization types, how to move through the **[!UICONTROL Opportunities]** experience, deploy behavior in [!DNL Adobe Commerce], and how external updates interact with LLM Optimizer suggestions. For architecture context (Catalog Agent, MCP, AI visibility), see the [integration overview](../overview.md).

## Understand Commerce optimizations in LLM Optimizer

LLM Optimizer surfaces more than one kind of improvement. At a high level:

| Focus | What it addresses |
| --- | --- |
| **[!UICONTROL Product Detail Page Enrichment]** (PDP enrichment) | Storefront PDP changes so **agent-visible** content better reflects product knowledge—often including a non-disruptive enrichment layer—without replacing your human merchandising layout. |
| **[!UICONTROL Product Catalog Enrichment]** | **Human-visible** catalog fields such as **product name** and **product description**, with suggestions tied to specific SKUs or URLs and deploy to Commerce core catalog data. |

Use the **[!UICONTROL Opportunities]** area to see which type applies to a given URL or SKU. Agent-visible or structured metadata recommendations may appear as separate guidance; follow in-product labels for those workflows.

## Navigate Commerce opportunities {#navigate-commerce-opportunities}

**To open Commerce-related opportunities:**

1. In the left rail, click **[!UICONTROL Opportunities]**.
1. Apply the **[!UICONTROL Commerce]** (or **[!UICONTROL Commerce opportunities]**) filter so the list shows optimization types that target your [!DNL Adobe Commerce] catalog or storefront.
1. Select the card for **[!UICONTROL Product Detail Page Enrichment]** or **[!UICONTROL Product Catalog Enrichment]** depending on what you want to work on.

![Commerce Opportunities](../assets/llmo-opportunities.png)

Inside an opportunity, you typically work across tabs or sections such as **[!UICONTROL Current suggestions]**, **[!UICONTROL Fixed suggestions]**, **[!UICONTROL Ignored suggestions]**, and **[!UICONTROL Deploy optimizations]** (exact names can vary by release). Search or filter by **SKU** or URL to find a product row.

## Review and deploy PDP enrichment

PDP enrichment is meant to improve what **bots and models** can read from a product URL while you confirm the **shopper-visible** page still looks correct.

1. Open **[!UICONTROL Product Detail Page Enrichment]** from **[!UICONTROL Opportunities]** (see [Navigate Commerce opportunities](#navigate-commerce-opportunities)).
1. On **[!UICONTROL Current suggestions]** (or the equivalent), locate your SKU or URL and click **[!UICONTROL Preview]** to open the proposed enrichment. Content is grounded in your Commerce catalog but structured for AI consumption.
1. Select the row for the SKU you want to change, then click **[!UICONTROL Deploy optimization]** and confirm.

After deploy, re-check the live PDP: the **human** view should match your expectations (for example, expandable sections unchanged where the product is designed that way). If your team uses optional **AI Content Visibility** tooling, run the same **human versus agent** comparison you used before deploy—the **agent** view should now include enrichment that was previously missing or unstructured.

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

On **[!UICONTROL Current suggestions]**, expand a product row to see **current** and **suggested** name and description side by side. Suggested copy often reads as a stronger **product narrative** (use cases and intent) than a bare SKU-style label—compare carefully before you deploy.

## Deploy catalog updates to Adobe Commerce

When you choose **[!UICONTROL Deploy optimization]** for product name or description:

- LLM Optimizer sends an update request to **[!DNL Adobe Commerce]** for the affected **SKU**.
- **Name and description are updated in the main catalog tables** used by the Admin. After a successful deploy, workflows that read those attributes—such as the product grid—should show the **LLM Optimizer-approved** values without extra manual steps in Commerce.

>[!IMPORTANT]
>
>Treat deploy as a **production catalog change**. Use your normal change-control, staging, and QA practices. Deploy only after merchandising and SEO stakeholders agree on the final copy.

Select the product, set the checkboxes for **product name** and/or **product description** to match what you want to push, click **[!UICONTROL Deploy optimization]**, and confirm. Catalog Agent writes the approved values into your [!DNL Adobe Commerce] catalog.

### Verify catalog enrichment in the Admin

1. Log in to the [!DNL Adobe Commerce] **Admin**.
1. Go to **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.
1. Use filters and the **store view** selector as needed (for example, **[!UICONTROL Default Store View]**), then search for the **SKU**.
1. Open the product in edit mode.

The grid and product form should show the **LLM Optimizer**-approved name and, under **[!UICONTROL Content]**, the updated **description** when you deployed description changes.

If the form shows an option such as **[!UICONTROL Override LLM Optimizer Provided Product Name]** (label may vary by release), you can use it to prefer a manually entered name while keeping merchandising control. Manual catalog edits can mark related LLM Optimizer opportunities **stale**; see [Manual override in the Admin](#manual-override-in-the-admin).

### Verify catalog enrichment on the storefront

Search for the SKU on your storefront and open the PDP. Confirm that the **name** and any storefront regions that surface the long **description** reflect what you approved, in addition to checking downstream channels that consume the same catalog attributes.

### PDP enrichment deploy and rollback

If your project includes **PDP enrichment** opportunities, deploy and **rollback** behavior may support **bulk** or **per-URL** actions depending on the capability. Follow LLM Optimizer UI options for rollback; Commerce core name/description rollback for **[!UICONTROL Product Catalog Enrichment]** is effectively a new catalog edit or a follow-up opportunity, not a separate "undo" button in Commerce unless your team implements one.

## Overrides, ingestion, and stale opportunities

After LLM Optimizer updates a product's name or description, other systems may change the same fields. Behavior distinguishes *Admin* edits from **automated ingestion** (REST API, CSV import, PIM feed, and similar).

### Ingestion sends the original catalog value again

If an external process writes the **original** name or description (the value that existed before LLM Optimizer's deploy), **Commerce continues to honor the LLM Optimizer-deployed value** for that field according to the integration rules. The opportunity may not revert automatically based on that ingestion alone.

### Ingestion sends a genuinely new value

If the external process sends a **new** value that is not merely a repeat of the pre-LLM Optimizer text—for example, renaming "Red Shoes" to "Iconic Red Shoes"—that **new** catalog value is **honored**, and the related LLM Optimizer opportunity is typically marked **stale** because the live catalog no longer matches the suggestion context.

### Manual override in the Admin {#manual-override-in-the-admin}

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
