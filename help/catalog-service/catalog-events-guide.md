---
title: Catalog Events and Adobe I/O Integration Guide
description: Learn how to enable catalog events in Adobe Commerce Catalog Service. Discover event types, [!DNL Adobe I/O Events] delivery, and validate end-to-end setup for consumers.
level: Intermediate
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

For the end-to-end path from [!DNL Adobe Commerce] to your event consumers, see [Event delivery through [!DNL Adobe I/O Events]](#event-delivery-through-adobe-io-events).

## Supported event types {#supported-event-types}

The Catalog events service focuses on storefront-relevant changes. The following table summarizes supported event categories and examples.

| Category | Events |
| --- | --- |
| Product | <ul><li>Product created</li><li>Product updated (attributes, media, custom attributes)</li><li>Product lifecycle changes (enabled/disabled, visibility changes)</li></ul> |
| Variant and options | <ul><li>Variant created or removed</li><li>Option attribute changes for complex products (for example, configurables)</li></ul> |
| Category | <ul><li>Category created</li><li>Category updated</li><li>Category deleted</li><li>Changes to category–product assignments</li></ul> |
| Price and availability | <ul><li>Price changes that impact storefront behavior</li><li>Selected availability changes that are surfaced through [!DNL Catalog Service]</li></ul> |

Each event includes:

* An *event type*, for example, `catalog.product.updated`, following [!DNL Adobe I/O] naming conventions.
* *Identity information* such as SKU or internal ID, and website/store context.
* A *payload* that describes what changed, aligned with [!DNL Catalog Service] product and category API models.

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

## Use cases {#use-cases}

You can use Catalog events in multiple scenarios.

### Static site and edge delivery

* Regenerate or invalidate specific product or category pages when catalog data changes.
* Avoid frequent polling of [!DNL Catalog Service] APIs.

### Search indexing and caching

* Trigger incremental updates in downstream search indexes.
* Update cache layers or external views of the catalog when product or category data changes.

### Integration with external systems

* Forward catalog changes to external systems such as PIM, pricing engines, or other line-of-business systems.
* Keep downstream applications synchronized without direct database access.

### Monitoring and observability

Combine Catalog events with existing monitoring (for example, [!DNL Grafana] and [!DNL Prometheus]) to:

* Monitor event throughput.
* Detect anomalies in catalog update volume.

## Enable catalog events {#enable-catalog-events}

Follow these steps to enable catalog events end to end.

>[!PREREQUISITES]
>
>Before you enable catalog events, ensure that you have the following:
>
>* An Adobe Commerce on cloud infrastructure or Adobe Commerce on premises 2.4.4+ project with [!DNL Catalog Service] enabled, or an Adobe Commerce as a Cloud Service instance with [!DNL Catalog Service] enabled.
>* [The [!DNL Adobe I/O] connection is configured for Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/configure-commerce).
>* [!DNL Adobe Developer Console] access—Developer permissions in the IMS organization where the Commerce instance is provisioned.
>* To verify sync to Commerce SaaS services, use the **[!UICONTROL Data Management Dashboard]** in the Admin.
>* Product Recommendations v6.0, [!DNL Live Search] v4.1.0+, or [!DNL Catalog Service] v1.17+ is required for dashboard verification. Adobe recommends updating your Commerce project to the latest supported versions of these services. For earlier service versions, use [Catalog Sync](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) for sync verification.

### Verify catalog data {#verify-catalog-data}

Verify that [!DNL Catalog Service] has current catalog data from your [!DNL Commerce] instance before you configure. Catalog events depend on [!DNL SaaS Data Export] completing two stages—confirm **both**:

1. Confirm successful **feed export from Commerce**.

   From the [!DNL Adobe Commerce] Admin, open the [Data Feed Sync Status](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) page (**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**) and confirm that the last export status is successful for each [!DNL Catalog Service] feed.

1. Confirm successful **sync to connected Commerce services** from the [!DNL Adobe Commerce] Admin.

   From the [!DNL Adobe Commerce] Admin, open the [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) (**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**) and verify that the synced products data includes the expected products.

### Register and subscribe to [!DNL Adobe I/O Events] {#register-events}

Define which Commerce events to subscribe to, then register them in the project.

If your instance is not in the selection list, then it is not connected to [!DNL Adobe I/O]. For instructions to fix the issue, see [Configure the [!DNL Adobe I/O] connection](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection) in the *Adobe Commerce Developer* documentation.

1. From the [!DNL Adobe Developer Console], sign in to the same IMS organization used for the Commerce project.

1. Create a project for Commerce Catalog Events, or add the events API to an existing project.

   * Select **[!UICONTROL APIs and services]** in the top navigation.

   * On the **[!UICONTROL Browse APIs and services]** page, select the **[!UICONTROL Events]** tab.

   * Quickly find Commerce Catalog Events APIs. Type _Catalog_ in the search box, or filter by the **[!UICONTROL Commerce]** product.

   * On the **[!UICONTROL Commerce Catalog Events]** card, select **[!UICONTROL Project]**.

   ![Commerce Catalog Events provider selected on the Browse APIs and services page](assets/catalog-event-select-provider.png){width="600" zoomable="yes"}

1. Configure event registration.

   Select the Commerce instance to receive event notifications from. Then, select **[!UICONTROL Next]**.

   ![Commerce instance selected on the event registration screen](assets/catalog-event-registration.png){width="600" zoomable="yes"}

1. Choose the events to subscribe to.

   Select all events or select by category (for example, Price or Product). Then, select **[!UICONTROL Next]**.

   ![Event categories selected for subscription on the registration screen](assets/catalog-event-subscription.png){width="600" zoomable="yes"}

1. Add OAuth server-to-server credentials.

   Enter a **[!UICONTROL Credential name]**. Then, select **[!UICONTROL Next]**.

1. Enter an **[!UICONTROL Event registration name]** and an **[!UICONTROL Event registration description]**. Then, select **[!UICONTROL Next]**.

1. On the final registration screen, accept the default consumer, the Journaling API.

   The default Journaling API consumer lets you test event registration and confirm that events are delivered. If you already configured a webhook or [!DNL Adobe I/O Runtime] action consumer, select it here. Otherwise, edit the event registration later when your consumer is ready.

   ![Journaling API consumer default selected on the event registration completion screen](assets/catalog-event-consumer.png){width="600" zoomable="yes"}

1. Select **[!UICONTROL Complete registration]**.

### Configure event consumer {#configure-consumer}

1. Configure a consumer, such as:

   * A webhook endpoint
   * An [!DNL Adobe I/O Runtime] action
   * Another supported destination

1. Edit the event registration to add the consumer details if you did not select a consumer during registration.

   * From the [!DNL Adobe Developer Console], edit your project. Then, select the event registration you created.

   * On the event registration details page, select **[!UICONTROL Edit Events Registration]**.

   * Select **[!UICONTROL Next]** until you reach the consumer selection screen. Then, select the consumer that you configured.

   * Update the consumer to your configured destination. Then, select **[!UICONTROL Save configured events]**.

### Validate the event flow {#validate-event-flow}

1. Make a simple catalog change, such as updating a product name or changing the enabled or disabled status.

1. Confirm the following outcomes:

   * The change is visible through [!DNL Catalog Service] APIs.
   * Your [!DNL Adobe I/O Events] consumer receives a corresponding event.

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

## Troubleshoot catalog events {#troubleshoot-catalog-events}

If catalog events are missing or delayed, work through these steps.

1. **Check Catalog Service data**

   [Use the [!DNL Catalog Service] API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/) to confirm that the catalog change is stored successfully.

2. **Verify [!DNL SaaS Data Export]**

   Catalog events require current data in [!DNL Catalog Service]. Confirm both stages of the export path:

   * **Feed export from Commerce** — On the [Data Feed Sync Status](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) page or in `var/log/saas-export.log`, confirm that [!DNL Catalog Service] feeds exported successfully from [!DNL Commerce].

   * **Sync to connected Commerce SaaS services** — On the [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard), [Catalog Sync](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync), or in export logs, confirm that data synced successfully to [!DNL Catalog Service].

   For troubleshooting export and sync jobs, see [Synchronize data with SaaS Data Export](../data-export/data-sync-manage.md) and [Logging and troubleshooting](../data-export/troubleshooting/logging.md).

3. **Validate [!DNL Adobe I/O Events] configuration**

   Confirm that:

   * The **[!UICONTROL Commerce Catalog Events]** provider is enabled.
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
>* [Synchronize data with SaaS Data Export](../data-export/data-sync-manage.md)
>* [Retrieve catalog data with the GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/){target="_blank"}
>* [[!DNL Catalog Service] and API Mesh](mesh.md)
>* [Configure the [!DNL Adobe I/O] connection](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection){target="_blank"}
>* [[!DNL Adobe I/O Events]](https://developer.adobe.com/events/docs/guides/){target="_blank"}
