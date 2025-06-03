---
title: 'Migrate to [!DNL Adobe Commerce as a Cloud Service]'
description: Learn how to migrate to [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Migration guide to [!DNL Adobe Commerce as a Cloud Service] overview

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] provides a comprehensive guide for developers transitioning an existing Adobe Commerce PaaS implementation to the new Adobe Commerce as a Cloud Service (SaaS) offering. Adobe Commerce as a Cloud Service represents a significant shift to a fully managed, versionless SaaS model, offering enhanced performance, scalability, simplified operations, and tighter integration with the broader Adobe Experience Cloud.

## Key benefits of Adobe Commerce as a Cloud Service

* **Automatic updates & maintenance** - Adobe manages core platform upgrades, patching, and security.
* **Enhanced performance & scalability** - Leverages Edge Delivery Services and a cloud-native architecture for superior speed and dynamic scaling.
* **Reduced TCO** - Eliminates the need for manual upgrades, patching, and significant infrastructure management.
* **AI-powered tools** - Integrates with Adobe Sensei for features like Live Search, Product Recommendations, and generative AI content creation.
* **Composable & headless capabilities** - Strong API-first design for flexible front-end development and integration.

## Understanding the shift - PaaS vs. SaaS

**Key differences**

* **PaaS (Current)**: Merchant manages application code, upgrades, patching, infrastructure configuration within Adobe's hosted environment. Shared responsibility model for services (MySQL, Elasticsearch, and others).
* **SaaS (New - [!DNL Adobe Commerce as a Cloud Service])**: Adobe fully manages the core application, infrastructure, and updates. Merchants focus on customization via extensibility points (APIs, App Builder, UI SDKs). Core application code is locked.

**Architectural implications**

* **Versionless platform**: Continuous updates mean no more major version upgrades for the core.
* **Microservices & API-first**: Deeper reliance on APIs for extensibility and integration.
* **Headless by default (optional)**: Strong support for decoupled storefronts (e.g., PWA Studio).
* **Edge Delivery Services**: Impact on front-end performance and deployment.

**New tooling & concepts**
* [Adobe App Builder](https://developer.adobe.com/app-builder/) and [API Mesh](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/)
* Self-service provisioning via [Cloud Manager](./getting-started.md#create-an-instance)

## Migration paths

[!DNL Adobe Commerce as a Cloud Service] supports multiple migration paths, depending on your timeline, storefront, and customizations.

As an alternative to a full migration, [!DNL Adobe Commerce as a Cloud Service] supports a phased migration, using Commerce Optimizer or an incremental approach.

* **Incremental migration**—This approach involves migrating your data, customizations, and integrations in stages. This approach is ideal for large merchants with many customizations who want to gradually transition their complex customizations and data to [!DNL Adobe Commerce as a Cloud Service] at their own pace.

![incremental migration](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—This approach allows you to migrate iteratively, by using Commerce Optimizer as a transitional phase to move complex customizations and data to [!DNL Adobe Commerce as a Cloud Service] at your own pace. Commerce Optimizer provides access to Merchandising Services powered by Catalog Channels and Policies, Commerce Storefront powered by Edge Delivery, and Product Visuals powered by AEM Assets.

![iterative migration](./assets/optimizer.png){width="600" zoomable="yes"}

* **Full migration**—This approach involves migrating all data, customizations, and integrations at once. This approach is ideal for smaller merchants with few customizations who want to quickly transition to [!DNL Adobe Commerce as a Cloud Service].

The following table provides an overview of the migration process for different storefronts and configurations:

|                    | LUMA Storefront                        | PWA Storefront                         | Commerce Storefront powered by Edge Delivery               | Headless                               |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Data migration     | Required                               | Required                               | Required                               | Required                               |
| Storefront         | Migrate to Commerce Storefront powered by Edge Delivery                         | Migrate to Commerce Storefront powered by Edge Delivery or maintain             | No impact                              | No impact                              |
| API Mesh           | Build new mesh                         | Build new mesh or reconfigure existing | Build new mesh or reconfigure existing | Build new mesh or reconfigure existing |
| Integrations       | Leverage integration starter kit       | Leverage integration starter kit       | Leverage integration starter kit       | Leverage integration starter kit       |
| Customizations     | Move to App Builder & API Mesh         | Move to App Builder & API Mesh         | Move to App Builder & API Mesh         | Move to App Builder & API Mesh         |
| Assets Management  | Migration required if using OOTB       | Migration required if using OOTB       | Migration required if using OOTB       | Migration required if using OOTB       |
| Extensions         | Migrate to App Builder                 | Migrate to App Builder                 | Migrate to App Builder                 | Migrate to App Builder                 |

As indicated by the table, the mitigations for each migration will consist of:

* **Data migration**—Using provided migration tooling to migrate data from your existing instance to [!DNL Adobe Commerce as a Cloud Service].
* **Storefront**—Existing EDS and headless storefronts do not require mitigation, but LUMA storefronts require migrating to Commerce Storefront powered by Edge Delivery. PWA Studio storefronts can be migrated to Commerce Storefront powered by Edge Delivery or maintained in their current state. Adobe will provide accelerators to assist with storefront migration.
* **[API Mesh](https://developer.adobe.com/graphql-mesh-gateway)**—Create a new mesh or modify the existing one. Adobe will provide preconfigured meshes to assist with this process.
* **Integrations**—All integrations need to leverage either the [integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) or the [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/).
* **Customizations**—All customizations must move to App Builder and API Mesh.
* **Assets Management**—All assets management requires migration. If you are already using AEM Assets, there is no need to migrate.
* **Extensions**—Any in-process extensions need to be recreated as out-of-process extensions. By the end of 2025, Adobe will provide access to our most popular extensions to minimize build times.

## Migration phases

The following phases describe the necessary steps and considerations for migrating to [!DNL Adobe Commerce as a Cloud Service].

### Pre-migration assessment and planning

This phase is critical for minimizing risks and establishing a clear migration path and identifying issues before they arise.

**Discovery and audit of current environment:**

**Codebase analysis:**

  * Identify all custom modules, themes, and overrides.
  * Analyze core code modifications and determine which will need refactoring as part of migration.
  * Assess third-party extensions and determine compatibility with [!DNL Adobe Commerce as a Cloud Service], are there SaaS-compatible alternatives, or do you need to create custom API integrations.
  * Identify any deprecated code or functionality.

**Data audit:**

  * Assess your database size and complexity.
  * Identify unused data or tables for cleanup.
  * Review existing data import/export processes.

**Integrations review:**

  * List all external systems integrated with Adobe Commerce (ERP, CRM, PIM, payment gateways, shipping providers, OMS, and any other systems).
  * Assess integration methods (API, custom scripts, and other methods).
  * Evaluate compatibility with [!DNL Adobe Commerce as a Cloud Service]'s API-first approach and App Builder.

**Performance benchmarking:**

  * Document current Lighthouse scores, page load times, and key performance indicators (KPIs).
    * This provides a baseline to measure post-migration improvements.

**Security configuration review:**

  * Assess any custom WAF rules, IP whitelists, and any other security configurations.

**Defining migration scope and strategy:**

* **Phased vs. all-at-once migration:** Discuss the pros and cons of each approach.
* **Identify core business processes:** Prioritize functionalities that must be migrated first.
* **Headless vs. monolithic storefront:** Decision point for new storefront development or adapting existing storefronts.
* **Integration strategy:** Determine how existing integrations will be re-platformed (API Mesh, App Builder, direct API).
* **Data migration strategy:** Determine if you intend to migrate using full historical data, partial data, or no migrated data.

**Team readiness & training:**

* Familiarization yourself with [!DNL Adobe Commerce as a Cloud Service] concepts, development workflows, and new tools.
* Attend hands-on training with Adobe App Builder, Edge Delivery Services, and [!DNL Adobe Commerce as a Cloud Service] deployment pipelines.

**Environment setup & provisioning:**

* Provision your [!DNL Adobe Commerce as a Cloud Service] sandbox and development environments with Adobe Cloud Manager.
* Familiarize yourself with the new environment variables and configuration management.

### Incremental migration phase

The following steps outline the development and execution process of the migration using an incremental approach:

#### Phase 1 - foundational migration and storefront POC

**Code refactoring & customization strategy:**

* **Identify and remove core overrides:** Prioritize removing or re-implementing any direct core Adobe Commerce code modifications. These are mostly incompatible with [!DNL Adobe Commerce as a Cloud Service]'s locked core.
* **Refactor custom modules:** Adapt custom modules to adhere to [!DNL Adobe Commerce as a Cloud Service] extensibility patterns (service contracts, plugins, events).
* **Analyze third-party extensions:** Replace with [!DNL Adobe Commerce as a Cloud Service] compatible versions or custom integrations with App Builder.
* **Implement new [!DNL Adobe Commerce as a Cloud Service] storefront front-end components:** (optional, but recommended)
  * Start with Commerce Storefront powered by Edge Delivery Services or custom headless storefront.
  * Connect to [!DNL Adobe Commerce as a Cloud Service] using GraphQL APIs.
  * Develop basic product display, category listing, and non-transactional functionality.

**Data migration preparation:**

* Clean and optimize existing data.
* Identify critical data sets for initial migration (such as products and categories).
* Familiarize yourself with Adobe's recommended data migration tools.

**Basic [!DNL Adobe Commerce as a Cloud Service] environment setup:**

* Configure core [!DNL Adobe Commerce as a Cloud Service] settings (such as store views and basic locales).
* Establish continuous integration/continuous deployment (CI/CD) pipelines with Cloud Manager.

#### Phase 2 - core Commerce functionality and integrations

**Product and catalog migration:**

* Migrate product data (attributes, images, inventory) to [!DNL Adobe Commerce as a Cloud Service].
* Leverage new catalog management features.
* Integrate with existing PIM systems (if applicable) using App Builder or API Mesh.

**Customer and order data migration:**

* Migrate existing customer accounts and order history (consider the volume and business necessity).
* Ensure customer password compatibility (or plan for password reset on first login).

**Payment and shipping integrations:**

* Re-integrate existing payment gateways and shipping providers.
* Leverage Adobe's Payment Services where applicable.
* Implement custom integrations using App Builder, if needed.

**Search and merchandising:**

* Integrate with Adobe Commerce's Live Search and Product Recommendations (powered by AdobeSensei).
* Configure merchandising rules and dynamic categories.

**Basic B2B functionality (if applicable):**

* Migrate company accounts, shared catalogs, and pricing rules.
* Configure quote management and purchase approvals.

**Performance optimization:**

* Leverage Edge Delivery Services for front-end optimization.
* Monitor performance metrics in the [!DNL Adobe Commerce as a Cloud Service] environment.

#### Phase 3 - Advanced features and optimization

**Content management (CMS integration):**

* Leverage AEM Sites integration for rich content experiences (headless or hybrid).

**Remaining integrations:**

* Migrate any remaining third-party integrations (ERP, CRM, OMS, and others) using App Builder and API Mesh.
* Develop custom APIs or webhooks as needed.

**User acceptance testing (UAT) and performance testing:**

* Thoroughly test all functionalities, user flows, and integrations.
* Stress test to ensure [!DNL Adobe Commerce as a Cloud Service] can handle peak loads.

### Post-migration and ongoing operations

**DNS cutover & go-live:**

* Carefully plan the DNS cutover with minimal downtime.
* Monitor site health and performance immediately post-launch.

**Post-launch operations:**

**Decommissioning PaaS environment:**

* Securely archive or delete old PaaS instances and data after the validation period.

**Ongoing development workflow:**

* Embrace the versionless nature of [!DNL Adobe Commerce as a Cloud Service], which has continuous small deployments rather than large upgrades.
* Utilize Cloud Manager for managing environments and deployments.
* Leverage App Builder for extending functionality without impacting the core.

**Monitoring, performance and security:**

* Continuously monitor site performance, errors, and security logs.
* Utilize Adobe's built-in security features and adhere to best practices.

**Training and documentation:**

* Train new developers and business users on the [!DNL Adobe Commerce as a Cloud Service] platform and workflows.
* Maintain up-to-date internal documentation for custom integrations and processes.
