---
title: Design a Commerce Platform for Shoppers and AI Agents
description: Learn how to build a commerce platform that serves human shoppers and AI agents from a single source of truth, from catalog design and MCP to telemetry.
role: Developer, Leader
recommendations: noCatalog
autotag-review: '2026-10-20T20:32:40.424Z'
TQID: 'https://experienceleague.adobe.com/ub4oTxr4IfLGgqqz0S1npY-sn0FZb3mKq-GdjD9eDjI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
    internal-label: Data quality
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
---

# Design a commerce platform for shoppers and AI agents

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Portrait of Surya Lamech" src="../../assets/guidance-and-insights/agentic-commerce-author-avatar-slamech.png" width="96"></td>
   <td valign="middle" style="vertical-align: middle;"><strong>Surya Lamech</strong><br><em>Principal Product Marketing Manager</em></td>
</tr>
</table>

![Hero illustration of an agentic commerce platform where humans and AI agents interact with a single source of truth](../../assets/guidance-and-insights/agentic-commerce-hero.png "The architectural foundations of an agentic commerce platform")

*Designing a commerce platform where humans and AI agents interact with a single source of truth.*

Commerce is undergoing a structural shift. Customers are no longer relying solely on search engines or browsing storefronts to explore their options. Instead, they are turning to LLM-powered interfaces, chat-based assistants, and agentic shopping tools to ask questions, compare products across retailers, and accelerate early-stage decision-making.

These interfaces are powerful engines for discovery, education, and comparison. They help customers clarify needs, evaluate trade-offs, and narrow choices faster than traditional browsing.

Yet when it comes time to complete a purchase, customers still overwhelmingly prefer trusted storefronts and brand-owned sites where payment security, fulfillment transparency, and post-purchase service are well understood. Conversion remains anchored in environments where trust has already been established.

Importantly, AI does not disappear at this stage. When customers arrive on a brand's owned storefront, agentic AI can enhance the experience by guiding product selection, personalizing recommendations in real time, answering objections, bundling complementary items, and streamlining checkout. In these trusted environments, AI becomes a conversion accelerator, improving completion rates, and increasing average order value.

To compete in this new landscape, enterprises need a commerce foundation that is **structured, governed, and optimized for both human and agent consumption**. Adobe Commerce is built for this shift, and the principles below outline what it takes to be truly agent-ready.

## A commerce architecture built for two audiences

![Diagram showing storefronts and apps for humans on the left and chat assistants and autonomous agents on the right, both drawing from a central Commerce Core of products, pricing, inventory, promotions, cart, and checkout that is exposed through APIs and MCP](../../assets/guidance-and-insights/agentic-commerce-foundational-model.png){width="800" zoomable="yes"}

*What customers see and what agents consume stay consistent, accurate, and on-brand.*

The modern commerce stack must now serve two equally important audiences: people and AI agents. Human-facing experiences like storefronts and apps remain essential for engagement, brand expression, and building customer loyalty. But alongside them sits a rapidly expanding agent-facing surface: machine-readable endpoints that supply LLMs and autonomous agents with structured facts, governed content, and transactional capabilities.

Agents perform best when working with clean, structured data delivered through predictable APIs rather than attempting to interpret JavaScript or infer business rules from presentation layers. That means product specifications, pricing, availability, and promotional logic must exist as addressable resources exposed through APIs and standardized interfaces such as MCP servers. When both human- and agent-facing surfaces draw from the same underlying source of truth, brands ensure that what customers see and what agents consume remain consistent, accurate, and on-brand.

This dual-surface architecture is the foundation of agentic commerce.

## A catalog designed for machine reasoning

![Diagram showing structured product entities (SKUs, attributes, variants, bundles, pricing, and availability) shaped by catalog layers and policies, then delivered through catalog views to a brand storefront, marketplace, partner feed, mobile app, and AI or agent surface](../../assets/guidance-and-insights/agentic-commerce-agent-interaction.png){width="800" zoomable="yes"}

*One governed source of truth, shaped per channel without ever forking the product data.*

The catalog is the core of agentic commerce. It must be structured for machines, governed for compliance, and flexible enough to support the full range of human and agent interactions. Adobe Commerce's catalog model built around catalog views, policies, layers, and structured product entities is designed for this future.

Catalog views define where and how product data is exposed, whether to a storefront, marketplace, partner feed, or AI surface. Each view can carry its own product availability, pricing, and attribute visibility rules, ensuring that the right information reaches the right consumer or agent. Catalog layers enable you to enrich product data for specific channels without modifying the source product data. Policies govern customer eligibility, inventory logic, pricing, and compliance constraints. Combined, enterprises have precise control over what catalog data an agent can access or act upon.

## MCPs as the common language for agents

![Diagram showing shopping assistants, support agents, and developer tools sending requests through the Model Context Protocol, which includes the Commerce MCP and Developer MCP, to Adobe Commerce capabilities such as cart creation, checkout, payments, inventory, and promotions and returns](../../assets/guidance-and-insights/agentic-commerce-reference-stack.png){width="800" zoomable="yes"}

*MCP standardizes how agents request actions in natural intent, and Adobe Commerce carries them out as governed, deterministic actions.*

For Agentic Commerce to function end-to-end, ecommerce platforms must support standardized protocols that allow agents to execute actions securely such as cart creation, checkout initiation, payment orchestration, inventory validation, promotions, and returns.

Through native support for Model Context Protocol (MCP), Adobe structures and exposes commerce capabilities in a way that LLMs can interpret consistently. MCP standardizes how product data, business rules, and transactional context are presented to LLMs, ensuring agents can reason over them reliably while enterprises maintain governance and control. With the Commerce MCP, businesses can build custom agentic experiences like shopping assistants, agentic cart creation, support agents, and much more.

The Developer MCP brings AI-powered development capabilities that enable teams to rapidly extend platform functionality and deploy composable storefront components. By embedding Adobe's knowledge sources, documentation, and platform best practices directly into the development workflow, the Developer MCP helps new developers onboard faster and become productive from their first sprint. It generates code that follows proven architectural patterns, is easy to maintain, and meets the quality standards that enterprise commerce demands. The result is an accelerated path from idea to production, giving enterprises the speed to experiment, iterate, and ship commerce capabilities ahead of competitors.

Adobe is also committed to supporting agentic commerce protocols such as Agentic Commerce Protocol (ACP) and Universal Commerce Protocol (UCP), enabling product discovery and secure, standards-based transactional interactions between agents and your storefront.

By embracing open protocols rather than point integrations, Adobe ensures commerce interactions are governed, deterministic, and secure while enabling a new model of agent-to-merchant engagement where trusted agents can transact directly under clearly defined policies.

## Telemetry and continuous optimization

In an AI-mediated ecosystem, telemetry becomes the strategic advantage. Businesses need visibility into how their brand is represented across LLMs, how accurately agents represent their content, how agent-referred traffic converts, and where governance or compliance issues arise. They also need operational telemetry that tracks agent execution and anomaly detection across agent interactions.

Adobe gives you visibility into how your products appear in LLMs, enhances product data with AI, and increases readability of your data by LLMS. By adding meaningful context to your catalog, it helps LLMs not only discover your products accurately, but understand what they are, who they are for, and why they matter to customers.

Additionally, your product detail pages that have been optimized for human consumption can often have data that is invisible to agents. This data could be hidden behind modals, configurators, and linked pages. Agents may not fully understand product categories, bundles, and variants. Adobe can identify this critical missing information and deploy it as JSON-LD to the edge so agents can get all the relevant product data.

Through this constant telemetry and optimization brands can ensure maximum visibility and stay competitive across LLMs.

## Why this matters

Ecommerce is no longer confined to storefronts and search results. LLMs and autonomous agents increasingly mediate discovery, evaluation, and transactions. This shift changes the mechanics of visibility, the dynamics of control, and the foundations of trust. The brands that win will architect for an AI-native foundation.

## Related guidance

* [Catalog views](/help/optimizer/setup/catalog-view.md)
* [Catalog layers](/help/optimizer/setup/catalog-layer.md)
* [Policies](/help/optimizer/setup/policies.md)
* [AI coding developer tooling for Adobe Commerce App Builder](/help/cloud-service/migration/coding-tools.md)
* [Commerce APIs](../../apis/commerce-apis.md)
* [Commerce Developer Agent playlist](https://experienceleague.adobe.com/en/playlists/commerce-developer-agent)—Watch technical videos on setting up and using the Commerce Developer Agent.
