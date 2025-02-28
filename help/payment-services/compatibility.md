---
title: Compatibility for [!DNL Payment Services]
description: Learn if [!DNL Payment Services] is available in your country, and its compability with your Adobe Commerce version.
role: User
level: Intermediate
feature: Payments, Checkout
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

| Standard (Express Checkout) | Advanced (Fully Supported) |
| ------------ | -------------------- |
| PayPal Checkout<br>PayPal Debit or Credit card button<br>Custom checkout configurations<br>Standard pricing <br><br>**Available in XX countries** | Debit card<br>PayPal credit<br>Credit Card Fields<br>Apple Pay button<br>Google Pay button<br>PayPal Payment buttons<br>PayPal button<br>Venmo button<br>PayPal Debit or Credit card button<br>Pay Later Button<br>Custom checkout configurations<br>Customized pricing<br>(L2/L3 pricing capabilities – US Only)<br>FPA <br><br>**Only available in United States (US), Canada (CA), Australia (AUS). France (FR), United Kingdom (UK)** |

{style="table-layout:auto"}

>[!TIP]
>
> See [Lifecycle policy](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html) and the [[!DNL Payment Services] release notes](release-notes.md) pages for more release and version-specific information.

To get the full instructions and start the onboarding process, see [Get Started with [!DNL Payment Services]](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/get-started/onboard). 

## Payment methods

[!DNL Payment Services] accepts the currencies of the countries [in which it is available](#availability). See [Currency configuration](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html) for more information on setting up currency rates.

### Accepted credit cards and currencies

For more information on the currencies and payment methods available with PayPal products and services, refer to the following: 

* [Supported currencies documentation](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Payment methods documentation](https://developer.paypal.com/docs/checkout/payment-methods/).

>[!MORELIKETHIS]
>
> * [Troubleshoot [!DNL Payment Services] installation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
> * [PayPal sandbox account not verified](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
> * [Delayed [!DNL Payment Services] report data](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
> * [Test credit card fails with PayPal when processing payments in a Sandbox environment](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)

#### [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] provide a simple and secure checkout for credit card, or debit card, payment methods. To complete an order, shoppers enter their name, billing address, and card details, which are securely processed to ensure a smooth checkout experience.

![Credit card fields in checkout](assets/credit-card-fields.png){width="500" zoomable="yes"}

#### [!UICONTROL Digital Wallets]

##### [!DNL Apple Pay] button

With [[!DNL Apple Pay]](https://www.apple.com/apple-pay/), merchants can provide a secure, streamlined checkout experience in Safari (for up to 99 domains per merchant account), which can increase conversions. The [!DNL Apple Pay] button autofill uses credit and debit card payment credentials stored on an iOS or macOS device, to make purchases.

![Apple Pay button in the minicart](assets/applepay-button.png){width="500" zoomable="yes"}

The [!DNL Apple Pay] button is visible from the product page, mini-cart, shopping cart, and checkout views.

To use [!DNL Apple Pay] for your stores, complete [self-registration with [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Register your live domain_ section only) and [configure it for your stores in [!DNL Payment Services]](settings.md#payment-buttons).

   >[!NOTE]
   >
   > See [advanced checkout](https://www.paypal.com/us/cshelp/article/what-is-paypal-advanced-checkout-and-how-do-i-get-started-help953){target=_blank} in the PayPal developer documentation to check how to enable enable buyers to pay with Apple Pay on your site.

You can configure [!UICONTROL Apple Pay] in the store configuration or the Payment Services Home. See [Settings](settings.md#apple-pay) for more information.

##### [!DNL Google Pay] button

By integrating [[!DNL Google Pay]](https://pay.google.com/about/) into your checkout experience, merchants can collect saved payment, contact, and shipping information from the shopper's Google Account, offering a convenient, streamlined checkout across supported browsers and apps. 

[!DNL Google Pay] is only available in certain countries or regions and on certain devices. See [[!DNL Google Pay] documentation](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration) for more information.

![Google Pay button in the checkout](assets/google-pay-button.png){width="500" zoomable="yes"}

When enabled, the [!DNL Google Pay] button is visible from the product page, mini-cart, shopping cart, and checkout views.

You can configure [!UICONTROL Google Pay] in the store configuration or the Payment Services Home. See [Settings](configure-admin.md) for more information.

   >[!NOTE]
   >
   > The [!DNL Google Pay] API can only be used on websites in a secure context. See [Troubleshooting](https://developers.google.com/pay/api/web/support/troubleshooting) documentation for more information.

##### [!DNL PayPal Payment] buttons

Merchants can use [!DNL PayPal Payment] buttons to facilitate purchases by securely accessing payment information stored on PayPal. Customers can choose from previously saved payments or enter in new payment details. New billing and shipping information will be safely stored for future transactions. 

![PayPal button](assets/paypal-button.png){width="350" zoomable="yes"}

You can configure [!UICONTROL PayPal payment] buttons in the store configuration or the [!DNL Payment Services] Home. See [Settings](settings.md#payment-buttons) for more information.

* [!DNL PayPal] button

   Customers can check out with ease and confidence using the PayPal button.

   The [!DNL PayPal] button is visible from the product page, mini-cart, shopping cart, and checkout views.

* [!DNL Venmo] button

   Customers can check out using the [Venmo](https://venmo.com/) button.

   The [!DNL Venmo] button is visible from the product page, mini-cart, shopping cart, and checkout views.

* PayPal Debit or Credit card button

   Customers can check out using the PayPal Debit or Credit card button.

   The PayPal Debit or Credit card button is visible from the checkout page.

   This option can be used to present a debit or credit card payment option to your shoppers with a PayPal-hosted button as an alternative to a credit card integration.

* [!DNL Pay Later] button

   Offer your customers short-term, interest-free payments, and other financing options so that they can buy now and pay later with the [!DNL Pay Later] button.

   The [!DNL Pay Later] button is visible from the product page, mini-cart, shopping cart, and checkout views.

   See information about the Pay Later offers in [PayPal's Pay Later offers documentation](https://developer.paypal.com/docs/checkout/pay-later/us/). Use the **Country or region** dropdown to select a region of interest.

   Learn how to disable or enable the [!DNL Pay Later] messaging by updating the [Settings](settings.md#payment-buttons) configuration.

Learn about availability of payment methods by country in PayPal's [Payment methods documentation](https://developer.paypal.com/docs/checkout/payment-methods/).

## Checkout Options

With [!DNL Payment Services], you can configure the checkout experience for Adobe Commerce to best suit your shoppers' preferences and behaviors. Features such as credit card [vaulting](vaulting.md) and order auto-voiding ensure a seamless, hassle-free transaction for your customers. 

With Adobe Commerce and Magento Open Source [!DNL Payment Services], you have multiple checkout experiences available to you. There are different behaviors for each payment method depending on where you are in the checkout process: 

* Product page—--The product page for an item 

* Mini cart—--Available upon click of the cart icon when a product has been added to the carts 

* Shopping cart--—Available upon click of View and edit cart from the mini-cart 

* Checkout view—--Available upon click of Proceed to Checkout from mini-cart or shopping cart 
