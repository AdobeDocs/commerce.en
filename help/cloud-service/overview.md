---
title: '[!DNL Adobe Commerce as a Cloud Service] overview'
description: Learn about the key features and benefits of [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---

# [!DNL Adobe Commerce as a Cloud Service] overview

[!DNL Adobe Commerce as a Cloud Service] offers flexibility, scalability, and efficiency by enabling businesses to deliver and rapidly scale digital operations and accelerate innovation. Adobe's cloud-native infrastructure automatically adjusts resources to meet peak demands for traffic, orders, and catalog management.

The following table highlights the products that power [!DNL Adobe Commerce as a Cloud Service]:

<table style="table-layout:auto">
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Commerce Storefront</strong>
    </td>
    <td>
      Customer-facing interface where shoppers browse and purchase products
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Merchandising Services</strong>
    </td>
    <td>
      Backend services that manage product catalogs, pricing, and inventory
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Product Visuals</strong>
    </td>
    <td>
      Digital asset management for product images and media
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Developer Platform</strong>
    </td>
    <td>
      Core development tools and APIs for building custom functionality
    </td>
  </tr>
</table>

## Architecture

See the following video for a brief introduction to the [!DNL Adobe Commerce as a Cloud Service] architecture. Diagrams that illustrate the architecture are provided below the video.

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

This diagram illustrates the data flow between [!DNL Adobe Commerce as a Cloud Service] and all Adobe Experience Cloud solutions.

![[!DNL Adobe Commerce as a Cloud Service] architecture diagram](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Use Adobe's [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront) powered by Edge Delivery Services to create rich experiences in minutes with simple document-based authoring or visual editing with Storefront Builder.

Commerce Storefront is fully headless with a decoupled architecture that provides all Merchandising Services and data through a GraphQL API layer. This architecture allows teams to develop their frontends independently from the Commerce Foundation, providing the agility to build and test new touchpoints with emerging technologies.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] does not support Luma storefronts. If you are migrating from Adobe Commerce on Cloud or on-premises, see [existing storefronts](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts) for guidance on transitioning.

## Merchandising services and payment services

Adobe provides a rich set of intelligent, composable merchandising services to help you support your key business goals. These services also provide APIs that are critical to optimizing performance at scale.

- [Live Search](../live-search/overview.md)—Deliver smarter, faster and relevant results for shoppers with this AI-powered search tool.
- [Product Recommendations](../product-recommendations/overview.md)—Add AI-fueled recommendations based on shopper behavior, popular trends, product similarity, and more.
- [Merchandising Services powered by Catalog Views and Policies](../optimizer/setup/catalog-view.md)—Manage large and complex product catalogs with flexible data modeling to deliver highly performant, flexible commerce catalogs aligned with business structure and go-to-market strategies. Use with [Commerce Optimizer](../optimizer/overview.md) to optimize catalog performance and improve conversion rates.
- [Payment Services](../payment-services/guide-overview.md)—Drive customer satisfaction by offering various payment methods, including interest-free payment installments, and a single view into payment processing, orders, and invoices.

## Product Visuals powered by AEM Assets

Product Visuals helps simplify asset management using a digital asset management (DAM) system that integrates with the Adobe Experience Manager for managing rich media content.

The integration ensures that digital assets, such as product images or marketing content, are dynamically linked to the appropriate merchandising entities, including products and categories in Adobe Commerce, based on SKU or other key attributes.

Product Visuals is available out-of-the-box with [!DNL Adobe Commerce as a Cloud Service], providing some of the capabilities from AEM Assets.

Alternatively, the native capabilities within [!DNL Adobe Commerce as a Cloud Service] provide basic asset management tools for storing and managing digital assets.

### Product Visuals or AEM Assets

The following comparison helps you select the best option for your content supply chain needs:

<table style="width: 100%; border-collapse: collapse; margin: 20px 0;">
  <tr style="border: none;">
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">Product Visuals powered by AEM Assets</h3>
      <ul style="margin: 0; padding-left: 20px;">
        <li>Integrated, automated product image and video Digital Asset Manager (DAM)</li>
        <li>Resize, crop, and convert images</li>
        <li>High-speed image and video delivery</li>
        <li>Optimize image formats, sizes, and quality based on client browser capabilities</li>
        <li>Access to Adobe Express and Adobe Firefly</li>
        <li>Usage limits for image/video delivery capacity and user access</li>
        <li>Integrated asset selector</li>
      </ul>
    </td>
    <td style="width: 10%; text-align: center; vertical-align: middle; font-size: 98px; color: #d32f2f; font-weight: bold;">
      ›
    </td>
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">AEM Assets</h3>
      <ul style="margin: 0; padding-left: 20px;">
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
</table>

<table style="width: 100%; margin: 20px 0;">
  <tr>
    <td style="background: #f5f5f5; padding: 15px; text-align: center; font-weight: bold;">
      Adobe-branded integration is available for easy migration between offerings.
    </td>
  </tr>
</table>

See the [AEM Assets integration](../aem-assets-integration/overview.md) guide to learn more about how to integrate Product Visuals powered by AEM Assets with [!DNL Adobe Commerce as a Cloud Service].

## Developer Platform

Adobe provides developers with comprehensive extension points and tools to build applications that extend Commerce Foundation capabilities and integrate with third-party systems (such as CRMs, ERPS, and PIMS). These tools reduce your total cost of ownership of the platform in the following ways:

- **Scalability**—Applications can be scaled separately from the core software, allowing for greater efficiency and simplified upgrades.
- **Isolation**–An isolated environment means that developers can upgrade or modify their extensions at their discretion without relying on a core release.
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

Commerce Foundation provides a secure automated hosting platform and self-service features for managing your Commerce application in a cloud-native environment.

Key features include:

- Simplified onboarding
- Seamless upgrades
- Third-party integrations

### Simplified onboarding

Launch sandbox and production instances in minutes with the [!UICONTROL Commerce Cloud Manager] self-service provisioning portal. Everything that you need, including Merchandising Services, a headless Commerce instance, and App Builder, are automatically configured and integrated with your instances.

See [Getting started](getting-started.md) to learn how to create and manage Commerce instances.

### Seamless upgrades

Access the latest features and enhancements without the need for manual upgrades. The continuous delivery of new features and updates eliminates the need for manual patching, ensuring that you always have access to the latest capabilities with a low total cost of ownership.

The typical upgrade process for Adobe Commerce on Cloud involved creating backups, cloning instances, running compatibility tools, and fixing code conflicts. That's no longer necessary with [!DNL Adobe Commerce as a Cloud Service]. Adobe sends you in-app notifications when new feature and security updates have been released. You have a 30-day period to evaluate the new capabilities in your sandbox instances before the updates are automatically applied to your production environments.

>[!NOTE]
>
>Adobe guarantees backward compatibility for all updates. This means that when updates are applied, they will not break existing functionality or customizations that adhere to the [API-first extensibility](https://developer.adobe.com/commerce/extensibility/) model.

### Third-party integrations

Developers can use comprehensive [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) and [REST APIs](https://developer.adobe.com/commerce/webapi/rest/) to integrate Commerce Foundation with third-party systems and extend Commerce capabilities.

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

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
