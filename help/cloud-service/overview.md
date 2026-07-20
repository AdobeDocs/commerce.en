---
title: '[!DNL Adobe Commerce as a Cloud Service] overview'
description: Learn about the key features and benefits of [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
autotag-review: '2026-06-18T16:02:31.185Z'
TQID: 'https://experienceleague.adobe.com/D1Aq9qlw2HprQUy-g5KcIH2Ky2XUDawZIrAbe2Jz6ZI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
    internal-label: Categories
  - id: f236e2a1-90d4-477d-92e1-5996b5e92bff
    internal-label: Experience Cloud integration
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
    internal-label: Experimentation
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
---
# [!DNL Adobe Commerce as a Cloud Service] overview

[!DNL Adobe Commerce as a Cloud Service] offers flexibility, scalability, and efficiency by enabling businesses to deliver and rapidly scale digital operations while accelerating innovation. Adobe's cloud-native infrastructure automatically adjusts resources to meet peak demands for traffic, orders, and catalog management.

The following table highlights the products that power [!DNL Adobe Commerce as a Cloud Service]:

<table style="table-layout:auto">
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="checkmark" align="center"> <strong>Commerce Storefront</strong>
    </td>
    <td align="left">
      Customer-facing interface where shoppers browse and purchase products
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="checkmark" align="center"> <strong>Merchandising Services</strong>
    </td>
    <td align="left">
      Backend services that manage product catalogs, pricing, and inventory
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="checkmark" align="center"> <strong>Product Visuals</strong>
    </td>
    <td align="left">
      Digital asset management for product images and media
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="checkmark" align="center"> <strong>Developer Platform</strong>
    </td>
    <td align="left">
      Core development tools and APIs for building custom functionality
    </td>
  </tr>
</table>

## Architecture

See the following video for a brief introduction to the [!DNL Adobe Commerce as a Cloud Service] architecture. Diagrams that illustrate the architecture are provided below the video.

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

This diagram illustrates the data flow between [!DNL Adobe Commerce as a Cloud Service] and all Adobe Experience Cloud solutions.

![Data flow diagram showing [!DNL Adobe Commerce as a Cloud Service] integration with [!DNL Adobe Experience Cloud] solutions](./assets/data-flow.png){zoomable="yes"}

## Commerce Storefront

Use Adobe's [[!DNL Commerce Storefront]](https://experienceleague.adobe.com/developer/commerce/storefront) powered by [!DNL Edge Delivery Services] to create rich experiences in minutes with simple document-based authoring or visual editing with [!DNL Storefront Builder].

[!DNL Commerce Storefront] is fully headless with a decoupled architecture that provides all Merchandising Services and data through a GraphQL API layer. This architecture allows teams to develop their frontends independently from the Commerce Foundation, providing the agility to build and test new touchpoints with emerging technologies.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] does not support Luma storefronts. If you are migrating from Adobe Commerce on Cloud or on-premises, see [existing storefronts](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts) for guidance on transitioning.

## Merchandising services and payment services

Adobe provides a rich set of intelligent, composable merchandising services to help you support your key business goals. These services also provide APIs that are critical to optimizing performance at scale.

- [Live Search](../live-search/overview.md)—Deliver smarter, faster and relevant results for shoppers with this AI-powered search tool.
- [Product Recommendations](../optimizer/merchandising/recommendations/overview.md)—Add AI-fueled recommendations based on shopper behavior, popular trends, product similarity, and more.
- [Catalog Service](../catalog-service/guide-overview.md)—Give your customers an optimized product experience while boosting performance, improving scalability, and increasing conversions.
- [Payment Services](../payment-services/guide-overview.md)—Drive customer satisfaction by offering various payment methods, including interest-free payment installments, and a single view into payment processing, orders, and invoices.

## [!DNL Product Visuals powered by AEM Assets]

Product Visuals helps simplify asset management using a digital asset management (DAM) system that integrates with Adobe Experience Manager for managing rich media content.

The integration ensures that digital assets, such as product images or marketing content, dynamically link to the appropriate merchandising entities, including products and categories in Adobe Commerce, based on SKU or other key attributes.

[!DNL Product Visuals] is available out-of-the-box with [!DNL Adobe Commerce as a Cloud Service], providing some of the capabilities from [!DNL AEM Assets].

Alternatively, the native capabilities within [!DNL Adobe Commerce as a Cloud Service] provide basic asset management tools for storing and managing digital assets.

Check the [AEM Assets integration](../aem-assets-integration/overview.md) guide to learn more about how to integrate [!DNL Product Visuals powered by AEM Assets] with [!DNL Adobe Commerce as a Cloud Service].

### [!DNL Product Visuals] or [!DNL AEM Assets]

The following comparison helps you select the best option for your content supply chain needs:

<table>
  <tr>
    <td align="left">
      <strong>[!DNL Product Visuals powered by AEM Assets]</strong>
      <ul>
        <li>Integrated, automated product image and video Digital Asset Manager (DAM)</li>
        <li>Resize, crop, and convert images</li>
        <li>High-speed image and video delivery</li>
        <li>Optimize image formats, sizes, and quality based on client browser capabilities</li>
        <li>Access to Adobe Express and Adobe Firefly</li>
        <li>Usage limits for image/video delivery capacity and user access</li>
        <li>Integrated asset selector</li>
      </ul>
    </td>
    <td align="center">
      <br><br><br><br><br><br><br><br><br><br><br>
      <img src="../assets/icon-double-chevron-right.svg" alt="chevron" width="100">
    </td>
    <td align="left">
      <strong>AEM Assets</strong>
      <ul>
        <li>All capabilities from Product Visuals</li>
        <li>Full marketing Digital Asset Manager (DAM)</li>
        <li>Unlimited users (pay per user)</li>
        <li>Unlimited image and video delivery</li>
        <li>Advanced asset management functionality:</li>
        <ul>
          <li>360° spin sets and interactive viewers</li>
          <li>3D model support and immersive content</li>
          <li>PDF support</li>
          <li>AI-powered smart cropping</li>
          <li>Dynamic image templates</li>
          <li>Smart tagging</li>
          <li>Tracking and analytics on asset performance</li>
        </ul>
      </ul>
    </td>
  </tr>
    <tr>
    <td align="center" colspan="3">
      <strong>Adobe-branded integration is available for easy migration between offerings.</strong>
    </td>
  </tr>
</table>

## Developer Platform

Adobe provides developers with comprehensive extension points and tools to build applications that extend Commerce Foundation capabilities and integrate with third-party systems (such as CRMs, ERPs, and PIMs). These tools reduce your total cost of ownership of the platform in the following ways:

- **Scalability**—Applications can be scaled separately from the core software, allowing for greater efficiency and simplified upgrades.
- **Isolation**—An isolated environment means that developers can upgrade or modify their extensions at their discretion without relying on a core release.
- **Technological independence**–Developers can choose whichever technology stacks and coding languages that fit their needs.

>[!TIP]
>
>Vendor-built apps are also available for installation on [Adobe Exchange](https://exchange.adobe.com/).

Adobe provides the following developer tools for building integrations and customizations:

- [**API Mesh for Adobe Developer App Builder**](https://developer.adobe.com/graphql-mesh-gateway/)—Coordinate and combine multiple API, GraphQL, REST, and other sources into a single, queryable GraphQL endpoint.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/)—Build and deploy secure and scalable web applications that extend Commerce functionality and integrate with third-party solutions.
- [**Events**](https://developer.adobe.com/commerce/extensibility/events/)—Use custom event triggers to interact with other extensible development tools.
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/)—Use webhooks to trigger interactions between Commerce and third-party systems automatically.
- [**Admin UI SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/)—Customize and enhance the Commerce Admin with new pages and features for your merchants.
- [**Integration Starter Kit**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)—Accelerate your back-office integrations with reference integrations, onboarding scripts, and a standardized architecture.

## Commerce Foundation

[!DNL Commerce Foundation] provides a secure automated hosting platform and self-service features for managing your Commerce application in a cloud-native environment.

Key features include:

- Simplified onboarding
- Seamless upgrades
- Third-party integrations

### Simplified onboarding

Launch sandbox and production instances in minutes with the [!UICONTROL Commerce Cloud Manager] self-service provisioning portal. Everything that you need, including Merchandising Services, a headless Commerce instance, and [!DNL App Builder], is automatically configured and integrated with your instances.

See [Getting started](getting-started.md) to learn how to create and manage Commerce instances.

### Seamless upgrades

Access the latest features and enhancements without the need for manual upgrades. The continuous delivery of new features and updates eliminates the need for manual patching, ensuring that you always have access to the latest capabilities with a low total cost of ownership.

The typical upgrade process for Adobe Commerce on Cloud involved creating backups, cloning instances, running compatibility tools, and fixing code conflicts. That's no longer necessary with [!DNL Adobe Commerce as a Cloud Service]. Adobe sends you in-app notifications when new feature and security updates have been released. You have a 30-day period to evaluate the new capabilities in your sandbox instances before the updates are automatically applied to your production environments.

>[!NOTE]
>
>Adobe guarantees backward compatibility for all updates. This means that when updates are applied, they will not break existing functionality or customizations that adhere to the [API-first extensibility](https://developer.adobe.com/commerce/extensibility/) model.

### Third-party integrations

Developers can use comprehensive [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) and [REST APIs](https://developer.adobe.com/commerce/webapi/rest/) to integrate [!DNL Commerce Foundation] with third-party systems and extend Commerce capabilities.

<!-- 
## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. 
-->

## Benefits

The following sections provide information about the benefits that [!DNL Adobe Commerce as a Cloud Service] provides to business and IT leaders.

### Business leaders

- **Grow revenue**: Drive organic traffic with a high-performance storefront that boosts SEO. Create personalized experiences that drive conversion using rich data.
- **Scale operations**: Auto-scaling services meet the peak demands of your business with 99.9% availability. Rollout multiple brands and regions and support B2B and B2C from a single instance. Support large and complex product catalogs with flexible data modeling.
- **Boost merchandiser productivity**: Use AI powered merchandising services to improve conversion. Experiment natively, directly in the storefront. Manage the storefront experience to create rich experiences in minutes with simple document-based authoring or a visual editor.
- **Lower total cost of ownership (TCO) and accelerate innovation**: Always up-to-date services give you access to new features immediately. Activate new capabilities by easily installing apps from the marketplace. Free up resources from tedious maintenance to focus on building new capabilities.

### Information technology (IT) leaders

- **Fast provisioning**: Get started fast with self-service provisioning in minutes. All services are pre-configured to work seamlessly together to get started faster. Provision sandboxes for developer experimentation as needed.
- **Low cost of ownership**: No more upgrades with always up-to-date services. Stay secure and compliant with the latest security patches automatically applied for you. Scale automatically to meet the most demanding workloads.
- **High-performance storefront**: Create rich experiences in minutes with simple document-based authoring or a visual editor. Use AI-powered merchandising services to improve conversion. Native experimentation built into the storefront.
- **Faster innovation**: Free up resources from tedious maintenance to focus on building new capabilities that deliver business value. Use comprehensive extensibility and standards-based technologies (JavaScript, HTML, CSS, and low-code tools) to build differentiated experiences. Install third-party apps with a click to add new capabilities to your commerce platform.
