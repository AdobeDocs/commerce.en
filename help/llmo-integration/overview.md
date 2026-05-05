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
>Access to this integration is restricted. Contact your Technical Account Manager for details.

[!DNL Adobe LLM Optimizer] is an enterprise solution that helps brands monitor, analyze, and optimize how their content appears in answers from large language models (LLMs) and AI assistants. As shoppers increasingly use AI tools for research and product discovery, LLM Optimizer helps ensure that your brand and catalog are cited accurately and surfaced in context.

This guide describes how **[!DNL Adobe Commerce]** fits into that workflow when your product catalog is stored in Commerce. You'll learn what capabilities become available, what configuration is required, and how deployed optimizations behave in the Admin and across ingestion channels.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] is a standalone Adobe solution. Core monitoring and opportunity workflows do not require [!DNL Adobe Experience Manager] (AEM) or other Adobe applications. Commerce-specific deploy actions apply only when your catalog is connected to LLM Optimizer and you choose to push approved changes into [!DNL Adobe Commerce].

## What the integration enables {#what-integration-enables}

Connecting LLM Optimizer to your [!DNL Adobe Commerce] catalog lets you move from broad content insights to **catalog-aware** recommendations:

- **Identify** gaps and inconsistencies in catalog data–such as titles, descriptions, and structured signals–that affect how LLMs interpret your products.
- **Review** suggested improvements with supporting context, including justifications and before-and-after comparisons.
- **Deploy** selected optimizations—such as product name and description updates—directly to the Commerce catalog ensuring that Admin workflows, grids, and storefront-facing data stay aligned.

When the catalog source is [!DNL Adobe Commerce], Adobe can support the full end-to-end workflow: automatically identifying opportunities, suggesting changes, and applying approved fixes. For catalogs that originate outside Commerce, LLM Optimizer can still analyze and suggest improvements, but applying changes depends on your integration model (for example, a mirrored catalog or manual updates). See [Integration limits and boundaries](boundaries-limits.md).

## Who this is for {#who-this-is-for}

- **Digital marketers and merchandisers** who want product data to be accurate and consistent in LLM-driven answers and who need a controlled way to improve catalog copy at scale.
- **Commerce administrators** who own catalog integrity, Admin processes, and integrations (API, CSV, PIM) that feed product attributes.

## Prerequisites {#prerequisites}

The following prerequisites apply when you have **access** to the Adobe Commerce integration with Adobe LLM Optimizer. Contact your Technical Account Manager for details.

- Your storefront can be crawled by LLM-oriented and agentic bots where this crawl capability is part of your LLM Optimizer measurement and optimization strategy (a general prerequisite for catalog-aware insights).
- For Commerce-backed deploy workflows, required Commerce services and catalog connectivity are enabled and healthy. Task-level setup is described in [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md).

You should also understand how data moves between systems:

### High-level data flow {#high-level-data-flow}

Conceptually, catalog optimizations follow two patterns (your project may use one or both, depending on capability):

| Direction | Purpose |
| --- | --- |
| **Commerce catalog -> LLM Optimizer** | Catalog and URL signals feed opportunities and suggestions in the LLM Optimizer UI. |
| **LLM Optimizer -> Commerce** | After you approve a deploy action, updates to product name and description are written to the main Commerce catalog so that both the Admin and storefront reflect the optimized values. |

### [!DNL Adobe Commerce] compared with third-party catalogs {#commerce-vs-third-party}

| Catalog source | Typical LLM Optimizer coverage |
| --- | --- |
| **[!DNL Adobe Commerce]** | Strong support for identification and suggestions, plus deploy of approved catalog field updates you configure. |
| **Third-party commerce** | Identification and suggestions are supported; automated deploy into the merchant system depends on exporting, mirroring, or partner workflows rather than direct writes to the merchant's source catalog. |

## Catalog Agent, Storefront MCP, and LLM Optimizer {#catalog-agent-and-mcp}

Your [!DNL Adobe Commerce] **product catalog** is the system of record for product data: names, descriptions, attributes, pricing, and inventory. To power AI-assisted discovery and optimization, **Adobe Commerce Storefront MCP** (Model Context Protocol) is a structured interface between your live Commerce catalog data and Adobe AI experiences.

**Catalog Agent** sits on top of the Storefront MCP. Catalog Agent enables [!DNL Adobe LLM Optimizer] to query, enrich, and act on catalog and PDP context by identifying gaps, proposing improvements, and deploying changes when you approve them. Those capabilities surface in LLM Optimizer workflows described in [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md).

## How Catalog Agent improves Commerce for LLMs {#catalog-agent-optimizations}

Catalog Agent addresses discoverability through two complementary optimizations: product detail page enrichment and product catalog enrichment.

### Product detail page enrichment {#pdp-enrichment-overview}

**Product detail page (PDP) enrichment** suggests refinements to product page content so your merchandise reads more clearly when shoppers discover products through AI assistants and similar tools. The goal is to improve clarity and consistency without changing the storefront layout your team already merchandised. You review suggestions in LLM Optimizer and deploy when you are ready.

After you deploy, spot-check the live product page to confirm the shopping experience still looks as you expect.

### Product catalog enrichment {#catalog-enrichment-overview}

**Product catalog enrichment** suggests clearer **product names** and **product descriptions** where copy is thin, vague, or inconsistent. Each suggestion includes context so your team can decide what to change. When you approve an update, it can be applied to your [!DNL Adobe Commerce] catalog so the Admin, storefront, and other experiences that use those fields reflect the same wording.

Because those fields live in Commerce, improving a name or description once can benefit every channel that reads that product data (depending on how and when your systems refresh).

## Related topics {#related-topics}

- [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md)
- [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Integration limits and boundaries](boundaries-limits.md)
