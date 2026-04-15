---
title: Integrate [!DNL Adobe Commerce] with [!DNL Adobe LLM Optimizer]
description: Connect [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer] to monitor catalog signals in LLMs and deploy approved catalog optimizations.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Integrate [!DNL Adobe Commerce] with [!DNL Adobe LLM Optimizer]

[!DNL Adobe LLM Optimizer] is an enterprise solution that helps brands monitor, analyze, and optimize how their content appears in answers from large language models (LLMs) and AI assistants. As shoppers increasingly use AI tools for research and product discovery, LLM Optimizer helps ensure that your brand and catalog are cited accurately and surfaced in context.

This guide describes how **[!DNL Adobe Commerce]** fits into that workflow when your product catalog lives in Commerce: what becomes possible, what you must set up, and how deployed optimizations behave in the Admin and across ingestion channels.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] is a standalone Adobe solution. Core monitoring and opportunity workflows do not require [!DNL Adobe Experience Manager] (AEM) or other Adobe applications. Commerce-specific **deploy** actions apply only when your catalog is connected and you choose to push approved changes into [!DNL Adobe Commerce].

## What the integration enables

Connecting LLM Optimizer to your [!DNL Adobe Commerce] catalog lets you move from broad content insights to **catalog-aware** recommendations:

- **Identify** gaps and inconsistencies that affect how LLMs interpret your products (for example, titles, descriptions, and structured signals).
- **Review** suggested improvements with context such as justification and before/after comparisons.
- **Deploy** selected optimizations—for example, **product name and product description** updates—directly into the Commerce catalog so Admin workflows, grids, and storefront-facing data stay aligned.

When the catalog source is [!DNL Adobe Commerce], Adobe can support the full loop: auto-identify opportunities, suggest changes, and apply fixes you approve. For catalogs that originate outside Commerce, LLM Optimizer can still analyze and suggest improvements; applying changes depends on your integration model (for example, a mirrored catalog or manual updates). See [Integration limits and boundaries](boundaries-limits.md).

## Who this is for

- **Digital marketers and merchandisers** who want product data to be accurate and consistent in LLM-driven answers and who need a controlled way to improve catalog copy at scale.
- **Commerce administrators** who own catalog integrity, Admin processes, and integrations (API, CSV, PIM) that feed product attributes.

## Prerequisites

- Your organization is entitled to use [!DNL Adobe LLM Optimizer] and has completed any required onboarding in Experience Cloud.
- **Your storefront can be crawled** by LLM-oriented and agentic bots where that is part of your LLM Optimizer measurement and optimization strategy (a general prerequisite for catalog-aware insights).
- For Commerce-backed deploy workflows, **required Commerce services and catalog connectivity** are enabled and healthy. Task-level setup is described in [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md).

### High-level data flow

Conceptually, catalog optimizations follow two patterns (your project may use one or both, depending on capability):

| Direction | Purpose |
| --- | --- |
| **Commerce catalog -> LLM Optimizer** | Catalog and URL signals feed analysis, opportunities, and suggestions in the LLM Optimizer UI. |
| **LLM Optimizer -> Commerce** | After you approve a deploy action, updates—for example to **product name** and **description** stored in the main Commerce catalog—are written so the Admin and downstream channels reflect the optimized values. |

PDP-focused enrichments and other optimization types may follow product-specific deploy paths (for example, edge or experience-layer updates). The exact surfaces depend on your LLM Optimizer configuration and release. See [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md).

### [!DNL Adobe Commerce] compared with third-party catalogs

| Catalog source | Typical LLM Optimizer coverage |
| --- | --- |
| **[!DNL Adobe Commerce]** | Strong support for identification and suggestions, plus **deploy** of approved catalog field updates you configure. |
| **Third-party commerce** | Identification and suggestions are supported; automated **deploy** into the merchant system depends on exporting, mirroring, or partner workflows rather than direct writes to Commerce core tables. |

## Catalog Agent, Storefront MCP, and LLM Optimizer {#catalog-agent-and-mcp}

Your [!DNL Adobe Commerce] **product catalog** is the system of record for product data: names, descriptions, attributes, pricing, and inventory. To power AI-assisted discovery and optimization, that catalog must be reachable in a consistent, machine-readable way.

**Adobe Commerce Storefront MCP** (Model Context Protocol) is a structured interface between your live Commerce data and Adobe AI experiences. Think of it as a contract that lets agents ask natural-language questions about your catalog—for example, which products match a use case or attribute—and receive answers grounded in **current** Commerce data, not a static export alone.

**Catalog Agent** sits on top of that layer. It enables [!DNL Adobe LLM Optimizer] to **query**, **enrich**, and **act on** catalog and PDP context in near real time: identifying gaps, proposing improvements, and (where you approve) deploying changes. Catalog Agent capabilities are surfaced through LLM Optimizer workflows described in this guide and in [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md).

## How Catalog Agent improves Commerce for LLMs {#catalog-agent-optimizations}

Catalog Agent addresses discoverability through two complementary optimizations. Labels in the LLM Optimizer UI may vary slightly by release; use the **[!UICONTROL Commerce]** (or equivalent) opportunities filter to find Commerce-backed types.

### Product detail page enrichment {#pdp-enrichment-overview}

**Product detail page (PDP) enrichment** analyzes storefront PDPs and aligns **agent-visible** content with product knowledge that already exists in Commerce—often including information that appears to shoppers only after they expand a section or interact with a widget. The typical outcome is a **hidden or non-disruptive enrichment layer**: structured, intent-aligned data that LLM-oriented crawlers can consume **without** changing the core human-visible merchandising layout you designed.

After you deploy PDP enrichment, you should still validate that the **shopper-facing** experience matches expectations (for example, no unintended visual changes). Optional browser tooling (such as an **AI Content Visibility Checker** where your organization provides it) can compare a **human** view of the page with an **agent** view to illustrate what bots can extract before and after enrichment.

### Product catalog enrichment {#catalog-enrichment-overview}

**[!UICONTROL Product Catalog Enrichment]** (or **product catalog enrichment**) focuses on **human-visible** catalog fields—especially **product name** and **product description**—that many LLM crawlers and feeds rely on. Catalog Agent audits for sparse, vague, or inconsistent copy, proposes **suggested** name and description values with justification, and can **deploy** approved text **into** [!DNL Adobe Commerce] so the Admin, storefront, and downstream channels that read from the catalog inherit the update.

Because catalog enrichment writes to the **source** in Commerce, you **enrich once** and every channel that consumes those attributes can benefit (subject to your indexing and sync timing).

## Product narratives and shopper intent {#product-narrative}

A **product narrative** is natural-language copy that explains **value**, **use cases**, and **intent**—not only SKU-style labels or specs. LLM Optimizer and Catalog Agent aim to move key fields from "identifier-only" text toward narratives that both **shoppers** and **models** can interpret consistently. Human review before deploy remains essential for brand voice, legal claims, and SEO.

For step-by-step navigation, deploy, and verification in your own tenant, follow [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md#navigate-commerce-opportunities) together with [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md).

## Related topics

- [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md)
- [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Integration limits and boundaries](boundaries-limits.md)
