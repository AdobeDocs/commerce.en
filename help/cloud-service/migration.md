---
title: 'Migrate to [!DNL Adobe Commerce as a Cloud Service]'
description: Learn how to migrate to [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
---
# Migrate to [!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] provides most configuration out of the box. However, if you are migrating from an existing Adobe Commerce on Cloud or on-premises instance, you will need to perform different migration actions depending on your specific configuration.

## Migration paths

[!DNL Adobe Commerce as a Cloud Service] supports multiple migration paths, depending on your timeline, storefront, and customizations.

As an alternative to a full migration, [!DNL Adobe Commerce as a Cloud Service] supports a phased migration, using Commerce Optimizer or an incremental approach.

* **Incremental Migration**—This approach involves migrating your data, customizations, and integrations in stages. This approach is ideal for large merchants with many customizations who want to gradually transition their complex customizations and data to [!DNL Adobe Commerce as a Cloud Service] at their own pace.

![incremental migration](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—This approach allows you to migrate iteratively, by using Commerce Optimizer as a transitional phase to move complex customizations and data to [!DNL Adobe Commerce as a Cloud Service] at your own pace. Commerce Optimizer provides access to Merchandising Services powered by Catalog Channels and Policies, Commerce Storefront powered by Edge Delivery, and Product Visuals powered by AEM Assets.

![iterative migration](./assets/optimizer.png){width="600" zoomable="yes"}

* **Full Migration**—This approach involves migrating all data, customizations, and integrations at once. This approach is ideal for smaller merchants with few customizations who want to quickly transition to [!DNL Adobe Commerce as a Cloud Service].

The following table provides an overview of the migration process for different storefronts and configurations:

|                    | LUMA Storefront                        | PWA Storefront                         | Commerce Storefront powered by Edge Delivery               | Headless                               |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Data Migration     | Required                               | Required                               | Required                               | Required                               |
| Storefront         | Migrate to Commerce Storefront powered by Edge Delivery                         | Migrate to Commerce Storefront powered by Edge Delivery or Maintain             | No Impact                              | No Impact                              |
| API Mesh           | Build New Mesh                         | Build New Mesh or reconfigure existing | Build New Mesh or reconfigure existing | Build New Mesh or reconfigure existing |
| Integrations       | Leverage integration starter Kit       | Leverage integration starter Kit       | Leverage integration starter Kit       | Leverage integration starter Kit       |
| Customizations     | Move to App Builder & API Mesh         | Move to App Builder & API Mesh         | Move to App Builder & API Mesh         | Move to App Builder & API Mesh         |
| Assets Management  | Migration Required if using OOTB       | Migration Required if using OOTB       | Migration Required if using OOTB       | Migration Required if using OOTB       |
| Extensions         | Migrate to App Builder                 | Migrate to App Builder                 | Migrate to App Builder                 | Migrate to App Builder                 |

As indicated by the table, the mitigations for each migration will consist of:

* **Data Migration**—Using provided migration tooling to migrate data from your existing instance to [!DNL Adobe Commerce as a Cloud Service].
* **Storefront**—Existing EDS and headless storefronts do not require mitigation, but LUMA storefronts require migrating to Commerce Storefront powered by Edge Delivery. PWA Studio storefronts can be migrated to Commerce Storefront powered by Edge Delivery or maintained in their current state. Adobe will provide accelerators to assist with storefront migration.
* **[API Mesh](https://developer.adobe.com/graphql-mesh-gateway)**—Create a new mesh or modify the existing one. Adobe will provide preconfigured meshes to assist with this process.
* **Integrations**—All integrations need to leverage either the [integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) or the [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/).
* **Customizations**—All customizations must move to App Builder and API Mesh.
* **Assets Management**—All assets management requires migration. If you are already using AEM Assets, there is no need to migrate.
* **Extensions**—Any in-process extensions need to be recreated as out-of-process extensions. By the end of 2025, Adobe will provide access to our most popular extensions to minimize build times.

## Migration phases

Migrating from your current Adobe Commerce instance to a new [!DNL Adobe Commerce as a Cloud Service] instance primarily involves the following phases:

* **[Readiness](#readiness-phase)**—Begin by determining if your deployment is ready to be moved to ACCS. In this phase, you should also familiarize yourself with the changes that ACCS has introduced.​
* **[Implementation](#implementation-phase)**—Next, ready your code, storefront, extensions, and integrations for migration. To ease the transition, Adobe allows for both [short-term and long-term iterative approaches](#migration-paths).​
* **[Go-Live](#go-live-phase)**—Test and confirm everything is in place, then perform the data migration.
* **[Post Go-Live](#post-go-live-phase)**—In collaboration with Adobe, monitor for issues and improve performance as needed after the migration is complete.

### Readiness phase

1. Start by reviewing the [!DNL Adobe Commerce as a Cloud Service] architecture, extensibility framework, and storefront capabilities:

    * [Adobe Commerce on Cloud Services Architecture](./overview.md)—Review the platform architecture and how it differs from your current Adobe Commerce instance.
    * [Adobe Commerce Extensibility Framework](https://developer.adobe.com/commerce/extensibility/)—Identify how you want to transition your current customizations.
    * [Commerce Storefront powered by Edge Delivery](https://experienceleague.adobe.com/developer/commerce/storefront/)—Review the recommended storefront solution.

1. Audit your customization compatibility:

    * Identify your current custom modules and third-party integrations.
    * Evaluate customizations that need reimplementation using App Builder.
    * Map your current customizations to their App Builder extensions equivalents.

1. Confirm your storefront requirements and ensure they align with Adobe Edge Delivery capabilities.

1. Review your current third-party integrations and confirm API compatibility with the [!DNL Adobe Commerce as a Cloud Service] platform.

### Implementation phase

The following steps outline the development and execution process of the migration:

1. Create a new [!DNL Adobe Commerce as a Cloud Service] instance in the [Commerce Cloud Manager](./getting-started.md#create-an-instance).

1. Install required apps and customizations. [!DNL Adobe Commerce as a Cloud Service] has access to our most popular apps. If you need additional apps or customizations, you can reimplement them using App Builder.

1. Set up one of the following GraphQL-based storefronts:

   * [Create a Commerce storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)
   * [Use PWA Studio to create a custom GraphQL-based storefront](https://developer.adobe.com/commerce/pwa-studio/)

1. Migrate your data from your previous Commerce instance to ACCS:

    * Migrate native Adobe Commerce data using data migration tooling.
    * Migrate third-party extensions and customizations
    * Migrate configuration and integration data:
      * Transfer API Mesh configurations, third-party services, and system integrations using the [Adobe Commerce Integration Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/).

### Go-Live phase

Before launching, validate and test your new [!DNL Adobe Commerce as a Cloud Service] instance using a sandbox environment:

* **Functional Testing**—Ensure migrated data, storefront functionality, and customizations work seamlessly.

* **Performance Testing**—Evaluate the speed and scalability of your stores to ensure optimal performance globally.

* **Security Audit**—Review security measures, including API access control and any potential vulnerabilities.

Once you have validated and tested your new [!DNL Adobe Commerce as a Cloud Service] sandbox instance, you can launch your production instance.

### Post Go-Live phase

After Go Live, perform these post-launch activities:

1. Go live followup

    * Redirect traffic to the new platform and monitor performance.
    * Disable your old Adobe Commerce instance.

1. Post-launch Monitoring

    * Use monitoring tools to ensure stable operations and address any post-launch issues.
