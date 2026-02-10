---
title: '[!DNL Adobe Commerce as a Cloud Service] release notes'
description: Learn about the latest features, enhancements, and improvements in [!DNL Adobe Commerce as a Cloud Service], including GraphQL updates, App Builder integrations, and B2B capabilities.
feature: App Builder, GraphQL, Integration, SaaS
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
---
# Release notes

The following release notes contain updates to [!DNL Adobe Commerce as a Cloud Service]. 

>[!NOTE]
>
>If you are using Adobe Commerce on-premises or Adobe Commerce on cloud infrastructure, see the [Adobe Commerce release notes](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## February 2026 {#latest}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

The following items were released to Production environments of [!DNL Adobe Commerce as a Cloud Service] on February 10, 2026.

>[!BEGINSHADEBOX]

### Customize shipping methods and view Admin reports

The following enhancements were made to the [!DNL Commerce Admin]:

* Enhanced out-of-process [shipping webhook payloads](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) to include shipping address custom attributes. This change enables merchants to implement custom shipping methods. <!-- ACCS-235 -->

* Added access to Admin reports, including reports for [Customers](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports), [Marketing](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports), [Products](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports), and [Sales](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>Reports not available in [!DNL Adobe Commerce as a Cloud Service] are labelled as PaaS only ([!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}).

### Capture custom invoice amounts through the REST API

The Invoice API now supports [custom capture amounts](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) using extension attributes. <!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>Due to legal restrictions, the custom capture amount is only available in the North American (NA) region and other regions where payment overcapture is permitted.

### Enhancements and bug fixes

The following selected enhancements, optimizations, and bug fixes are included in this release:

* Fixed the Coupon Grid filter to display all custom coupons created through the API or by importing. <!-- CCSAAS-4509 -->

* Fixed an issue in the [!DNL Storefront Compatibility B2B Package] where the `setNegotiableQuoteShippingAddress` mutation did not save manually entered addresses to the customer's address book, even when `save_in_address_book` was set to `true`. <!-- LYNX-1031 --> 

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* Resolved an issue where product images were not displaying properly in [!DNL Edge Delivery Services] due to corrupted `no_selection` values in custom attributes related to asset roles. <!-- ACAP-1206 -->

* Resolved an issue preventing federated user accounts with null first name or last name values from accessing the Commerce Admin. <!-- ACCS-200 -->

* Simplified the Asset Selector configuration by automatically providing region-specific IMS Client IDs. Merchants no longer need to submit support tickets to configure Asset Selector for mapping product category images with assets. The system now automatically uses dedicated IMS Client IDs based on the Commerce region. <!-- ACCS-175 -->

* Various performance and optimization improvements. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

>[!ENDSHADEBOX]

## January 2026

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

The following items were released to Production environments of [!DNL Adobe Commerce as a Cloud Service] on January 20, 2026.

>[!BEGINSHADEBOX]

### B2B drop-ins

The following changes were made to B2B drop-in components:

* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). The following B2B drop-ins are now available:

  * **[Company management](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** - Enables company profile management and role-based permissions for Adobe Commerce storefronts.
  * **[Company switcher](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** - Provides a UI component for users to switch between multiple companies they are associated with.
  * **[Purchase orders](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** - Manages purchase order workflows, approval rules, and purchase order history for B2B transactions.
  * **[Quote management](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** - Enables negotiable quotes for B2B customers with quote request, negotiation, and approval workflows.
  * **[Requisition lists](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)** - Provides tools for creating and managing requisition lists for repeat purchases and bulk ordering.

* Released the B2B Storefront Compatibility Package. This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Clickable links to external shipping trackers

Transform shipment tracking numbers included in shopper emails from plain text into clickable links by [enabling Custom Tracking URLs](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). This feature is supported for USPS, UPS, FedEx, and DHL. <!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise support

[!DNL Adobe Commerce as a Cloud Service] storefronts now support [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). This feature delivers advanced bot protection by using adaptive risk analysis and machine learning to accurately distinguish human users from automated bots. It strengthens site security, prevents fraudulent activities, and reduces spam and abuse to maintain a trusted shopping experience. <!-- CCSAAS-4242 -->

### Instance-specific admin access

You can now [assign users access](./user-management.md#add-users) to individual [!DNL Adobe Commerce as a Cloud Service] instances in the Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Observability

By using [!DNL App Builder], you can gain deeper visibility into your [!DNL Adobe Commerce as a Cloud Service] instance with [OpenTelemetry observability](https://developer.adobe.com/commerce/extensibility/observability/), now automatically available. OpenTelemetry provides metrics, logs, and traces to help you monitor performance, troubleshoot issues faster, and optimize your storefront. This capability enables proactive insights into system health and improves reliability for your customers.

>[!NOTE]
>
>OpenTelemetry observability requires the use of [!DNL App Builder] or other out-of-process extensibility (OOPE) offerings.

### Tier pricing for catalog price rules

You can now combine tiered pricing discounts with catalog rule discounts using [catalog price rules](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). This enhancement allows you to create more dynamic and competitive pricing strategies—rewarding bulk purchases while applying promotional discounts at the same time. The result is greater flexibility to attract customers, increase order value, and drive conversions.<!-- See PR #708 in commerce-admin -->

### Enhancements and bug fixes

The following selected enhancements, optimizations, and bug fixes included in this release:

* Resolved an error that could occur when uploading a file to S3. <!-- CCSAAS-4189 -->

* Resolved a `User is not entitled to access this instance` error that could occur when logging into the Commerce Admin or accessing the REST API. <!-- CCSAAS-4324 -->

* Corrected an error that occurred when previewing or queueing a newsletter from the Newsletter Template grid. <!-- CCSAAS-4398 --> 

* Fixed a `404` error that occurred when clicking the [!UICONTROL **Reload Data**] button on the Admin dashboard. <!-- CCSAAS-4468 -->

* Resolved an issue where product custom attributes could not be updated through the REST API when [!DNL AEM Assets integration] was enabled and the product had images. <!-- ACAP-1178 -->

* Various performance and optimization improvements.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## November 2025

>[!BEGINSHADEBOX]

### Enhancements

* [User management](./user-management.md) - Changed **Product Admin** role in the Admin Console to automatically update user access to the Commerce Admin. <!-- CCSAAS-3012 -->

* Added the ability to upload and retrieve negotiable quote attachments as well as files and images associated with customers and customer addresses to Amazon S3 using presigned URLs in [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) and [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). With REST, you can also upload category images. <!-- CCSAAS-3250 -->

* Added the `POST /V1/customers` and `PUT /V1/customers/{customerId}` endpoints to the [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) to create and update customers. These endpoints require IMS authorization. <!-- CCSAAS-3112 -->

* Added the [`exchangeOtpForCustomerToken` mutation](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), which requires a shopper's email address and one-time password (OTP), and receives a customer token in exchange. This mutation is typically used in scenarios where a customer needs to authenticate using an OTP sent to their email or phone.

* If an address defined in the [!UICONTROL **Store Email Addresses**] configuration screen in the Admin contains a value that ends with `example.com`, Commerce does not send emails to this address. Instead, the system logs that the email was not sent.  <!-- CCSAAS-3533 -->

#### Custom order attributes

* Admin users can now view and edit [custom order attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directly from the Order View, Edit, and Create screens in the Admin panel. This enhancement improves the management of custom order data created via GraphQL.  <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
