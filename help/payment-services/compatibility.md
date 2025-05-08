---
title: Compatibility for [!DNL Payment Services]
description: Learn if [!DNL Payment Services] is available in your country, and its compability with your Adobe Commerce version.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
exl-id: 4bef8429-5053-424d-806a-9e8b96295b1b
---
# Compatibility for [!DNL Payment Services]

[!DNL Payment Services] is available for Adobe Commerce and Magento Open Source. [!DNL Payment Services] is now compatible with Adobe Commerce versions 2.4.x.

## Prerequisites

To use [!DNL Payment Services], you'll need to first connect your Commerce instance. **You set up this connection only once**.

1. If you are unsure whether your instance is connected, navigate to **System** > Services > **Commerce Services Connector** and view the public and private API key values in the Sandbox Keys and Production Keys sections, and the Project and Data Space fields in the SaaS Identifier section. If those values are present, then your instance is connected.
   
1. If you still need to connect your instance, view the instructions on the [Commerce Services Connector](../landing/saas.md) page. 
   
   >[!TIP]
   >
   > See our [Adobe Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) tutorial video for additional information.

1. If you have already connected your instance, navigate to the [onboarding](onboard.md) page for next steps.

>[!IMPORTANT]
>
> All merchants entitled for [!DNL Payment Services] can use **one production data space** and **two testing data spaces**.

## Standard vs. Advanced [!DNL Payment Services] Experience 

[!DNL Payment Services] provides **Standard** (Express Checkout) and **Advanced** (fully supported) payment options and onboarding flows, depending on the country in which you operate. 

>[!NOTE]
>
> [!DNL Payment Services] provides [Express Checkout capabilities](../payment-services/payments-options.md) (subset of payments options) for other [available countries during onboarding](../payment-services/production.md#complete-merchant-onboarding).

### Which [!DNL Payment Services] option is right for you?

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

See [Connect](connect.md) for more information on setting up your [!DNL Payment Services] extension.

>[!BEGINTABS]

>[!TAB Standard (Express Checkout)]

![check](assets/icon-check.png)  PayPal Checkout

![check](assets/icon-check.png)  PayPal Debit or Credit card button

![check](assets/icon-check.png)  Custom checkout configurations

![check](assets/icon-check.png)  Standard pricing

![check](assets/icon-check.png)  **Available in XX countries**

[![learn more](assets/learn-more-button.svg)](onboard.md)

>[!TAB Advanced (Fully Supported)]

![check](assets/icon-check.png)  Debit card

![check](assets/icon-check.png)  PayPal credit

![check](assets/icon-check.png)  Credit Card Fields

![check](assets/icon-check.png)  Apple Pay button

![check](assets/icon-check.png)  Google Pay button

![check](assets/icon-check.png)  PayPal Payment buttons

![check](assets/icon-check.png)  Venmo button

![check](assets/icon-check.png)  PayPal Debit or Credit card button

![check](assets/icon-check.png)  Pay Later Button

![check](assets/icon-check.png)  Custom checkout configurations

![check](assets/icon-check.png)  Customized pricing

![check](assets/icon-check.png)  (L2/L3 pricing capabilities – US Only)

![check](assets/icon-check.png)  **Only available in United States (US), Canada (CA), Australia (AUS). France (FR), United Kingdom (UK)**

[![learn more](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

See the [Lifecycle policy](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html) and the [[!DNL Payment Services] release notes](release-notes.md) pages for more release and version-specific information.

To get the full instructions and start the onboarding process, see [Get Started with [!DNL Payment Services]](onboard.md). 

### Accepted credit cards and currencies

[!DNL Payment Services] accepts the currencies of the countries [in which it is available](#availability). See [Currency configuration](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html) for more information on setting up currency rates.

For more information on the currencies and payment methods available with PayPal products and services, refer to the following pages: 

* [Supported currencies documentation](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Payment methods documentation](https://developer.paypal.com/docs/checkout/payment-methods/).
