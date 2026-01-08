---
title: '[!DNL Adobe Commerce as a Cloud Service] release notes'
description: Learn about the latest features and improvements in [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
---
# Release notes

The following release notes contain updates to [!DNL Adobe Commerce as a Cloud Service]. For release information for other products, refer to [Adobe Commerce Optimizer](../optimizer/release-notes.md) or [Adobe Commerce on-premises and Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

[!DNL Adobe Commerce as a Cloud Service] contains the latest versions of merchandising services, payments services, and extensibility releases. Use the following links to view the release notes for each:

| Services | Extensibility |
| --- | --- |
| <ul><li>[Catalog Service](../catalog-service/release-notes.md)</li><li>[Live Search](../live-search/release-notes.md)</li><li>[Payment Services](../payment-services/release-notes.md)</li><li>[Product Recommendations](../product-recommendations/release-notes.md)</li><li>[SaaS Data Export](../data-export/release-notes.md)</li></ul> | <ul><li>[Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[Events](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> |

## January 2026 {#latest}

[!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments."}

The following items are currently only available in Sandbox environments. This release is scheduled to move to Production environments on January XX, 2026.

>[!BEGINSHADEBOX]

### Instance-specific admin access

* You can now [assign users access](./user-management.md#add-users) to individual Adobe Commerce as a Cloud Service instances in the Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Google reCAPTCHA Enterprise support

* Added support for Google [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise), which provides advanced bot protection for Adobe Commerce as a Cloud Service storefronts. reCAPTCHA Enterprise uses adaptive risk analysis and machine learning to differentiate between human users and bots. This helps to prevent fraudulent activities, spam, and abuse on customer sites. <!-- CCSAAS-4242 -->

### Tier pricing for catalog price rules

* [Catalog price rules](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules) can now include tier pricing in their discount calculations. This allows you to combine tiered pricing discounts with catalog rule discounts for more flexible pricing strategies. <!-- See PR #708 in commerce-admin -->

![Apply Catalog Price Rule](assets/release/sales-promotions-settings.png)

### Security enhancements

* Access tokens for Adobe IMS admin authentication are now only accepted through POST requests. <!-- CCSAAS-4421 -->

### Enhancements and bug fixes

* Added missing GraphQL properties to quote template types including `NegotiableQuoteTemplate`, `ItemNote`, and `NegotiableQuoteTemplateGridItem`. <!-- LYNX-978 -->

* Resolved an error that could occur when uploading a file to S3. <!-- CCSAAS-4189 -->

* Resolved a `User is not entitled to access this instance` error that could occur when logging into the admin or accessing the REST API. <!-- CCSAAS-4324 -->

* Various performance and optimization improvements.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 -->

>[!ENDSHADEBOX]

## November 2025

>[!BEGINSHADEBOX]

### Enhancements

* [User management](./user-management.md) - Changed **Product Admin** role in the Admin Console to automatically update user access to the Commerce Admin. <!-- CCSAAS-3012 -->

* Added the ability to upload and retrieve negotiable quote attachments as well as files and images associated with customers and customer addresses to Amazon S3 using presigned URLs in [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) and [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). With REST, you can also upload category images. <!-- CCSAAS-3250 -->

* Added the `POST /V1/customers` and `PUT /V1/customers/{customerId}` endpoints to the [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) to create and update customers. These endpoints require admin authorization. <!-- CCSAAS-3112 -->

* Added the [`exchangeOtpForCustomerToken` mutation](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), which requires a shopper's email address and one-time password (OTP), and receives a customer token in exchange. This mutation is typically used in scenarios where a customer needs to authenticate using an OTP sent to their email or phone.

* If an address defined in the [!UICONTROL **Store Email Addresses**] configuration screen in the Admin contains a value that ends with `example.com`, Commerce does not send emails to this address. Instead, the system logs that the email was not sent.  <!-- CCSAAS-3533 -->

#### Custom order attributes

* Admin users can now view and edit [custom order attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directly from the Order View, Edit, and Create screens in the Admin panel. This enhancement improves the management of custom order data created via GraphQL.  <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
