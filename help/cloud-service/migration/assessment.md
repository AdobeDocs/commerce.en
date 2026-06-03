---
title: Migration Assessment Tool
description: Learn how to read an Adobe Commerce PaaS migration assessment report, interpret storefront and backend complexity signals, and use Adobe AI developer tools to begin building extensions for Adobe Commerce as a Cloud Service.
feature: Cloud, Migration
role: Developer, Admin
level: Intermediate
---

# Migration Assessment Tool

> [!IMPORTANT]
>
> The Migration Assessment Tool is only available when migrating from [!DNL Adobe Commerce on Cloud Infrastructure] or [!DNL Adobe Commerce on-premises] projects to [!DNL Adobe Commerce as a Cloud Service].

A Commerce migration assessment is an automated analysis of your existing Adobe Commerce store. Adobe's tooling scans your store's codebase and produces a structured report that inventories everything built, customized, or modified — and maps that inventory to what it means for your migration to [!DNL Adobe Commerce as a Cloud Service].

The report is delivered as an HTML file that opens in any browser. No access to your production environment is required beyond sharing your project codebase.

**The assessment provides:**

- A complete inventory of every module in your store, organized by type and impact level
- A Migration Complexity rating (High, Medium, or Low) computed from five risk-predictive metrics in your store
- A prioritized view of the highest-impact backend and storefront areas requiring migration planning
- A plain-language description of each custom module usable as direct input for Adobe's AI developer tools

>[!TIP]
>
>Contact your Solution Account Manager to request an assessment on your existing instance.

## Understanding the migration assessment report

The report is organized into three tabs: **[!UICONTROL Summary]**, **[!UICONTROL Module Reports]**, and **[!UICONTROL Report Reliability]**.

## Summary tab

The **[!UICONTROL Summary]** tab is your at-a-glance view. It surfaces key signals organized into these areas: Migration Complexity, File Type Breakdown, Highest-Impact Modules, Migration Drivers, and Customization Breakdown.

### Migration complexity

The Migration Complexity section contains the headline rating for your store overall — the first thing to read every time you open a report.

**Migration Complexity and Complexity Score**

The Complexity Score is a weighted composite number computed from five inputs that are each available on the **[!UICONTROL Summary]** page. The formula weights each input by how much it predicts migration difficulty:

| Input | Weight | Why it carries this weight |
| --- | --- | --- |
| Core table modifications | ×3.0 | The only irreversible signal. Modifications to core database tables cannot be rebuilt — they must be preserved and kept in sync with every future platform schema change. |
| Chain conflicts | ×2.0 | The primary cause of silent runtime breakage. When two plugins intercept the same function and one fails to pass control forward, features stop working with no error message. |
| Critical preferences | ×1.5 | Class preferences fully replace a core Commerce class. Any platform upgrade that changes that class breaks the preference silently. |
| High-impact modules | ×1.0 | Baseline weight. High-impact modules have a defined remediation path (Rebuild, Refactor, Replace, or Remove), so risk is proportional to count rather than compounding. |
| Total modules | ×0.3 | Scope tiebreaker only. Module count indicates how much there is to do, not how hard it is — included to differentiate otherwise similar profiles at different implementation scales. |

The formula is:

```text
score = (core_table_mods × 3.0)
      + (chain_conflicts × 2.0)
      + (critical_prefs × 1.5)
      + (high_impact_mods × 1.0)
      + (total_modules × 0.3)
```

The Complexity Score maps to a Migration Complexity rating using fixed thresholds:

| Rating | Score range | Typical migration approach |
| --- | --- | --- |
| Low | 150 or below | Standard playbook. Direct migration with payment provider coordination and data migration as parallel workstreams. |
| Medium | 151–375 | Modular migration in waves. Conflict triage per high-impact module cluster before scheduling. |
| High | Above 375 | Automated conflict graph tooling mandatory before scoping. Phased program of 12–24 months — no single cutover. |

>[!NOTE]
>
>These thresholds are absolute values, not percentiles. A score of 150 means the same thing regardless of how many other stores have been assessed — the rating does not drift as the assessed population grows.

**Custom Module Ratio**

The percentage of your store's modules that were built specifically for your implementation, rather than included standard with [!DNL Adobe Commerce]. A higher ratio means more custom code must be audited and migrated. The average across assessed customers is approximately 62%.

>[!TIP]
>
>Custom Module Ratio is a scope signal, not a complexity signal. A store with 80% custom modules can be simpler to migrate than one with 40% if the custom modules are isolated and low-risk. Use the Complexity Score and chain conflict count to assess difficulty, and the Custom Module Ratio to estimate volume.

**Highest-Impact Modules**

A shortlist of the specific modules in your store requiring the most migration attention — typically those touching checkout, payments, and order management. Each high-impact module needs its own migration plan. This list is the best starting point for conversations with your technical team.

### Migration drivers

The Migration Drivers section shows the five primary categories of customization driving your complexity rating.

| Driver | What it measures |
| --- | --- |
| Customization Footprint | The overall volume of custom code relative to total implementation |
| Plugins and Observers | Code that intercepts core platform behavior at runtime |
| Class Preferences | The most fragile customization pattern — replaces core classes entirely, breaks silently on upgrades |
| Data Model | Custom and modified database structures |
| Integrations | External systems connected to your store |

Each driver appears with a High, Medium, or Low signal. Address the highest-rated drivers first when scoping and planning.

## Customization breakdown

The Customization Breakdown section provides detailed metrics across every category of customization in your store. Not all subsections appear in every report — only the categories detected in your codebase are shown. Subsections that affect the front-end presentation layer are a distinct workstream from backend code migration and typically require separate planning conversations.

>[!NOTE]
>
>A store can have low backend complexity and high front-end complexity. Always review both backend and storefront-related subsections before scoping migration effort.

### Data Model

The Data Model section shows a count of custom tables, modifications to [!DNL Adobe Commerce]'s core database tables, and critical EAV (Entity-Attribute-Value) attributes.

Core table modifications are the hardest category to migrate — they create dependencies on a specific platform schema version and carry the highest weight (×3.0) in the Complexity Score formula.

>[!TIP]
>
>If your report shows more than 15–20 core table modifications, plan a dedicated data migration workstream before scoping backend module migration.

### Layout XML

The number of Layout XML files and the total operation count within them. Layout XML defines the structure of every page: which blocks appear, in which containers, and under which page types. A high file count with many operations signals significant page-structure customization that must be re-architected for ACAS.

### Core handle overrides

The number of places where your Layout XML overrides a core [!DNL Adobe Commerce] page handle (for example, `checkout_cart_index` or `catalog_product_view`). Core handle overrides are the highest-risk layout signal — they modify page structure at the platform level and require explicit rebuilding on ACAS.

| Override count | Signal |
| --- | --- |
| 0 | No core layout overrides |
| 1–3 | Runtime risk — each override needs explicit ACAS layout rebuild |
| 4 or more | Critical — plan a dedicated layout migration sprint |

### Blocks

The number of block and template (`.phtml`) files in your store. Blocks are the primary server-side rendering artifacts — each represents a discrete migration task.

| Block count | Signal |
| --- | --- |
| Under 100 | Baseline — standard effort |
| 100–300 | Medium — plan a structured front-end wave |
| Over 300 | High — prioritize as a dedicated workstream |

### High-risk blocks

Blocks that touch core render paths — checkout rendering, cart display, and similar load-bearing front-end surfaces. Any high-risk blocks require individual migration assessment before scheduling.

### Themes & Email Templates

The namespace of your store's custom theme (for example, `BrandName_Theme`). The presence of a custom theme means a full theme rebuild is required on ACAS. Every assessed store with a custom theme namespace must plan a dedicated front-end migration workstream.

### Template overrides (core modified)

The number of core [!DNL Adobe Commerce] `.phtml` templates that have been overridden. Each core template override creates a dependency on a specific version of that template. Platform updates that change the template break the override silently.

### Drop-in migration required

[!DNL Adobe Commerce as a Cloud Service] uses a modular Drop-in component architecture for storefront surfaces including checkout, cart, and product detail. If your store has customized these surfaces — for example, adding custom checkout steps, modifying cart display logic, or extending the product detail page — those customizations must be rebuilt as Drop-in components on ACAS.

This field identifies which storefront areas require Drop-in rebuilds.

>[!IMPORTANT]
>
>If **Checkout** is listed as a Drop-in migration requirement, plan a dedicated checkout Drop-in workstream. This is the most complex and business-critical storefront migration task.

## Use the Module Reports tab

The **[!UICONTROL Module Reports]** tab contains a dedicated entry for every module in your store. This is the most actionable part of the report for your technical team.

For each module, the report shows:

| Field | What it tells you |
| --- | --- |
| What it does | A plain-language description of the module's purpose and business function |
| Impact level | High, Medium, or Low — based on what commerce behavior the module touches |
| Hook count | How many places this module intercepts core platform behavior |
| Migration recommendation | Rebuild, Refactor, Replace with a native ACAS feature, or Remove |
| Dependencies | Which other modules this module interacts with, informing migration sequencing |

**To work through the Module Reports tab:**

1. Filter to **High-impact** modules first. These drive the most migration effort and cost.
1. For each module, determine: Is this still actively used? Could it be replaced by a native ACAS feature? If it must be rebuilt, what does it need to do?
1. Identify modules that can be retired or replaced. Each one reduces migration scope before any code is written.
1. Copy the plain-language description of each module marked Rebuild. These descriptions are direct input for Adobe's AI developer tools — see [Begin development with Adobe's AI tools](#begin-development-with-adobes-ai-tools) below.

## Reference: key terms

| Term | Plain-language meaning |
| --- | --- |
| Module | A self-contained package of functionality — like an app on a smartphone. Your store has dozens to hundreds of these. |
| Plugin (interceptor) | Code that intercepts a Commerce function and changes its behavior before, during, or after it runs. |
| Observer | Code that listens for a specific platform event (such as "order placed") and runs custom logic when that event fires. |
| Preference (class override) | The most fragile customization type — completely replaces a core Commerce class. Breaks silently when the platform upgrades that class. |
| Chain conflict | When two or more plugins intercept the same function and one fails to pass control to the next. Can cause features to stop working silently, with no error message. |
| Core table modification | A structural change to Commerce's built-in database tables. Creates an irreversible dependency on a specific platform schema version. Carries the highest weight in the Complexity Score formula. |
| EAV attribute | A flexible custom field added to products or customers (for example, a custom "warranty period" field). High EAV counts increase data migration complexity. |
| Hook density | The average number of plugins and observers per module. Higher density means customization is more tightly woven into the core platform. |
| Drop-in | [!DNL Adobe Commerce as a Cloud Service]'s modular approach to storefront components (checkout, cart, product detail). Custom checkout behavior on PaaS typically requires a Drop-in rebuild on ACAS. |
| App Builder | Adobe's out-of-process extensibility platform — the recommended way to build custom functionality on ACAS, replacing in-process PHP extensions. |
| Layout XML | Configuration files that define which blocks appear on which pages. Custom Layout XML must be re-architected for ACAS's page structure. |
| Core handle override | A Layout XML customization that modifies a core Commerce page structure globally — the highest-risk layout pattern for migration. |

## Begin development with Adobe's AI tools

The plain-language module descriptions in the **[!UICONTROL Module Reports]** tab are direct input for Adobe's AI developer tooling. Developers can take a module description and use it as a natural-language prompt to scaffold, build, and deploy an ACAS-compatible replacement extension — without starting from a blank page.

### What the tools provide

[Adobe's AI developer tools for Commerce extensibility](https://developer.adobe.com/commerce/extensibility/developer-agent/) include two primary capabilities.

**Adobe Commerce App Builder MCP server**

A Model Context Protocol (MCP) integration that connects AI coding assistants — including [!DNL Cursor] and [!DNL GitHub Copilot] — directly to [!DNL Adobe Commerce] documentation, APIs, and App Builder development patterns. Developers describe what they want to build in plain language; the MCP server provides Commerce-aware code generation, architecture guidance, and deployment automation within the IDE.

**Agent skills**

Pre-built AI skills covering the most common Commerce extensibility patterns: REST APIs, checkout extensions, storefront components, event-driven integrations, and more. Skills guide the AI through architecture, implementation, testing, and deployment steps specific to ACAS and App Builder.

### Use assessment output as AI input

1. Open the **[!UICONTROL Module Reports]** tab and find a High-impact module with a Rebuild recommendation.
1. Read the module's plain-language description — for example: *"Manages custom shipping rate calculations based on customer account tier and order weight thresholds."*
1. Open your IDE ([!DNL Cursor] or [!DNL VS Code] with [!DNL GitHub Copilot]) with the Commerce extensibility MCP server enabled.
1. Use the module description as your prompt to the AI agent.
1. Review the scaffolded App Builder application and iterate with the agent to refine the implementation.

>[!TIP]
>
>The assessment gives you the blueprint. The AI tools let your team start building against it immediately — before a full migration plan is finalized.

### Set up the tooling

**Prerequisites:** Node.js 22.x, npm 9.0.0 or higher, Adobe I/O CLI.

To install the Commerce extensibility tools, run:

```bash
aio commerce extensibility tools-setup
```

This installs the App Builder MCP server, agent skills, and IDE configuration. For full installation instructions including IDE configuration for [!DNL Cursor] and [!DNL GitHub Copilot], see [Coding tools setup](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools/).

### Resources

| Resource | Link |
| --- | --- |
| AI developer tools overview | [developer.adobe.com/commerce/extensibility/developer-agent/](https://developer.adobe.com/commerce/extensibility/developer-agent/) |
| Coding tools setup | [Coding tools setup](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools/) |
| Skills, prompts, and commands | [Skills and prompts](https://developer.adobe.com/commerce/extensibility/developer-agent/skills-and-prompts/) |
| Use cases | [Use cases](https://developer.adobe.com/commerce/extensibility/developer-agent/use-cases/) |
| Best practices | [Best practices](https://developer.adobe.com/commerce/extensibility/developer-agent/best-practices/) |
| Ratings extension tutorial | [Ratings extension tutorial](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/tutorials/ratings-extension) |
| Shipping method tutorial | [Shipping method tutorial](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/tutorials/shipping-method-extension) |
| Storefront AI skills | [Storefront AI skills](https://experienceleague.adobe.com/developer/commerce/storefront/boilerplate/ai-agent-skills/) |

## Next steps

1. Open the **[!UICONTROL Summary]** tab. Review Migration Complexity and Highest-Impact Modules, then check the Customization Breakdown subsections. If your store has a custom theme, high-risk blocks, or a Checkout Drop-in listed, plan a parallel front-end workstream alongside backend migration.
1. Share the **[!UICONTROL Module Reports]** tab with your technical team or development partner. Ask them to flag any modules that are no longer actively used or that could be replaced by a native ACAS feature.
1. Start building. Use the plain-language module descriptions as AI tool input to begin scaffolding ACAS-compatible extensions before a full migration plan is finalized.
1. Schedule a walkthrough call with your Adobe account team. Adobe reviews the findings with you, answers questions about specific modules and storefront signals, and helps map out the migration approach for your complexity profile.

## Related documentation

- [Adobe Commerce as a Cloud Service overview](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview)
- [App Builder extensibility](https://developer.adobe.com/commerce/extensibility/)
- [Integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)
- [Checkout starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/)
- [Adobe Commerce migration overview](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/migration/overview)
