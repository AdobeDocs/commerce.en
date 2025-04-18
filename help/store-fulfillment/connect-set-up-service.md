---
title: Connect the Store Fulfillment Solution
description: Establish the connections between Adobe Commerce and the Store Fulfillment solution. Create and authorize an Adobe Commerce integration, and add the Store Fulfillment account credentials to the Adobe Commerce service configuration.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
exl-id: 07409650-6f24-4b4c-942a-a97fefdcab28
---
# Connect the Store Fulfillment Solution

Connect Store Fulfillment Services with Adobe Commerce by adding the required authentication credentials and connection data to the Adobe Commerce Admin.

- **[Configure [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)**–Create an Adobe Commerce integration for Store Fulfillment services and generate the access tokens to authenticate incoming requests from the Store Fulfillment servers.

- **[Configure account credentials for Store Fulfillment Services](#configure-store-fulfillment-account-credentials)**–Add your credentials to connect Adobe Commerce to your Store Fulfillment account.

>[!NOTE]
>
>Complete the connection configuration and validate the connection successfully before you begin testing.

## Create an Adobe Commerce integration

To integrate Adobe Commerce with Store Fulfillment services, you create a Commerce integration and generate access tokens that can be used to authenticate requests from Store Fulfillment servers. You must also update the Adobe Commerce [!UICONTROL Consumer Settings] options to prevent `The consumer isn't authorized to access %resources.` response errors on requests from Adobe Commerce to [!DNL Store Fulfillment] services.

1. From the Admin, create the Integration for Store Fulfillment.

   - Name the extension
   - Enter your email address
   - Enter your Admin account password

1. Configure API Resource Access permissions for the integration with the following:

   - Sales > BOPIS Order update
   - System > Store Fulfillment App Permissions

1. Generate the access tokens for authentication by saving and activating the integration.

1. Copy and save the access tokens to a secure, encrypted location.

1. Work with your Account Manager to complete the configuration on the Store Fulfillment side and to authorize the integration.

1. Enable the Adobe Commerce [!UICONTROL Consumer Settings] option to [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens].

   - From the Admin, go to **[!UICONTROL Stores]** >  [!UICONTROL Configuration] > **[!UICONTROL Services]** >  **[!UICONTROL OAuth]** > **[!UICONTROL Consumer Settings]**

   - Set the [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] option to **[!UICONTROL Yes]**.

>[!IMPORTANT]
>
> The integration token is environment specific. If you restore the database for an environment with the source data from a different environment—for example restoring production data from a staging environment—exclude the `oauth_token` table from the database export so that the integration token details are not overwritten during the restore operation.


## Configure Store Fulfillment account credentials

After you complete the intake form, a Walmart Store Fulfillment account is created for you. You receive the following credentials when they are available:

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL] (usually the same as above configuration)

These credentials are required to configure and use Store Fulfillment.

  >[!NOTE]
  >
  >The account creation process can take some time to complete. While you wait for credentials, [review and configure other settings for the  Store Fulfillment solution](service-config-settings-overview.md).

### Add credentials to connect to Store Fulfillment

1. Configure [account credentials](enable-general.md) for the Production and Sandbox environments.

1. From the Admin, go to **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**

1. Enter the account credentials provided for the **[!UICONTROL Production environment]**. All fields are required.

1. Select **[!UICONTROL Save Config]**.

1. Test the connection by selecting **[!UICONTROL Validate Credentials]**.

>[!NOTE]
>
>If the credentials are invalid, verify that you entered the correct values for each environment and revalidate. Contact your account representative if you still have problems connecting.
