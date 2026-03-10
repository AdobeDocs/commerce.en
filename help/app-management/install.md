---
title: "Install and access [!DNL App Management]"
description: "Prerequisites and access requirements for using Adobe Commerce [!DNL App Management]."
feature: App Builder, Extensibility, Integration
---
# Install and access [!DNL App Management]

[!DNL App Management] is available in the Commerce Admin for eligible Commerce instances. Availability depends on your deployment type.

## Availability

After meeting the following requirements, select the corresponding tab for your deployment type below, to see whether [!DNL App Management] requires installation or is already available on your instance.

## Prerequisites

Before associating an app, ensure you have the following:

| Requirement | Description |
|-------------|-------------|
| **Admin access** | Commerce Admin with [!DNL App Management] permissions |
| **Deployed app** | App Builder application deployed to your organization and ready to connect |
| **Organization access** | Access to the Adobe organization where the app is deployed |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management] is available automatically on [!DNL Adobe Commerce as a Cloud Service]. No installation is required. [Enable it in the Admin](#access-app-management) and start associating apps.

>[!TAB Adobe Commerce on Cloud (PaaS) and on-premises]

* **Adobe Commerce 2.4.8 and later**—[!DNL App Management] is included automatically. No installation is required.

* **Adobe Commerce 2.4.5 to 2.4.7**—Install the [!DNL Admin UI SDK] (which includes [!DNL App Management]) using Composer:

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  Then run:

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

 See [Install or update Adobe Commerce Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"} for more information.

>[!ENDTABS]

## Access [!DNL App Management]

1. Log in to the Commerce Admin.

1. Navigate to **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

The [!DNL App Management] view displays. Here, you can associate, configure, and manage App Builder applications.

## Installing App Builder apps

If you need to install an App Builder app from Adobe Exchange (for example, a pre-built integration or marketplace app), see [Install App Builder apps from Adobe Exchange](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} for step-by-step instructions.

After an app is installed and deployed, use [!DNL App Management] to [associate it with your Commerce instance](manage-app.md#associate-an-app) and configure its settings.
