---
title: Onboarding [!DNL Payment Services] flow
description: Connect your instance with [!DNL Payment Services] functionality by completing a few onboarding steps.
role: User
level: Intermediate
exl-id: 1ee8c660-0941-4378-a1d7-ae45de3de211
feature: Payments, Checkout, Integration
---
# Onboarding [!DNL Payment Services] flow

To get started using [!DNL Payment Services], you must complete a few onboarding steps. For accurate guidance, please select the Adobe Commerce option below that best aligns with your organization's instance and version.

>[!BEGINSHADEBOX]

**Help me find my instance and version**

![Version](assets/which-version.png){width="500" zoomable="yes"}

>[!ENDSHADEBOX]

This flow diagram shows the general process for onboarding [!DNL Payment Services]:

![Onboarding flow](assets/flow-payment-services.png){width="700" zoomable="yes"}

See below for your specific Adobe Commerce version to onboard with [!DNL Payment Services].

## Adobe Commerce or Magento Open Source | v2.4.7+

>[!BEGINTABS]

>[!TAB Sandbox]

This flow diagram shows the general process for onboarding [!DNL Payment Services] with an Adobe Commerce or Magento Open Source newer than v2.4.7.

![Onboarding flow](assets/flow-sandbox-configuration-onboarding-2.4.7.png){width="700" zoomable="yes"}

[![learn more](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB Production]

This flow diagram shows the general process for onboarding [!DNL Payment Services] with an Adobe Commerce or Magento Open Source newer than v2.4.7.

![Onboarding flow](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

[![learn more](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

## Adobe Commerce or Magento Open Source | v2.4.0-2.4.6

>[!BEGINTABS]

>[!TAB Sandbox]

This flow diagram shows the general process for onboarding [!DNL Payment Services] with Adobe Commerce or Magento Open Source versions 2.4.0 to 2.4.6.

![Onboarding flow](assets/flow-sandbox-installation-configuration-onboarding-2.4.0.png){width="700" zoomable="yes"}

[![learn more](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB Production]

This flow diagram shows the general process for onboarding [!DNL Payment Services] with Adobe Commerce or Magento Open Source versions 2.4.0 to 2.4.6.

![Onboarding flow](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

[![learn more](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

>[!NOTE]
>
>If you do not configure your Commerce Services in the Admin (step 3), you cannot set up sandbox or live payments.

## Onboarding Part 1: Adobe Commerce or Magento Open Source | v2.4.7+ 

>[!BEGINTABS]

>[!TAB Step 1: Configure Services Connector]

### Step 1: Configure Services Connector

To connect your instance, you'll need to: 

1. Obtain production and sandbox API keys from the API Portal in your Magento account 

1. Add production and sandbox API keys to your Commerce dashboard 

1. Select a data space in the SaaS identifier tab

>[!NOTE]
>
> If you navigate to **System** > Services > **Commerce Services Connector** and there are values present in the API key fields, and the Project and Data Space fields in the SaaS Identifier section, then your instance is connected.

See our [[!DNL Adobe Commerce] Services Connector](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en) video for additional information.

* If you have *already connected your instance*, by obtaining and using your API credentials and configuring Commerce Services, you can proceed to [setting up your testing sandbox](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html).
* If you still *need to connect your instance*, see the information in this topic about [obtaining API credentials](#obtain-api-credentials) and [configuring Commerce Services](#configure-commerce-services).
* If you are *unsure whether your instance is connected*, navigate to **System** > Services > **Commerce Services Connector** and view the public and private API key values in the [!UICONTROL Sandbox Keys] and [!UICONTROL Production Keys] sections, and the *Project* and *Data Space* fields in the [!UICONTROL SaaS Identifier] section. If those values are present, then your instance is connected.

>[!NOTE]
>
> All merchants entitled for Payment Services can use one production data space and two testing data spaces.

**Continue to Step 2**

>[!TAB Step 2: Set up Sandbox environment]

### Step 2: Set up Sandbox Environment

To ensure that Admin users can create and manage orders in the Commerce Admin, enable [!DNL Payment Services]-specific resources to user roles.

See [User roles](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html) to learn how to manage roles.

When assigning resources to the role, you must select:

* **Pay with [!DNL Payment Services]**---This resource ensures that when you create an order in the Admin, [!DNL Payment Services] credit cards are available as a payment method. If you select the **Actions** parent resource, this resource will also be selected.
* **[!DNL Payment Services]**---This resource includes the **Dashboard** and **SaaS Services Proxy** resources, which must also be selected. They ensure that [!DNL Payment Services] appears in the _Sales_ menu.

   ![Payment Services resources](assets/roles-payments.png){width="400" zoomable="yes"}

To complete sandbox onboarding:

1. Navigate to the [PayPal Developer Account page](https://developer.paypal.com/developer/accounts/).
1. Click **[!UICONTROL Log in to Dashboard]** and log in with your existing PayPal Developer Portal-generated Business sandbox test account or click **Sign Up** to create an account.
1. Create a PayPal sandbox account:
   1. Go to _[!UICONTROL Testing Tools]_ > **[!UICONTROL Sandbox Accounts]**.
   1. Click **[!UICONTROL Create account]**.

      If you created an a PayPal sandbox account during the sandbox PayPal onboarding process, you must [reset your onboarding sandbox](#reset-your-sandbox-account) because or you cannot verify your email.

   1. Select **[!UICONTROL Business]** as the Account Type and click **[!UICONTROL Create]**.
   1. In the _[!UICONTROL Sandbox Accounts]_ section, click the three dots in the _[!UICONTROL Manage accounts]_ column for the sandbox account you created.
   1. Click **[!UICONTROL View/edit account]**.

      ![PayPal - View/edit sandbox account](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. Copy and save the Email ID and System-Generated Password for future use.

1. On the _Admin_ sidebar, go to **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Click **[!UICONTROL Sandbox onboarding]**.

   This option is visible if you have not yet completed sandbox onboarding for [!DNL Payment Services].

   A sandbox merchant ID is auto-generated and populated into [settings](settings.md). Do not change or alter this ID.

   You are presented with a PayPal window for connecting a PayPal account to start accepting payments.

1. Enter the email and password of the PayPal sandbox account you generated in step 3 (not your PayPal business account information) and your country or region.
1. Click **[!UICONTROL Next]**.

   ![PayPal - Connect PayPal account for payments](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. Continue to follow the PayPal flow, using your previously saved sandbox account credentials.
1. On the _Admin_ sidebar, go to **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

   The **[!UICONTROL Sandbox onboarding]** button is no longer visible and you see a "Sandbox payments pending" text.

  When your PayPal sandbox onboarding is approved, you should see a notification stating that your payment system is currently in sandbox mode and is not processing live payments.

   >[!IMPORTANT]
   >
   >If you revoke consent to [!DNL Payment Services] for [!DNL Adobe Commerce] and [!DNL Magento Open Source] for processing your payments (in your PayPal account settings), orders in your store cannot be processed by [!DNL Payment Services]. On your Payment Services home, an alert about the revoked consent appears. To dismiss the alert, click **[!UICONTROL Do not show again]**.

### Reset your sandbox account

If you created an a PayPal sandbox account during the sandbox PayPal onboarding process, you must reset your onboarding sandbox because or you cannot verify your email.

To reset your sandbox account:

1. Click **[!UICONTROL Reset sandbox]**. [Create a PayPal business sandbox account](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account).
1. Click **[!UICONTROL Sandbox onboarding]** and complete the next set of steps.

## Enable contact telephone number

Contact telephone number allows you to obtain the contact telephone numbers that PayPal collects from your customers. PayPal always collects contact telephone numbers from PayPal account holders to help confirm their identities and to contact them to resolve problems on their accounts, or to complete their fulfillment processes. However, PayPal discourages the use of contact phone numbers directly from the merchant because it can negatively impact sales. See the [PayPal get contact telephone numbers](https://www.sandbox.paypal.com/businessmanage/preferences/website) documentation for more information.

This feature is `off` by default. When you enable it, store administrators can see phone numbers when a customer completes a Branded Checkout flow outside of the checkout page.

>[!IMPORTANT]
>
>This setting does not apply to other checkout flows.

**Continue to Step 3**

>[!TAB Step 3: Enable Payment Services]

### Step 3: Enable Payment Services

>[!TAB Step 4: Test Sandbox environment]

>[!ENDTABS]