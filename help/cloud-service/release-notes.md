---
title: '[!DNL Adobe Commerce as a Cloud Service] release notes'
description: Learn about the latest features and improvements in [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
---
# Release notes

The following release notes contain updates to [!DNL Adobe Commerce as a Cloud Service]. For release information for other products, refer to [Adobe Commerce Optimizer](../optimizer/release-notes.md) or [Adobe Commerce on-premises and Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## September 2025

**Release date**: September 11, 2025

>[!BEGINSHADEBOX]

### Enhancements

- Upgraded Adobe Commerce as a Cloud Service to contain all changes from Adobe Commerce PaaS `2.4.8-p2`. <!-- CCSAAS-3111 -->
- Changed **Product Admin** role in the Admin Console to automatically update user access to the Commerce Admin. <!-- CCSAAS-3012 -->
- Enabled uploading category images using REST API for categories. <!-- CCSAAS-3250 -->

#### Custom attributes

- Added API support to upload media files as customer custom attributes. <!-- CCSAAS-2456 -->
- Added support for storefront users to download files from customer custom attributes. <!-- CCSAAS-3398 -->
- Exposed custom order attributes in the admin panel for viewing and editing. <!-- CEXT-5044 -->

#### Logging

- Added a new module with message queue/consumer setup and log forwarding. <!-- CEXT-5057 -->
- Added enhanced logging and extension points for Commerce Eventing, including Opentelemetry context. <!-- CEXT-4802 -->
- Implemented additional logging and extension points for Commerce Webhooks with Opentelemetry support. <!-- CEXT-4801 -->

>[!ENDSHADEBOX]

## August 2025

**Release date**: August 28, 2025

>[!BEGINSHADEBOX]

### EU region now available

European Union region (eu1) support for customer IMS organizations is now available. You can now select **European Union** as a **Region** when [adding a Commerce SaaS instance](./getting-started.md#create-an-instance) in the Cloud Manager. The European Union region is only available for production environments.

The base production URLs for the European Union region are:

* Admin: `https://eu1.admin.commerce.adobe.com`
* REST and GraphQL: `https://eu1.api.commerce.adobe.com`

![create instance](./assets/create-instance-eu.png){width="600" align="center" zoomable="yes"}

>[!ENDSHADEBOX]
