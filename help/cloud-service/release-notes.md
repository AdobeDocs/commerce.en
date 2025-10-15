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

[!DNL Adobe Commerce as a Cloud Service] contains the latest versions of merchandising services, payments services, and extensibility releases. Use the following links to view the release notes for each:

* Services
  * [Catalog Service](../catalog-service/release-notes.md)
  * [Live Search](../live-search/release-notes.md)
  * [Payment Services](../payment-services/release-notes.md)
  * [Product Recommendations](../product-recommendations/release-notes.md)
  * [SaaS Data Export](../data-export/release-notes.md)
* Extensibility
  * [Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
  * [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
  * [Events](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
  * [Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

## October 2025

>[!BEGINSHADEBOX]

### Enhancements

* [User management](./user-management.md) - Changed **Product Admin** role in the Admin Console to automatically update user access to the Commerce Admin. <!-- CCSAAS-3012 -->

* Added the ability to upload and retrieve negotiable quote attachments as well as files and images associated with customers and customer addresses to Amazon S3 using presigned URLs in [GraphQL](developer.adobe.com/commerce/webapi/graphql/schema/uploads) and [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). With REST, you can also upload category images. <!-- CCSAAS-3250 -->

* Added the `POST /V1/customers` and `PUT /V1/customers/{customerId}` endpoints to the [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) to create and update customers. These endpoints require admin authorization. <!-- CCSAAS-3112 -->

* If an address defined in the [!UICONTROL **Store Email Addresses**] configuration screen in the Admin contains a value that ends with `example.com`, Commerce does not send emails to this address. Instead, the system logs that the email was not sent.  <!-- CCSAAS-3533 -->

#### Custom order attributes

* Admin users can now view and edit [custom order attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)  directly from the Order View, Edit, and Create screens in the Admin panel. This enhancement improves the management of custom order data created via GraphQL.  <!-- CEXT-5044 -->

>[!ENDSHADEBOX]

## August 2025

>[!BEGINSHADEBOX]

### EU region now available

European Union region (eu1) support for customer IMS organizations is now available. You can now select **European Union** as a **Region** when [adding a Commerce SaaS instance](./getting-started.md#create-an-instance) in the Cloud Manager. The European Union region is only available for production environments.

The base production URLs for the European Union region are:

* Admin: `https://eu1.admin.commerce.adobe.com`
* REST and GraphQL: `https://eu1.api.commerce.adobe.com`

![create instance](./assets/create-instance-eu.png){width="600" align="center" zoomable="yes"}

>[!ENDSHADEBOX]
