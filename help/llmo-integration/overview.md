---
title: Integrate [!DNL Adobe Commerce] with [!DNL Adobe LLM Optimizer]
description: Connect [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer] to monitor catalog signals in LLMs and deploy approved catalog optimizations.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Integrate [!DNL Adobe Commerce] with [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>This feature is in [beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta).

[!DNL Adobe LLM Optimizer] is an enterprise solution that helps brands monitor, analyze, and optimize how their content appears in answers from large language models (LLMs) and AI assistants. As shoppers increasingly use AI tools for research and product discovery, LLM Optimizer helps ensure that your brand and catalog are cited accurately and surfaced in context.

This guide describes how **[!DNL Adobe Commerce]** fits into that workflow when your product catalog lives in Commerce: what becomes possible, what you must set up, and how deployed optimizations behave in the Admin and across ingestion channels.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] is a standalone Adobe solution. Core monitoring and opportunity workflows do not require [!DNL Adobe Experience Manager] (AEM) or other Adobe applications. Commerce-specific deploy actions apply only when your catalog is connected and you choose to push approved changes into [!DNL Adobe Commerce].

## What the integration enables {#what-integration-enables}

Connecting LLM Optimizer to your [!DNL Adobe Commerce] catalog lets you move from broad content insights to **catalog-aware** recommendations:

- **Identify** gaps and inconsistencies that affect how LLMs interpret your products (for example, titles, descriptions, and structured signals).
- **Review** suggested improvements with context such as justification and before/after comparisons.
- **Deploy** selected optimizations—for example, product name and product description updates—directly into the Commerce catalog so Admin workflows, grids, and storefront-facing data stay aligned.

When the catalog source is [!DNL Adobe Commerce], Adobe can support the full loop: auto-identify opportunities, suggest changes, and apply fixes you approve. For catalogs that originate outside Commerce, LLM Optimizer can still analyze and suggest improvements; applying changes depends on your integration model (for example, a mirrored catalog or manual updates). See [Integration limits and boundaries](boundaries-limits.md).

## Who this is for {#who-this-is-for}

- **Digital marketers and merchandisers** who want product data to be accurate and consistent in LLM-driven answers and who need a controlled way to improve catalog copy at scale.
- **Commerce administrators** who own catalog integrity, Admin processes, and integrations (API, CSV, PIM) that feed product attributes.

## Prerequisites {#prerequisites}

- Your organization is entitled to use [!DNL Adobe LLM Optimizer] and has completed any required onboarding in Experience Cloud.
- Your storefront can be crawled by LLM-oriented and agentic bots where that is part of your LLM Optimizer measurement and optimization strategy (a general prerequisite for catalog-aware insights).
- For Commerce-backed deploy workflows, required Commerce services and catalog connectivity are enabled and healthy. Task-level setup is described in [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md).

You should also understand how data moves between systems:

### High-level data flow {#high-level-data-flow}

Conceptually, catalog optimizations follow two patterns (your project may use one or both, depending on capability):

| Direction | Purpose |
| --- | --- |
| **Commerce catalog -> LLM Optimizer** | Catalog and URL signals feed opportunities and suggestions in the LLM Optimizer UI. |
| **LLM Optimizer -> Commerce** | After you approve a deploy action, updates to product name and description stored in the main Commerce catalog are written so the Admin and storefront reflect the optimized values. |

### [!DNL Adobe Commerce] compared with third-party catalogs {#commerce-vs-third-party}

| Catalog source | Typical LLM Optimizer coverage |
| --- | --- |
| **[!DNL Adobe Commerce]** | Strong support for identification and suggestions, plus deploy of approved catalog field updates you configure. |
| **Third-party commerce** | Identification and suggestions are supported; automated deploy into the merchant system depends on exporting, mirroring, or partner workflows rather than direct writes to Commerce core tables. |

## Catalog Agent, Storefront MCP, and LLM Optimizer {#catalog-agent-and-mcp}

Your [!DNL Adobe Commerce] **product catalog** is the system of record for product data: names, descriptions, attributes, pricing, and inventory. To power AI-assisted discovery and optimization, **Adobe Commerce Storefront MCP** (Model Context Protocol) is a structured interface between your live Commerce data and Adobe AI experiences.

**Catalog Agent** sits on top of the Storefront MCP. Catalog Agent enables [!DNL Adobe LLM Optimizer] to query, enrich, and act on catalog and PDP context by identifying gaps, proposing improvements, and deploying changes when you approve them. Those capabilities surface in LLM Optimizer workflows described in [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md).

## How Catalog Agent improves Commerce for LLMs {#catalog-agent-optimizations}

Catalog Agent addresses discoverability through two complementary optimizations: product detail page enrichment and product catalog enrichment.

### Product detail page enrichment {#pdp-enrichment-overview}

Product detail page (PDP) enrichment analyzes storefront PDPs and aligns agent-visible content with product knowledge that already exists in Commerce—often including information that appears to shoppers only after they expand a section or interact with a widget. The typical outcome is a hidden or non-disruptive enrichment layer: structured, intent-aligned data that LLM-oriented crawlers can consume without changing the core human-visible merchandising layout you designed.

After you deploy PDP enrichment, you should still validate that the shopper-facing experience matches expectations (for example, no unintended visual changes). Optional browser tooling (such as an AI Content Visibility Checker where your organization provides it) can compare a human view of the page with an agent view to illustrate what bots can extract before and after enrichment.

### Product catalog enrichment {#catalog-enrichment-overview}

Product catalog enrichment focuses on **human-visible** catalog fields, such as **product name** and **product description**. Many LLM crawlers and feeds rely on those fields. **Catalog Agent** audits for sparse, vague, or inconsistent copy, proposes suggested name and description values with justification, and can deploy approved text into [!DNL Adobe Commerce] so the Admin, storefront, and downstream channels that read from the catalog inherit the update.

Because catalog enrichment writes to the **source** in Commerce, you **enrich once** and every channel that consumes those attributes can benefit (subject to your indexing and sync timing).

## Related topics {#related-topics}

- [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md)
- [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Integration limits and boundaries](boundaries-limits.md)
