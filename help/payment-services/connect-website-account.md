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
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Connect a different PayPal account for a website

For Commerce instances with **multiple websites**, you may need **different PayPal merchant accounts**. [!DNL Payment Services] enables **website-scoped** PayPal onboarding after **global** onboarding.

>[!NOTE]
>
> This feature only supports connecting new accounts.

## Prerequisites for website-scoped onboarding

Website-level onboarding is only available once your store meets these requirements:

- [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) setup is complete.
- A PayPal account is connected at the global (Default Config) scope.

You can confirm this by checking that the following fields are populated at the default scope:

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

If these fields are empty, you must [complete global onboarding](configure-admin.md) first. The **[!UICONTROL Connect different account]** button is disabled until you complete the prerequisites.

## Start the website-level connection

1. On the _Admin_ sidebar, go to **[!UICONTROL Stores]** > _[!UICONTROL Settings]_ > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** and choose **[!UICONTROL Payment Methods]**.
1. In the scope selector in the upper-left corner, switch from **[!UICONTROL Default Config]** to the **[!UICONTROL Website]** you want to onboard.
1. Click **[!UICONTROL Connect different account]**.

    If the button is disabled, your store has not met the [prerequisites](#prerequisites-global-scope) above.

## Complete the onboarding modal

A popup window opens.

1. Select your **[!UICONTROL Country]** from the dropdown.
1. Choose your onboarding type: **[!UICONTROL Basic]** or **[!UICONTROL Advanced]**.
1. Click **[!UICONTROL Next]**.

>[!NOTE]
>
> If you are onboarding in Hungary, Spain, or Austria, you must open and view the Terms and Conditions link before you can click the **[!UICONTROL I Accept]** button. The button is disabled until you open the Terms and Conditions.

## Sign in to PayPal

After you are redirected to the PayPal login, sign in and complete the onboarding steps within PayPal.

>[!IMPORTANT]
>
> Once you click **[!UICONTROL Confirm and Continue]**, your session for the global scope ends and the website-level connection begins. If you accidentally clicked **[!UICONTROL Connect different account]**, you can cancel by selecting **[!UICONTROL Cancel]** or clicking the **X** icon before confirming.

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

If you see an `ERROR` status, an error message displays that explains the issue. You can retry the onboarding process by clicking **[!UICONTROL Connect different account]** again.
