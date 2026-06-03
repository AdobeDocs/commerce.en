---
title: Catalog Events and Adobe I/O Integration Guide
description: Learn how to enable catalog events in the Commerce Catalog Service. Discover event types, [!DNL Adobe I/O Events] delivery, and end-to-end setup.
recommendations: noCatalog
role: Admin, Developer
feature: Services, Catalog Service
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Catalog events and Adobe I/O integration guide

Catalog events are machine-generated notifications that describe changes in catalog data stored by [!DNL Catalog Service]. They enable event-driven workflows such as:

* Keeping external caches or services in sync with catalog updates.
* Triggering downstream processes when products, variants, prices, or categories change.
* Powering Experience Edge and [!DNL Edge Delivery Services] use cases that require near real-time catalog updates.

For the end-to-end path from [!DNL Adobe Commerce] to your event consumers, see [Event delivery through Adobe I/O Events](#event-delivery-through-adobe-io-events).

## Supported event types

The Catalog events service focuses on storefront-relevant changes. Typical event categories include [product](#product-events), [variant and options](#variant-and-options-events), [category](#category-events), and [price and availability changes](#price-and-availability-events).

Each event includes:

* An *event type*, for example, `catalog.product.updated`, following Adobe I/O naming conventions.
* *Identity information* such as SKU or internal ID, and website/store context.
* A *payload* that describes what changed, aligned with [!DNL Catalog Service] product and category API models.

### Product events {#product-events}

* Product created
* Product updated (attributes, media, custom attributes)
* Product lifecycle changes (enabled/disabled, visibility changes)

### Variant and options events {#variant-and-options-events}

* Variant created or removed
* Option attribute changes for complex products (for example, configurables)

### Category events {#category-events}

* Category created
* Category updated
* Category deleted
* Changes to category–product assignments

### Price and availability events {#price-and-availability-events}

* Price changes that impact storefront behavior
* Selected availability changes that are surfaced through [!DNL Catalog Service]

## Event delivery through Adobe I/O Events {#event-delivery-through-adobe-io-events}

[!DNL Adobe I/O Events] delivers catalog events to your integrations. The following diagram shows how catalog changes flow from [!DNL Adobe Commerce] through [!DNL Catalog Service] and the Storefront Eventing Service to subscribed consumers:

![Catalog event pipeline from Adobe Commerce through Catalog Service to Adobe I/O Events consumers](assets/catalog-service-event-pipeline.png)

The diagram organizes the pipeline into Commerce, Catalog Service, and Delivery layers. The following steps explain each handoff in more detail:

1. **Adobe Commerce → Catalog Service**

   [!DNL Adobe Commerce] exports catalog data to [!DNL Catalog Service] using the supported SaaS Data Export extensions.

1. **Catalog Service → Storefront Eventing Service**

   * The Storefront Eventing Service listens to [!DNL MongoDB] collections using *change streams*.
   * It converts raw changes into standardized catalog events and applies filtering and normalization.

1. **Storefront Eventing Service → Adobe I/O Events**

   * Normalized events are published into [!DNL Adobe I/O Events].
   * Consumers subscribe using webhooks, [!DNL Adobe I/O Runtime] actions, or other supported mechanisms.

[!DNL Adobe I/O Events] provides:

* *At-least-once delivery* per subscriber (duplicate events are possible).
* *Best-effort ordering* per logical key (such as product), but no strict global ordering guarantees.

Your consumers must handle duplicate events and out-of-order delivery. See [Idempotency](#idempotency) for implementation guidance.

## Use cases

You can use Catalog events in multiple scenarios.

### Static site and Edge Delivery

* Regenerate or invalidate specific product or category pages when catalog data changes.
* Avoid frequent polling of [!DNL Catalog Service] APIs.

### Search indexing and caching

* Trigger incremental updates in downstream search indexes.
* Update cache layers or external views of the catalog when product or category data changes.

### Integration with external systems

* Forward catalog changes to external systems such as PIM, pricing engines, or other line-of-business systems.
* Keep downstream applications synchronized without direct database access.

### Monitoring and observability

Combine Catalog events with existing monitoring (for example, Grafana and Prometheus) to:

* Monitor event throughput.
* Detect anomalies in catalog update volume.

## Enable catalog events

>[!PREREQUISITES]
>
>Before you enable catalog events, ensure that you have the following:
>
>* An Adobe [!DNL Commerce] 2.4.4+ instance with [!DNL Catalog Service], [!DNL Live Search], or [!DNL Product Recommendations] installed. See [Onboarding and Installation](installation.md). If you are enabling events for [!DNL Adobe Commerce as a Cloud Service], these services are already installed.
>* Access to the Adobe Developer Console with permission to enable [!DNL Adobe I/O Events] and subscribe to the Catalog events provider for your [!DNL IMS] organization.
>* To verify sync to Commerce SaaS services on the [!UICONTROL Data Management Dashboard], Product Recommendations v6.0, [!DNL Live Search] v4.1.0+, or [!DNL Catalog Service] v1.17+ are required. Adobe recommends updating your Commerce project to the latest supported versions of these services. Earlier service versions, use [Catalog Sync](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) for sync verification.

Follow these steps to enable catalog events end to end.

1. Verify that [!DNL Catalog Service] has current catalog data from your [!DNL Commerce] instance before you configure [!DNL Adobe I/O Events]. Catalog events depend on [!DNL SaaS Data Export] completing two stages—confirm **both**:

   * **Feed export from Commerce**—Confirm that catalog feeds exported successfully from [!DNL Commerce] using the CLI or the Commerce Admin.

     * **CLI**—Use the `saas:resync` command to sync each [!DNL Catalog Service] feed and confirm successful completion in `var/log/saas-export.log`:

       ```shell
       bin/magento saas:resync --feed productattributes
       bin/magento saas:resync --feed products
       bin/magento saas:resync --feed scopesCustomerGroup
       bin/magento saas:resync --feed scopesWebsite
       bin/magento saas:resync --feed prices
       bin/magento saas:resync --feed productoverrides
       bin/magento saas:resync --feed variants
       bin/magento saas:resync --feed categories
       bin/magento saas:resync --feed categoryPermissions
       ```

       Adobe does not recommend using `saas:resync` regularly except for initial sync or troubleshooting. For additional options, see [SaaS Data Export CLI commands](../data-export/data-export-cli-commands.md) and [Logging and troubleshooting](../data-export/troubleshooting-logging.md).

     * **Commerce Admin**—Open the [Data Feed Sync Status](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) page (**[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**) and confirm that the last export status is successful for each [!DNL Catalog Service] feed.

   * **Sync to connected Commerce SaaS services**—Confirm that the exported data synced successfully to [!DNL Catalog Service] and other connected Commerce SaaS services.

     * **CLI**—When you run `saas:resync`, review `var/log/saas-export.log` and confirm that feed operations report items as `synced` to Commerce SaaS services without errors.

     * **Commerce Admin**—When your storefront services meet the version requirements in the prerequisites, open the [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) (**[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Management Dashboard]**) and confirm successful synchronization for [!DNL Catalog Service] feeds.

   For more about the export and synchronization process, see [Synchronize data with SaaS Data Export](../data-export/data-synchronization.md).

1. Configure [!DNL Adobe I/O Events].

   Work with your Adobe administrator to complete these tasks:

   * Enable [!DNL Adobe I/O Events] for your [!DNL IMS] organization.
   * Subscribe to the *Catalog events provider* for your [!DNL Commerce] environment.

   Configure a consumer, such as:

   * A webhook endpoint
   * An [!DNL Adobe I/O Runtime] action
   * Another supported destination

   For instructions to complete the steps yourself, see [Configure the I/O connection](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection) in the *Adobe Commerce Developer* documentation.

1. Validate the event flow.

   * Make a simple catalog change, such as updating a product name or changing the enabled or disabled status.

   * Confirm the following outcomes:

     * The change is visible through [!DNL Catalog Service] APIs.
     * Your [!DNL Adobe I/O Events] consumer receives a corresponding event.

### Result

Catalog events are enabled for your environment. When catalog data changes in [!DNL Commerce], updates flow through [!DNL Catalog Service] to [!DNL Adobe I/O Events], and your subscribed consumer receives the corresponding catalog event. Review [Limits and best practices](#limits-and-best-practices) before you build production integrations.

## Limits and best practices {#limits-and-best-practices}

When building on Catalog events, follow these best practices.

### Idempotency {#idempotency}

[!DNL Adobe I/O Events] can deliver the same catalog event more than once, and events for a single product can arrive out of order. Design consumers to be idempotent by:

* Using entity IDs with a version or timestamp field.
* Safely ignoring duplicate notifications for the same change.

### Throughput and backpressure

Large catalogs with high update rates can generate significant event volume. Ensure that:

* Consumers can process events at peak throughput.
* You use buffering, batching, or queues where necessary.

### Security and isolation

* [!DNL Adobe I/O Events] enforces *tenant isolation*.
* Your organization receives events only for its own environments and entitlements.

### Schema evolution

Catalog event payloads follow the same conceptual model as [!DNL Catalog Service] APIs. To remain forward-compatible:

* Avoid strict schema enforcement where possible.
* Ignore unknown fields instead of failing.

## Troubleshoot catalog events

If catalog events are missing or delayed, work through these steps.

1. **Check Catalog Service data**

   [Use the [!DNL Catalog Service] API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/) to confirm that the catalog change is stored successfully.

2. **Verify [!DNL SaaS Data Export]**

   Catalog events require current data in [!DNL Catalog Service]. Confirm both stages of the export path:

   * **Feed export from Commerce** — On the [Data Feed Sync Status](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) page or in `var/log/saas-export.log`, confirm that [!DNL Catalog Service] feeds exported successfully from [!DNL Commerce].

   * **Sync to connected Commerce SaaS services** — On the [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard), [Catalog Sync](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync), or in export logs, confirm that data synced successfully to [!DNL Catalog Service].

   For troubleshooting export and sync jobs, see [Synchronize data with SaaS Data Export](../data-export/data-synchronization.md) and [Logging and troubleshooting](../data-export/troubleshooting-logging.md).

3. **Validate Adobe I/O Events configuration**

   Confirm that:

   * The Catalog events provider is enabled.
   * The subscription is active.
   * Your endpoint or action can receive and process other test events.

4. **Contact Adobe Support**

   When opening a support ticket, select the issue reason that corresponds to **Adobe Commerce application** and include the following information:

   * Catalog Service details (environment, region).
   * [!DNL Adobe I/O Events] subscription details.
   * Approximate time and description of missing events.

   For additional help, see [Support tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

>[!MORELIKETHIS]
>
>
>* [Onboarding and installation](installation.md)
>* [Get started with the Catalog Service](get-started.md)
>* [Synchronize data with SaaS Data Export](../data-export/data-synchronization.md)
>* [Retrieve catalog data with the GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/){target="_blank"}
>* [Catalog service and API Mesh](mesh.md)
>* [Configure the I/O connection](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection){target="_blank"}

