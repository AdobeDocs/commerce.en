---
title: '[!DNL Adobe Commerce as a Cloud Service] release notes'
description: Learn about the latest features and improvements in [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
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

## April 2026 {#latest}

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

The following items were released to Production environments on April 1, 2026.

>[!BEGINSHADEBOX]

### Check price and stock alert subscription status through GraphQL

New GraphQL queries, [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"} and [`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}, let storefronts determine whether a shopper is already subscribed to stock or price alerts for a product. <!-- ACCS-334 -->

### Create numeric product attributes that support negative values

A new `numeric` [product attribute input type](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) allows merchants to create decimal attributes that support negative values. <!-- ACCS-600 -->

### Query reCAPTCHA configuration for multiple forms in one GraphQL request

The [`recaptchaFormConfigs` query](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/) can return configuration details for multiple form types in a single request. <!-- ACCS-628 -->

### View all company orders with a new B2B permission

A new `view_all_company_orders` [company role](https://developer.adobe.com/commerce/webapi/rest/b2b/roles/) enables B2B company customers to view all orders within their company, including historical orders created by Admin users. <!-- ACCS-675 -->

### Enhancements and bug fixes

The following selected enhancements, optimizations, and bug fixes are included in this release:

* You can now filter Order and Company REST API results using applicable custom attributes, supporting scenarios such as company-scoped order searches. <!-- ACCS-633 -->

* Resolved an error that could appear in the browser developer console. <!-- CCSAAS-4650 -->

* Fixed an error that could occur when cancelling a guest order with order comments. <!-- ACCS-674 -->

* Fixed an error that could occur when adding a grouped product with many associated items to a requisition list. <!-- ACCS-627 -->

{{accs-release}}

>[!ENDSHADEBOX]

## March 2026 - release #2

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

The following items were released to Production environments on March 24, 2026.

>[!BEGINSHADEBOX]

### Log in as a customer using one-time codes

Admins can now generate [one-time codes](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer) for customer impersonation through the [!DNL Commerce Admin] and REST API. The one-time code can be exchanged for a customer access token through the `generateCustomerToken` or `exchangeOtpForCustomerToken` GraphQL mutations, enabling passwordless "Login as Customer" flows for seller-assisted shopping scenarios. <!-- ACCS-404 -->

For guidance on implementing this feature using APIs, see the [REST API](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/) and [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/) documentation.

### Manage gift card accounts through the REST API

[Gift card accounts](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/) can now be created, updated, deleted, and queried through the REST API. Additionally, JSON bulk import support is available through the `/V1/import/json` endpoint, enabling third-party integrations to programmatically synchronize gift cards. <!-- ACCS-476 -->

### Trigger transactional emails through the REST API

A new REST API endpoint (`POST /V1/custom-email/send`) allows you to [trigger transactional emails](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/) on demand by specifying an email template ID, recipient email, and template variables. The API supports nested arrays as template variables for complex email content. <!-- ACCS-325, ACCS-481 -->

### Subscribe to the out-of-process shipping get-rates webhook

The `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` webhook is now available in the Admin Webhooks list in [!DNL Adobe Commerce as a Cloud Service]. Use it to implement [custom shipping methods](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods). <!-- ACCS-478 -->

### Upload PDFs and other files through product attributes

A new "file" [Attribute Input Type](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) allows you to create attribute sets where you can upload files, such as PDFs, to individual products. You can configure allowed file extensions and max file size by navigating to [!UICONTROL **Stores**] > [!UICONTROL **Configuration**] > [!UICONTROL _Catalog_] > [!UICONTROL **Product File Attributes**]. <!-- ACCS-535, ACCS-565 -->

### Configure company custom attributes

Admins can now manage company custom attributes on the Company edit page in the [!DNL Commerce Admin]. Custom attributes can be configured, saved, and validated from the Admin UI for [!DNL Adobe Commerce as a Cloud Service]. 

To configure company custom attributes, navigate to [!UICONTROL **Customers**] > [!UICONTROL **Companies**] and select a company to open the edit page. Then select the [!UICONTROL **Custom Attributes**] tab to add new attributes.
<!-- ACCS-294 -->

### Subscribe to price and stock alerts through GraphQL

EDS storefronts now work with [price and stock alerts](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup). <!-- ACCS-334 -->

Additionally, there are several new GraphQL mutations to subscribe and unsubscribe to price and stock alerts:

+++New GraphQL mutations

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### Enhancements and bug fixes

The following selected enhancements, optimizations, and bug fixes are included in this release:

* The [!UICONTROL Sales] > [!UICONTROL View Orders] company role now functions as expected. <!-- ACCS-604 -->

* The `last_login_at` customer extension attribute is now available through the REST API, enabling integrations to retrieve the most recent login date for each customer. <!-- ACCS-555 -->

* Fixed an issue with the [!DNL AEM Assets] integration form suggestions. <!-- ACCS-209 -->

* Fixed an issue where bulk company assignment and unassignment actions on the Shared Catalog grid could cause an error. <!-- CCSAAS-4614 -->

* Fixed an issue where custom cart pricing was overwritten when the same product was added to the cart again with a different quantity or custom price. <!-- ACCS-529 -->

* Requisition list item UIDs are now consistent with cart and wishlist item UIDs. <!-- ACCS-349 -->

* Fixed a product edit page timeout that could occur with large shared catalogs. <!-- CCSAAS-4657 -->

* Re-enabled the GET `/V1/directory/countries` and GET `/V1/directory/countries/:countryId` REST API endpoints for admin integrations, allowing clients to look up valid country and region data. <!-- ACCS-518 -->

* Fixed a timeout issue that could occur in the REST API when a user has a large shared catalog. <!-- ACCS-4657 -->

* Fixed an issue where blocked B2B companies could still add products to the cart. <!-- ACCS-552 -->

* If you have a large amount of data on the Customer or Company grids, the export buttons are no longer available to prevent errors. <!-- ACCS-320 -->

* Fixed an issue where attached file sizes did not display correctly. <!-- ACCS-566 -->

* Fixed an issue with creating and deleting "File" attribute types in the [!DNL Commerce Admin]. <!-- ACCS-605, ACCS-606 -->

{{accs-release}}

>[!ENDSHADEBOX]


## March 2026 - release #1

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

The following items were released to Production environments of [!DNL Adobe Commerce as a Cloud Service] on March 9, 2026.

>[!BEGINSHADEBOX]

### App Builder AI coding tools and tutorials

You can now use the [AI coding developer tooling](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"} to create new [!DNL App Builder] applications and convert existing [!DNL Adobe Commerce] PHP extensions to [!DNL App Builder] applications. The following tutorials are available to demonstrate how to use the tools:

* [Tutorial prerequisites](./tutorials/tutorial-prerequisites.md)
* [Ratings extension tutorial](./tutorials/ratings-extension.md)
* [Shipping method extension tutorial](./tutorials/shipping-method-extension.md)

### Access App Builder app management through the Admin

The [!DNL Commerce Admin] now includes a menu item linking to [App Management](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}, a unified shell for managing [!DNL App Builder] apps associated with the Commerce instance. This addition is powered by the latest Admin UI SDK update. <!-- CEXT-5755 -->

### Request entity creation limit change

The limit on the number of websites, stores, and store views was previously limited to 50. You can now submit a [support request](https://experienceleague.adobe.com/home?support-tab=home#support) to modify these limits, if necessary. <!-- ACCS-398 -->

### Customize storefront authentication messages with structured error codes

The [`generateCustomerToken` GraphQL mutation](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} now returns typed error codes alongside error messages, enabling storefronts to display specific UI messages per failure reason. Available error codes include: `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED`, and `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Send automated email reminders for cart and wishlist inactivity

The [Email Reminder module](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) is now active in [!DNL Adobe Commerce as a Cloud Service], allowing merchants to create automated reminder rules that trigger emails to customers based on cart and wishlist inactivity. <!-- CCSAAS-4597 -->

### Subscribe to category deletion events webhook

The `observer.catalog_category_delete_before` webhook is now available in [!DNL Adobe Commerce as a Cloud Service]. Use it to run logic before a category is deleted. <!-- CEXT-5862 -->

### Track guest orders placed with a registered email

A new optional store-level configuration allows customers to [track guest orders](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails) they made, if the order was placed using an email address that matches a registered customer account. <!-- ACCS-289 -->

### Enhancements and bug fixes

The following selected enhancements, optimizations, and bug fixes are included in this release:

* Fixed an issue where some organization admins could incorrectly access tenant instances without per-tenant entitlement. <!-- ACCS-335 -->

* Fixed an issue that could log a user out of the [!DNL Commerce Admin] when making changes to a shared catalog. <!-- ACCS-318 -->

* Fixed an issue that caused some webhooks fields to display incorrectly in the [!DNL Commerce Admin] UI. <!-- CEXT-5874 -->

{{accs-release}}

>[!ENDSHADEBOX]

## February 2026 - release #2

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

The following items were released to Production environments of [!DNL Adobe Commerce as a Cloud Service] on February 24, 2026.

>[!BEGINSHADEBOX]

### Send context fields with commerce events

[!DNL Adobe Commerce as a Cloud Service] now supports [context fields](https://developer.adobe.com/commerce/extensibility/events/context-fields/) in event payloads, allowing you to include data that is not part of the event by default. <!-- CEXT-5713 -->

### Subscribe to quote item save events using a new webhook

The `observer.sales_quote_item_save_before` webhook is now available in [!DNL Adobe Commerce as a Cloud Service]. Use it to run logic before a quote item is saved. <!-- ACCS-346 -->

### Enhancements and bug fixes

The following selected enhancements, optimizations, and bug fixes are included in this release:

* Fixed an error that could cause display issues in the [!DNL Commerce Admin] product list. The product list now limits the number of shared catalogs displayed to improve performance. <!-- CCSAAS-1242 -->

* Fixed a GraphQL error that could prevent adding customizable gift cards to the cart. <!-- ACCS-313 -->

{{accs-release}}

>[!ENDSHADEBOX]

## February 2026 - release #1

[!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."}

The following items were released to Production environments of [!DNL Adobe Commerce as a Cloud Service] on February 10, 2026.

>[!BEGINSHADEBOX]

### Customize shipping methods and view Admin reports

The following enhancements were made to the [!DNL Commerce Admin]:

* Enhanced out-of-process [shipping webhook payloads](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) to include shipping address custom attributes. This change enables merchants to implement custom shipping methods. <!-- ACCS-235 -->

* Added access to Admin reports, including reports for [Customers](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports), [Marketing](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports), [Products](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports), and [Sales](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>Reports not available in [!DNL Adobe Commerce as a Cloud Service] are labeled as PaaS only ([!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}).

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

You can now combine tiered pricing discounts with catalog rule discounts using [catalog price rules](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). This enhancement allows you to create more dynamic and competitive pricing strategies, rewarding bulk purchases while applying promotional discounts at the same time. The result is greater flexibility to attract customers, increase order value, and drive conversions.<!-- See PR #708 in commerce-admin -->

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

* Added the ability to upload and retrieve negotiable quote attachments as well as files and images associated with customers and customer addresses to Amazon S3 using presigned URLs in [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) and [REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads). With REST, you can also upload category images. <!-- CCSAAS-3250 -->

* Added the `POST /V1/customers` and `PUT /V1/customers/{customerId}` endpoints to the [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) to create and update customers. These endpoints require IMS authorization. <!-- CCSAAS-3112 -->

* Added the [`exchangeOtpForCustomerToken` mutation](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), which requires a shopper's email address and one-time password (OTP), and receives a customer token in exchange. This mutation is typically used in scenarios where a customer needs to authenticate using an OTP sent to their email or phone.

* If an address defined in the [!UICONTROL **Store Email Addresses**] configuration screen in the Admin contains a value that ends with `example.com`, Commerce does not send emails to this address. Instead, the system logs that the email was not sent.  <!-- CCSAAS-3533 -->

#### Custom order attributes

* Admin users can now view and edit [custom order attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directly from the Order View, Edit, and Create screens in the Admin panel. This enhancement improves the management of custom order data created via GraphQL.  <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
