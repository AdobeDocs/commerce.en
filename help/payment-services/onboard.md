---
title: Onboard [!DNL Payment Services]
description: Connect your instance with [!DNL Payment Services] functionality by completing a few onboarding steps.
role: User
level: Intermediate
feature: Payments, Checkout, Integration
exl-id: 8d434a17-ecf4-4611-bbbf-88ec8c7baf3c
---
# Onboard [!DNL Payment Services]

To get started using [!DNL Payment Services] for [!DNL Adobe Commerce] and [!DNL Magento Open Source], you must complete a few onboarding steps for connecting your instance with the payments functionality.

## Onboarding flow

This flow diagram shows the general process for onboarding [!DNL Payment Services].

![Onboarding flow](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> For Adobe Commerce versions 2.4.7 or newer, you can skip the Marketplace extension step, as [!DNL Payment Services] is available out-of-the-box.

After you complete onboarding for sandbox or live payments, financial reporting is accessible from [!DNL Payment Services] in the Admin.

If both sandbox and live payments are onboarded and enabled, you can easily switch between those modes from the [!DNL Payment Services] Home.

## Prerequisites

In order to use [!DNL Payment Services], you must have  all dependent modules enabled and the following available for your instance:

* Services Connector module
* Services ID module
* API keys

The Services Connector and Services ID modules are automatically installed during the [installation of [!DNL Payment Services]](install.md).

When installation is complete, you can see a new section in the configuration settings (**[!UICONTROL Stores]** > _[!UICONTROL Settings]_ > **[!UICONTROL Configuration]**) if you expand **[!UICONTROL Services]**---**[!UICONTROL Commerce Services Connector]**.

To learn how to create or access your API keys, see [API credentials](#obtain-api-credentials).

## Onboarding steps

1. [Install the [!DNL Payment Services] extension](install.md#get-payment-services).
1. [Obtain API credentials](connect.md#obtain-api-credentials).
1. [Connect your instance](connect.md#configure-commerce-services) to Commerce Services. This connect must be completed only once per Commerce instance.
1. [Set up the sandbox service](sandbox.md#enable-sandbox-testing) (or, alternatively, proceed to [enabling live payments](sandbox.md#enable-live-payments) if you've tested functionality in another environment) with a test PayPal payment processing account.
1. [Set [!DNL Payment Services] as your payment method](production.md#set-payment-services-as-payment-method), in sandbox mode, to start processing test payments.
1. [Request payments entitlement](production.md#request-payments-entitlement-from-adobe) to enable live onboarding.
1. [Complete merchant onboarding](production.md#complete-merchant-onboarding) to enable live payments for your Commerce websites.
1. [Get your [!DNL Payment Services] Merchant ID](production.md#configure-pricing-tier) and hand it to Sales to configure the correct pricing tier.
1. [Enable [!DNL Payment Services] in live mode](production.md#enable-live-payments) to begin processing live payments.
1. Test Payments, in both [sandbox](sandbox.md#test-in-sandbox-environment) and [production](production.md#test-in-production) environments.

>[!NOTE]
>
>If you do not configure your Commerce Services in the Admin (step 3), you cannot set up sandbox or live payments.

## Troubleshooting

* [Troubleshoot [!DNL Payment Services] installation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [PayPal sandbox account not verified](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [Delayed [!DNL Payment Services] report data](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
* [Test credit card fails with PayPal when processing payments in a Sandbox environment](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
