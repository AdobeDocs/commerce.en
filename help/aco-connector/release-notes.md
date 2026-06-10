---
title: '[!DNL Adobe Commerce Optimizer Connector] Release Notes'
description: Learn about [!DNL Adobe Commerce Optimizer Connector] release notes, including new features, bug fixes, and known issues for catalog synchronization and export.
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Adobe Commerce Optimizer Connector release notes

These release notes describe all releases for the [!DNL Adobe Commerce Optimizer Connector] and include:

![New](../assets/new.svg) New features
![Fixed issue](../assets/fix.svg) Fixes and improvements
![Known issue](../assets/bug.svg) Known issues

## 2026 Releases

### 1.0.13 Release

_May 6, 2026_

![Fix](../assets/fix.svg) **Improved [!DNL Adobe Commerce Optimizer Connector] configuration instructions** – Updated the [!DNL Adobe Commerce Optimizer] configuration page in the Commerce Admin to link to the _[!DNL Adobe Commerce Optimizer Connector] Integration Guide_.
<!--COMOPT-1922-->

![Fix](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector] metadata enhancement** – The [!DNL Adobe Commerce Optimizer Connector] now includes its installed version in the metadata header. This improvement enables teams to quickly identify which connector version is in use during troubleshooting or support engagements.<!--MDEE-1323-->

### 1.0.12 Release

_April 2, 2026_

![New](../assets/new.svg) **Added support for the Categories feed in `saas:resync` command**–You can now easily refresh and view your latest category data using the `saas:resync` CLI command:

```terminal
bin/magento saas:resync --feed=categories
```

### 1.0.11 Release

_March 10, 2026_

![Fixed issue](../assets/fix.svg) Fixed a compatibility issue that blocked access to the [!DNL Commerce Services Connector] configuration page from the Commerce Admin **[!UICONTROL System]** and **[!UICONTROL Configuration]** menus when the [!DNL Adobe Commerce Optimizer Connector] is installed on a [!DNL Adobe Commerce] instance.  Now, you can access the [!DNL Commerce Services Connector] configuration page when both extensions are installed. <!--MDEE-1322-->


### 1.0.10 Release

_March 09, 2026_

![Fix](../assets/fix.svg) If you access the **[!UICONTROL Data Feed Sync Status]** page before completing the connector configuration, you are now automatically redirected to the connector configuration page. This guided flow ensures that the connector setup is completed and helps prevent errors caused by missing configuration settings that could result in failed or incomplete status items.<!--MDEE-1296-->

### v1.0.9 Release

_March 01, 2026_

General availability release of the [!DNL Adobe Commerce Optimizer Connector].

>[!NOTE]
>
>If you participated in the Beta program for the [!DNL Adobe Commerce Optimizer Connector] and have an earlier version of the extension installed, upgrade to the General availability version to receive the latest updates.
