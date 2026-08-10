---
title: Connect a different PayPal account for a website
description: Complete website-scoped PayPal onboarding in the Admin to connect a different PayPal merchant account to an individual website.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
---
# Connect a different PayPal account for a website

For Commerce instances with **multiple websites**, you may need **different PayPal merchant accounts**. [!DNL Payment Services] enables **website-scoped** PayPal onboarding after **global** onboarding.

>[!NOTE]
>
> This feature currently supports connecting new accounts only.

## Prerequisites for website-scoped onboarding

Website-level onboarding is only available once your store meets these requirements:

- [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) setup is complete.
- A PayPal account is already connected at the global (Default Config) scope.

You can confirm this by checking that the following fields are populated at the default scope:

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

If these fields are empty, you must [complete global onboarding](configure-admin.md) first. The **[!UICONTROL Connect different account for website]** button remains disabled until this configuration is done.

## Start the website-level connection

1. On the _Admin_ sidebar, go to **[!UICONTROL Stores]** > _[!UICONTROL Settings]_ > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** and choose **[!UICONTROL Payment Methods]**.
1. In the scope selector in the upper-left corner, switch from **[!UICONTROL Default Config]** to the **[!UICONTROL Website]** you want to onboard.
1. Click **[!UICONTROL Connect different account for website]**.

    If the button is disabled, your store has not met the [prerequisites](#prerequisites-global-scope) above.

## Complete the onboarding modal

A popup window opens.

1. Select your **[!UICONTROL Country]** from the dropdown.
1. Choose your onboarding type: **[!UICONTROL Basic]** or **[!UICONTROL Advanced]**.
1. Click **[!UICONTROL Next]**.

>[!NOTE]
>
> If you are onboarding in Hungary, Spain, or Austria, you must open and view the Terms and Conditions link before the **[!UICONTROL I Accept]** button becomes clickable. The button stays disabled until the terms have been opened.

## Sign in to PayPal

You are redirected to the PayPal login flow. Sign in and complete the onboarding steps within PayPal.

>[!IMPORTANT]
>
> Once you click **[!UICONTROL Confirm and Continue]** during this step, your session for the global scope ends and the website-level connection begins. If you clicked **[!UICONTROL Connect different account for website]** by accident, you can cancel at this point by selecting **[!UICONTROL Cancel]** or the **X** in the corner before confirming.

## Finish and return to the Admin

1. After completing the PayPal steps, close the PayPal window.
1. Click **[!UICONTROL Finish]**, or the **X** in the top-right corner, to close the onboarding popup.
1. The Commerce configuration page refreshes automatically.

## Confirm the result

After the page refreshes, check the website scope configuration page for:

- An updated **[!UICONTROL PayPal Merchant ID]** for that website.
- A status label showing the result of onboarding:

| Status | Meaning |
| --- | --- |
| `ACTIVE` | Onboarding completed successfully |
| `PENDING` | Onboarding is still processing |
| `ERROR` | Onboarding did not complete successfully |

If you see an `ERROR` status, an error message is displayed explaining the issue. You can retry the onboarding process by clicking **[!UICONTROL Connect different account for website]** again.
