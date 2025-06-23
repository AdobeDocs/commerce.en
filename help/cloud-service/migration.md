---
title: 'Migrate to [!DNL Adobe Commerce as a Cloud Service]'
description: Learn how to migrate to [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Architect
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
* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) and [API Mesh for Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
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

### Incremental migration phases

**Strategic refactoring and externalization**

This phase consists of the core of the migration, focusing on adapting your codebase to the [!DNL Adobe Commerce as a Cloud Service] cloud-native paradigm. This involves strategically adopting new Adobe services and moving custom logic out of the core Commerce platform.

#### 1. Migrate "in-process" customizations and extensions to App Builder

This is a crucial phase for achieving a "locked core" and future-proofing your solution, central to the [!DNL Adobe Commerce as a Cloud Service] architectural philosophy.

* **Externalize complex logic to App Builder**: Analyze existing custom modules and third-party extensions within your PaaS codebase. For complex business logic, bespoke integrations, or microservices that do not require direct, in-process manipulation of the core Commerce data model, refactor and re-platform them as serverless applications within Adobe Developer App Builder.
* **Leverage API Mesh**: For scenarios requiring data from multiple backend systems (for example, your PaaS Commerce backend, ERP, CRM, and custom App Builder microservices), implement an API Mesh layer within App Builder. This consolidates disparate APIs into a single, performant GraphQL endpoint consumed by your new storefront or other services, simplifying complex data fetching.
* **Event-driven architecture**: Utilize Adobe I/O Events to trigger App Builder actions based on events occurring in your PaaS instance (for example, product updates, customer registrations, order status changes) or other connected systems. This promotes asynchronous communication, reduces tight coupling, and enhances system resilience.

**Benefit**: This step significantly reduces technical debt associated with deeply embedded customizations, dramatically improves upgradeability of your core Commerce instance, enhances the scalability and independent deployability of custom logic, and promotes faster development cycles for extensions.

#### 2. Adopt SaaS-based Adobe Commerce merchandising services and integrate catalog data

This is a critical initial integration point with two options regarding catalog data management:

**Option 1 (transitional) - Leverage existing Catalog SaaS service integrated with PaaS backend**

This option serves as a transitional step, building upon an existing integration where your PaaS backend populates an existing instance of the Adobe Commerce Catalog SaaS service.

* **Catalog data synchronization**: Ensure your Adobe Commerce PaaS instance continues to synchronize product and catalog data to your existing Adobe Commerce Catalog SaaS service. This typically relies on established connectors or modules within your PaaS instance. The Catalog SaaS service remains the authoritative source for search and merchandising functions, deriving its data from your PaaS backend.
* **API Mesh for optimization**: While the headless storefront (on EDS) and other services could directly consume data from the Catalog SaaS service, it is highly recommended to use API Mesh (within App Builder). API Mesh can unify APIs from the Catalog SaaS service with other necessary APIs from your PaaS backend (for example, real-time inventory checks from the transactional database or custom product attributes not fully replicated to the Catalog SaaS service) into a single, performant GraphQL endpoint. This also allows for centralized caching, authentication, and response transformation.
* **Integrate Live Search and Product Recommendations**: Configure Live Search and Product Recommendations SaaS services to ingest catalog data directly from your existing Adobe Commerce Catalog SaaS service, which in turn is populated by your PaaS backend.

**Benefit**: This provides a faster path to a headless storefront and advanced SaaS merchandising features by leveraging an existing and operational Catalog SaaS service and its integration pipeline with your PaaS backend. However, it retains the dependency on the PaaS backend for the primary catalog data source and does not provide the multi-source aggregation capabilities inherent in the new Composable Catalog Data Model. This option is a valid stepping-stone towards a fuller composable architecture.

**Option 2 - Adopt the new Composable Catalog Data Model (CCDM)**

This is the strategic, future-proof approach for leveraging Adobe Commerce Optimizer. CCDM provides a flexible, scalable, and unified catalog service designed for multi-source data aggregation and dynamic merchandising.

* **Data ingestion and unification**
  * Begin by ingesting product and catalog data from your existing Adobe Commerce PaaS instance (and/or other PIM/ERP systems) into the new Composable Catalog Data Model (CCDM).
  * Map existing product attributes to the CCDM's flexible schema. Prioritize critical product data for initial ingestion.
  * Establish robust data pipelines for continuous synchronization. This can involve:
    * **Event-driven** (through App Builder): Utilize Adobe I/O Events from your PaaS instance to trigger custom Adobe App Builder applications. These applications would transform and push data changes (create, update, and delete) to the CCDM through its APIs.
    * **Batch ingestion**: For large initial loads or periodic bulk updates, use secure file transfers (for example, CSV or JSON) to a staging area, processed by Adobe Experience Platform (AEP) ingestion services into CCDM.
    * **Direct API integration** (with App Builder orchestration): For more complex scenarios, App Builder can act as an orchestration layer, making direct API calls to your PaaS backend, transforming the data, and pushing it to CCDM.
* **Channel and policy definition**: Configure channels (logical groupings for unique catalog presentation, such as store views, regions, and B2B/B2C segments) and define policies (rule sets for product presentation, filtering, and merchandising) within the CCDM. This enables dynamic control over product assortments and display logic per channel.
* **Integrate Live Search and Product Recommendations**: Once catalog data is present in CCDM, integrate Adobe's SaaS-based Live Search and Product Recommendations services. These leverage Adobe Sensei AI and machine learning models for superior search relevance and personalized recommendations, consuming data directly from the CCDM.

**Benefit**: By abstracting catalog management and discovery into CCDM and associated SaaS services, you achieve improved performance, gain AI-driven merchandising capabilities, significantly offload read operations from your legacy backend, and enable a robust "peel-off" of the top-of-funnel experience.

#### 3. Build out your storefront on Edge Delivery Services (EDS)

With merchandising data pipelines established and customizations externalized, the focus shifts to building your high-performance frontend.

* **Initial setup**: Set up your project using the Adobe Commerce Storefront boilerplate for EDS. This provides a foundational headless frontend built on modern web technologies.
* **Connect to catalog services and API Mesh**: Your EDS storefront will consume data primarily through GraphQL APIs:
  * **Option 1**: From the existing Catalog SaaS service (through API Mesh) for product information and merchandising rules.
  * **Option 2**: From CCDM for product information and merchandising rules.
  * From API Mesh for any orchestrated data from your legacy backend (PaaS instance) or custom App Builder services (for example, real-time inventory, custom product attributes, and loyalty points display).
* **Content migration (AEM Services)**: Migrate your existing static content (for example, "About Us" pages, blog posts, and marketing banners) into AEM Services, which powers the EDS storefront. Leverage AEM's content authoring capabilities and ensure assets are optimized for EDS delivery.
* **Develop core UI components**: Build out critical user interface components for product display pages (PDPs), category listing pages (CLPs), and general content pages using EDS drop-in components and custom React/Vue components. Prioritize core commerce flows.
* **Integration with existing cart/checkout**: Initially, the EDS storefront will orchestrate a handoff to your existing Adobe Commerce PaaS (or other third-party platform) for cart management and checkout. This typically involves:
  * **Redirection**: Redirecting the user to the legacy platform's native cart and checkout URLs, passing necessary session and cart identifiers.
  * **Direct API interaction** (with App Builder orchestration): Building custom cart and checkout UI components within EDS that interact directly with your PaaS backend's cart and checkout APIs. This often involves App Builder as a Backend-for-Frontend (BFF) to orchestrate calls to multiple backend services (for example, PaaS cart, payment gateways, and shipping calculators).

**Benefit**: Delivers a blazing-fast, SEO-optimized, and highly flexible storefront experience. This phase directly contributes to a superior customer experience and lays the groundwork for future frontend innovation.

#### 4. Data migration (phased process)

Data migration is a critical and multi-faceted process that runs concurrently with refactoring and storefront development, ensuring data consistency and integrity.

* **Clean and optimize existing data**: Prior to any large-scale migration, perform comprehensive data cleansing, de-duplication, and validation on your existing PaaS database. This proactive step is crucial to minimize the transfer of legacy data issues and ensure the quality of data in the new environment.

**Bulk data migrations**

Bulk data migration involves taking a full data dump from your Adobe Commerce PaaS instance, transforming that entire dataset, and importing it into Adobe Commerce as a Cloud Service all at one time. This method is typically used for the initial population of data.

* **Tooling availability**: Dedicated tooling for customer use for first-party Commerce bulk data migrations will be available by request in mid-July 2025. If customers require assistance with bulk data migration beforehand, Adobe can facilitate the data transfer on their behalf by request.

* **Process**:
  * **Full data export**: Extract a complete dataset from your Adobe Commerce PaaS instance (for example, products, categories, customer accounts, historical order data, static blocks, and page content).
  * **Data transformation**: Apply necessary transformations to align the extracted data with the schema requirements of the new Adobe Commerce as a Cloud Service components, including the Composable Catalog Data Model (CCDM) if adopted, and any other relevant Adobe services or databases. This may involve custom scripts or specialized data mapping tools.
  * **Initial import**: Import the transformed full dataset into the respective components of Adobe Commerce as a Cloud Service. For product and category data, this populates the chosen catalog service (CCDM or existing Catalog SaaS). For customer and order data, this populates the transactional backend or associated services.
  * **Validation**: Rigorously validate the imported data to ensure completeness, accuracy, and consistency across all new systems.

**Iterative data migrations**

Iterative data migrations focus on synchronizing incremental changes and deltas from the source PaaS instance to the new Cloud Service components, ensuring data freshness leading up to and after cutover.

* **Tooling availability**: Tooling specifically designed for iterative data migrations will be available in the second half of 2025.

* **Process**:
  * **Delta identification**: Establish mechanisms to identify changes (creations, updates, and deletions) in critical data sets on your PaaS environment since the last sync. This can involve change data capture (CDC), timestamp comparisons, or event-based triggers.
  * **Continuous synchronization**: Implement robust mechanisms for continuous, incremental data synchronization from your PaaS environment to the new Cloud Service components (for example, CCDM and transactional backend). This is crucial for maintaining data freshness and minimizing downtime during cutover.
  * **Leveraging events**: Utilize Adobe I/O Events where possible to trigger App Builder actions for real-time or near real-time updates from your PaaS instance to the new services. For example, a product update in PaaS could trigger an event that updates the corresponding entry in CCDM.
  * **API-driven updates**: For data that is not event-driven, use scheduled API calls (through App Builder or other integration platforms) to pull changes from PaaS and push them to the new systems.
  * **Error handling and monitoring**: Implement robust error handling, logging, and monitoring for all iterative data pipelines to ensure data integrity is maintained throughout the process.

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
