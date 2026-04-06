---
title: Integrate [!DNL Adobe Commerce] with [!DNL Adobe LLM Optimizer]
description: Connect [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer] to monitor catalog signals in LLMs and deploy approved catalog optimizations.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Integrate [!DNL Adobe Commerce] with [!DNL Adobe LLM Optimizer]

[!DNL Adobe LLM Optimizer] (LLMO) is an enterprise solution that helps brands monitor, analyze, and optimize how their content appears in answers from large language models (LLMs) and AI assistants. As shoppers increasingly use AI tools for research and product discovery, LLMO helps ensure that your brand and catalog are cited accurately and surfaced in context.

This guide describes how **[!DNL Adobe Commerce]** fits into that workflow when your product catalog lives in Commerce: what becomes possible, what you must set up, and how deployed optimizations behave in the Admin and across ingestion channels.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] is a standalone Adobe solution. Core monitoring and opportunity workflows do not require [!DNL Adobe Experience Manager] (AEM) or other Adobe applications. Commerce-specific **deploy** actions apply only when your catalog is connected and you choose to push approved changes into [!DNL Adobe Commerce].

## What the integration enables

Connecting LLMO to your [!DNL Adobe Commerce] catalog lets you move from broad content insights to **catalog-aware** recommendations:

- **Identify** gaps and inconsistencies that affect how LLMs interpret your products (for example, titles, descriptions, and structured signals).
- **Review** suggested improvements with context such as justification and before/after comparisons.
- **Deploy** selected optimizations—for example, **product name and product description** updates—directly into the Commerce catalog so Admin workflows, grids, and storefront-facing data stay aligned.

When the catalog source is [!DNL Adobe Commerce], Adobe can support the full loop: auto-identify opportunities, suggest changes, and apply fixes you approve. For catalogs that originate outside Commerce, LLMO can still analyze and suggest improvements; applying changes depends on your integration model (for example, a mirrored catalog or manual updates). See [Integration limits and boundaries](boundaries-limits.md).

## Who this is for

- **Digital marketers and merchandisers** who want product data to be accurate and consistent in LLM-driven answers and who need a controlled way to improve catalog copy at scale.
- **Commerce administrators** who own catalog integrity, Admin processes, and integrations (API, CSV, PIM) that feed product attributes.

## Prerequisites and architecture

### Prerequisites

- Your organization is entitled to use [!DNL Adobe LLM Optimizer] and has completed any required onboarding in Experience Cloud.
- **Your storefront can be crawled** by LLM-oriented and agentic bots where that is part of your LLMO measurement and optimization strategy (a general prerequisite for catalog-aware insights).
- For Commerce-backed deploy workflows, **required Commerce services and catalog connectivity** are enabled and healthy. Task-level setup is described in [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md).

### High-level data flow

Conceptually, catalog optimizations follow two patterns (your project may use one or both, depending on capability):

| Direction | Purpose |
| --- | --- |
| **Commerce catalog → LLMO** | Catalog and URL signals feed analysis, opportunities, and suggestions in the LLMO UI. |
| **LLMO → Commerce** | After you approve a deploy action, updates—for example to **product name** and **description** stored in the main Commerce catalog—are written so the Admin and downstream channels reflect the optimized values. |

PDP-focused enrichments and other optimization types may follow product-specific deploy paths (for example, edge or experience-layer updates). The exact surfaces depend on your LLMO configuration and release. See [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md).

### [!DNL Adobe Commerce] compared with third-party catalogs

| Catalog source | Typical LLMO coverage |
| --- | --- |
| **[!DNL Adobe Commerce]** | Strong support for identification and suggestions, plus **deploy** of approved catalog field updates you configure. |
| **Third-party commerce** | Identification and suggestions are supported; automated **deploy** into the merchant system depends on exporting, mirroring, or partner workflows rather than direct writes to Commerce core tables. |

## Related topics

- [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md)
- [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Integration limits and boundaries](boundaries-limits.md)
