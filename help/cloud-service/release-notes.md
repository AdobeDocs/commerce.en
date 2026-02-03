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

The following release notes contain updates to [!DNL Adobe Commerce as a Cloud Service]. 

>[!NOTE]
>
>If you are using Adobe Commerce on-premises or Adobe Commerce on cloud infrastructure, see the [Adobe Commerce release notes](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## February 2026 {#latest}

[!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."}

The following items are currently only available in Sandbox environments of [!DNL Adobe Commerce as a Cloud Service]. This release is scheduled to move to Production environments on February 10, 2026.

>[!BEGINSHADEBOX]

### Customize Admin orders and legacy admin reports

* You can now enter a custom shipping amount when creating orders in the Admin. This enhancement provides Customer Service teams with the flexibility to charge custom shipping prices for backend orders. <!-- ACCS-235 -->

* Added access to legacy Admin reports, including: Best Sellers, Coupons, Customer Accounts, Customer Orders, Customer Segments, Customer Totals, Invoiced, Low Stock, Products Sold, Products Viewed, Refunded, Sales, Shipping, Shopping Cart, and Tax. <!-- CCSAAS-3085 -->

### Capture custom invoice amounts through the REST API

* The Invoice API now supports custom capture amounts using extension attributes. This capability allows merchants to capture a custom amount when creating an invoice using the `POST V1/order/:orderId/invoice` REST endpoint and specifying the amount in the `extension_attributes.custom_capture_amount` field of the payload. As a result, merchants have greater flexibility for partial captures and specialized payment scenarios. Contact your support representative to enable this feature. <!-- ACCS-186, ACCS-197, ACCS-143 -->

### Enhancements and bug fixes

The following selected enhancements, optimizations, and bug fixes are included in this release:

* Fixed the Coupon Grid filter to display all custom coupons created through the API or by importing. <!-- CCSAAS-4509 -->

* Fixed an issue in the [!DNL Storefront Compatibility B2B Package] where the `setNegotiableQuoteShippingAddress` mutation did not save manually entered addresses to the customer's address book, even when `save_in_address_book` was set to `true`. <!-- LYNX-1031 --> 

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* Resolved an issue where product images were not displaying properly in [!DNL Edge Delivery Services] due to corrupted `no_selection` values in custom attributes related to asset roles. <!-- ACAP-1206 -->

* Resolved an issue preventing federated user accounts with null first name or last name values from accessing the Commerce Admin. <!-- ACCS-200 -->

* Various performance and optimization improvements. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

* Simplified the Asset Selector configuration by automatically providing region-specific IMS Client IDs. Merchants no longer need to submit support tickets to configure Asset Selector for mapping product category images with assets. The system now automatically uses dedicated IMS Client IDs based on the Commerce region. <!-- ACCS-175 -->

### Internal improvements (to be deleted)

* Updated Adobe IMS Client ID configuration in development environment templates. <!-- CCSAAS-4473 -->

* Prepared infrastructure to support switchable MDEE feed versions (V1 to V2 - CCDM), allowing future migration to Common Commerce Data Model format. <!-- CCSAAS-3728 -->

* Disabled the category design cache observer for headless architecture, removing unnecessary overhead in Commerce implementations using [!DNL Edge Delivery Services]. <!-- CCSAAS-4494 -->

* Fixed invalid URL formation for V2 feed service endpoints that was missing the `/api` path segment. <!-- CCSAAS-4501 -->

* Resolved feed metadata errors for Commerce Optimizer price book feeds. <!-- CCSAAS-4505 -->

* Fixed company lookup errors that occurred when processing B2B company data. <!-- CCSAAS-4457 -->

* Resolved REST API filter issues that prevented using `pickup_location_code` field for filtering orders with pickup locations. <!-- ACCS-199 -->

* Corrected Admin UI permissions that were incorrectly limited for users properly configured as Product Administrators in the Admin Console. <!-- ACCS-217 -->

* Added access for legacy reports in the Commerce Admin. <!-- CCSAAS-3085 -->

* Resolved an issue where the Admin crashed when configuring an [!DNL Admin UI SDK] menu extension with an invalid identifier. Additional validation checks now prevent processing of extensions with non-existent IDs. <!-- CEXT-5701 -->

* Removed the **[!UICONTROL Login as Customer]** button from Order, Invoice, Shipment, and Credit Memo pages in the Admin. This feature is not supported in headless Commerce implementations using [!DNL Edge Delivery Services]. <!-- ACCS-38 -->

* Fixed the Coupon Grid filter to display all custom coupons created through the API or by importing. Previously, the grid only showed auto-generated coupons and filtered out manually created coupons. This change makes API-created and imported coupons visible to merchants and enables Export functionality to include all coupon types. <!-- CCSAAS-4509 -->

* Resolved an issue where product images were not displaying properly in [!DNL Edge Delivery Services] due to corrupted `no_selection` values in custom attributes related to asset roles. The [!DNL AEM Assets] integration now detects and removes these invalid values to ensure proper image display. <!-- ACAP-1206 -->

* Implemented OPcache preloading to optimize PHP bootstrap performance. By loading framework core classes, dependency injection container components, and GraphQL engine classes into shared memory at startup, this enhancement eliminates file I/O overhead for critical classes loaded on every request. <!-- CCSAAS-4255 -->

* Improved sorting for generated GraphQL schemas to ensure consistent output regardless of module installation order, reducing unnecessary changes to the router service. <!-- CCSAAS-4472 -->

* Added performance monitoring for Admin Order Grid browsing scenarios in trend builds. <!-- CCSAAS-4462 -->

* Moved predefined event and webhook configuration from Commerce Core SaaS service to regular Commerce modules, making event metadata available in both PaaS and SaaS environments. <!-- CEXT-5253 -->

* Enhanced bundle product data collection to register and handle failed items during bundle product options processing. <!-- CCSAAS-4458 -->

#### Version updates (to be deleted)

* Updated [!DNL Storefront Compatibility Package for B2B] to version 1.0.16. <!-- LYNX-1031 -->

* Updated [!DNL AEM Assets Integration] extension to version 1.2.12. <!-- ACAP-1206 -->

* Updated [!DNL Admin UI SDK] to version 3.2.6. <!-- CEXT-5701 -->

{{accs-release}}

>[!ENDSHADEBOX]

## January 2026

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

The following items were released to Production environments of [!DNL Adobe Commerce as a Cloud Service] on January 20, 2026.

>[!BEGINSHADEBOX]

### B2B drop-ins

The following changes were made to B2B drop-in components:

* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). The following B2B drop-ins are now available:

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
