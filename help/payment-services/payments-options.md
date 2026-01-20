---
title: Payment Options
description: Set the payment options to customize the methods available for your store customers.
exl-id: 95e648e6-6cb8-4226-b5ea-e1857212f20a
feature: Payments, Checkout, Configuration, Paas, Saas
---
# Payment Options

With [!DNL Adobe Commerce] and [!DNL Magento Open Source] [!DNL Payment Services], you have multiple payment options available to you.

You can configure these payment options in [Home settings](payments-home.md) or [Store configuration](configure-admin.md) (recommended for legacy payment options or a multi-store setup).

There are different behaviors for each payment method depending on where you are in the checkout process:

* Product page---The product page for an item
* Mini cart---Available upon click of the cart icon when a product has been added to the carts
* Shopping cart---Available upon click of _View and edit cart_ from the mini-cart
* Checkout view---Available upon click of _Proceed to Checkout_ from mini-cart or shopping cart

>[!IMPORTANT]
>
>[!DNL Payment Services] onboarding must be completed before payments can be processed.

## Standard vs. Advanced Payments Experience

[!DNL Payment Services] provides **Advanced** (fully supported) and **Standard** (Express Checkout) payment options and onboarding flows, depending on the country in which you operate.

* **Advanced** - All available [payments options](../payment-services/payments-options.md) are available for current [fully supported countries](../payment-services/introduction.md#availability). During onboarding to enable live payments, select the [Advanced onboarding option](../payment-services/production.md#advanced-onboarding).

* **Standard** - A subset of payments options (Express Checkout)---PayPal credit and debit cards---is available for other available supported countries. [Credit card fields](#credit-card-fields) and [Apple Pay](#apple-pay-button) are not available for this onboarding option. During onboarding to enable live payments, select the [Standard onboarding option](../payment-services/production.md#standard-onboarding).

See [Enable [!DNL Payment Services] for production](../payment-services/production.md#complete-merchant-onboarding) for information about completing Advanced and Standard onboarding.

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] provide a simple and secure checkout for credit card or debit card payment methods. When a shopper checks out using credit card fields, they enter their name, billing address, and credit or debit card information to place their order. Their customer information is securely used during the purchase session to seamlessly guide them through the checkout flow.

![Credit card fields in checkout](assets/credit-card-fields.png){width="500" zoomable="yes"}

## [!UICONTROL Digital Wallets]

### [!DNL Fastlane] button 

[!DNL Fastlane] offers a quick, secure, and hassle-free way to pay online. During a **Guest checkout**, you can securely store your card and shipping details for even faster purchases in the future.

* **Instant access for verified shoppers**: Recognize millions of returning customers and enable seamless payments in seconds.
* **Boost revenue**: Enhance conversion and authorization rates with more completed purchases.
* **Accelerate checkout**: Reduce friction with a secure, passwordless login experience.

When [!DNL Fastlane] is enabled, the [!UICONTROL Credit Card Fields] option is disabled by default.

>[!NOTE]
>
> In sandbox instances, Fastlane transactions do not show the shipping address in the Transaction Activity view.

See [Fastlane by PayPal](https://www.paypal.com/us/fastlane){target=_blank} topic for more information.

### [!DNL Apple Pay] button

With [!DNL Apple Pay], merchants can provide a secure, streamlined checkout experience in Safari (for up to 99 domains per merchant account), which can increase conversions. The [!DNL Apple Pay] button autofill's stored payment, contact, and shipping details from customers' iOS or macOS devices, enabling a quick, one-tap checkout experience.

![Apple Pay button in the minicart](assets/applepay-button.png){width="500" zoomable="yes"}

When enabled, the [!DNL Apple Pay] button is visible from the product page, mini-cart, shopping cart, and checkout views. You can configure [!DNL Apple Pay] in the store configuration or the extension's Home.

>[!NOTE]
>
>  The Apple Pay domain verification certificate is already included into the Payment Services code. Verify that the path `/.well-known/apple-developer-merchantid-domain-association` returns a 200 response code. See [PayPal developer documentation about Integrating with Apple Pay](https://developer.paypal.com/docs/checkout/apm/apple-pay/#download-and-host-sandbox-domain-association-file) for more information about the **Apple Pay Domain verification** certificate.

See [Settings](configure-admin.md#apple-pay) for more information.

### [!DNL Google Pay] button

By integrating [!DNL Google Pay] into your checkout experience, merchants can collect saved payment, contact, and shipping information from the shopper's Google Account, offering a convenient, streamlined checkout across supported browsers and apps.

[!DNL Google Pay] is only available in certain countries or regions and on certain devices. See [[!DNL Google Pay] documentation](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration) for more information.

![Google Pay button in the checkout](assets/google-pay-button.png){width="500" zoomable="yes"}

When enabled, the [!DNL Google Pay] button is visible from the product page, mini-cart, shopping cart, and checkout views. See [Settings](configure-admin.md) for more information.

   >[!NOTE]
   >
   > The [!DNL Google Pay] API can only be used on websites in a secure context. See [Troubleshooting](https://developers.google.com/pay/api/web/support/troubleshooting) documentation for more information.

### [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons], which use PayPal to complete a purchase, stores your shopper's shipping address, billing addresses, and payment details for later use. Shoppers can use any payment method previously stored or offered by PayPal.

![PayPal button](assets/paypal-button.png){width="350" zoomable="yes"}

You can configure [!UICONTROL PayPal payment buttons] in the store configuration or the [!DNL Payment Services] Home.

Learn about availability of payment methods by country in PayPal's [Payment methods documentation](https://developer.paypal.com/docs/checkout/payment-methods/).

#### [!DNL PayPal] button

Customers can check out with ease and confidence using the PayPal button.

The [!DNL PayPal] button is visible from the product page, mini-cart, shopping cart, and checkout views.

#### [!DNL Venmo] button

Customers can check out using the [Venmo](https://venmo.com/) button.

The [!DNL Venmo] button is visible from the product page, mini-cart, shopping cart, and checkout views.

#### PayPal Debit or Credit card button

Customers can check out using the PayPal Debit or Credit card button.

The PayPal Debit or Credit card button is visible from the checkout page.

This option can be used to present a debit or credit card payment option to your shoppers with a PayPal-hosted button as an alternative to a credit card integration.

#### [!DNL Pay Later] button

Offer your customers short-term, interest-free payments, and other financing options so that they can buy now and pay later with the [!DNL Pay Later] button.

The [!DNL Pay Later] button is visible from the product page, mini-cart, shopping cart, and checkout views.

See information about the [Pay Later offers](https://developer.paypal.com/docs/checkout/pay-later/us/) in the PayPal Developer documentation. Use the **Country or region** dropdown to select a region of interest.

Learn how to disable or enable the [!DNL Pay Later] messaging by updating the [Settings](configure-admin.md#pay-later-button) configuration.

##### Optional. Configure Pay Later Messaging

**Configure messaging** for [Pay Later](configure-admin.md#pay-later-button) allows merchants to modify the default styles for this payment option. If you set **[!UICONTROL Display Pay Later Message]** to `Yes` in your [Settings](configure-admin.md#pay-later-button) configuration, a **[!UICONTROL Configure Messaging]** modal button is displayed so you can set the styles for the **[!UICONTROL PayPal Pay Later messaging]**.

![Pay Later Messaging](assets/pay-later-messaging.png){width="500" zoomable="yes"}

### Use only PayPal payment buttons

To quickly get your store into production mode, you can configure _only_ PayPal payment buttons (Venmo, PayPal, and so on.)---instead of also using the PayPal credit card payment option.

This allows you to:

* Provide various payment options for your customers, including Venmo and PayPal payment buttons, with the option to turn off PayPal hosted card fields and use an existing credit card provider.
* Use your existing credit card provider for credit card payments, while also using PayPal's other payment options.
* Use PayPal's payment buttons in regions where PayPal does not support credit cards as a payment option.

To **capture payments with _only_ PayPal payment buttons (_not_ the PayPal credit card payment option)**:

1. Ensure that your store is [in production mode](configure-admin.md#enable-payment-services).
1. [Configure the desired PayPal payment buttons](configure-admin.md#payment-buttons) in Settings.
1. Turn _Off_ the **[[!UICONTROL Show PayPal Credit and Debit card button]](configure-admin.md#payment-buttons)** option in the _[!UICONTROL Payment buttons]_ section.

To **capture payments with your existing credit card provider _and_ PayPal payment buttons**:

1. Ensure that your store is [in production mode](configure-admin.md#enable-payment-services).
1. [Configure the desired PayPal payment buttons](configure-admin.md#payment-buttons).
1. Turn _Off_ the **[[!UICONTROL PayPal Show Credit and Debit card button]](configure-admin.md#payment-buttons)** option in the _[!UICONTROL Payment buttons]_ section.
1. Turn _Off_ the **[[!UICONTROL Show on checkout page]](configure-admin.md#credit-card-fields)** option in the _[!UICONTROL Credit card fields]_ section and use your [existing credit card provider account](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html#payments).

## Checkout Options

With [!DNL Payment Services], you can configure the checkout experience for Adobe Commerce to best suit your shoppers' preferences and behaviors. Features such as credit card [vaulting](vaulting.md) and order auto-voiding ensure a seamless, hassle-free transaction for your customers. 

With Adobe Commerce and Magento Open Source [!DNL Payment Services], you have multiple checkout experiences available to you. There are different behaviors for each payment method depending on where you are in the checkout process: 

* Product page—--The product page for an item 

* Mini cart—--Available upon click of the cart icon when a product has been added to the carts 

* Shopping cart--—Available upon click of View and edit cart from the mini-cart 

* Checkout view—--Available upon click of Proceed to Checkout from mini-cart or shopping cart 

### Order recalculation

When a customer enters the checkout flow from the mini-cart, shopping cart, or product page, they are directed to an order review page where they can see the selected shipping address in a PayPal popup window. After the customer selects the shipping method, the order amount is recalculated appropriately and the customer can see shipping costs and taxes.

When a customer enters the checkout flow from the checkout page, the system is already aware of the shipping address and final calculated amount, and totals are appropriately represented.

Tax holidays, shipping costs, and sales tax can vary widely from location to location. After [!DNL Payment Services] receives the shipping address and rate, it quickly recalculates all applicable costs and display them appropriately during the last stages of checkout.

Learn about availability of payment methods by country in [PayPal's Payment methods](https://developer.paypal.com/docs/checkout/payment-methods/){target=_blank} documentation.
