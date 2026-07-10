---
title: '[!DNL Adobe Commerce Optimizer Connector] Release Notes'
description: Learn about [!DNL Adobe Commerce Optimizer Connector] release notes, including new features, bug fixes, and known issues for catalog synchronization and export.
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
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
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Adobe Commerce Optimizer Connector release notes

These release notes describe all releases for the [!DNL Adobe Commerce Optimizer Connector] and include:

![New](../assets/new.svg) New features
![Fixed issue](../assets/fix.svg) Fixes and improvements
![Known issue](../assets/bug.svg) Known issues

## 2026 Releases

### 1.0.15 Release

_July 10, 2026_

![Fix](../assets/fix.svg) fix tests. <!--MDEE-1397-->
![Fix](../assets/fix.svg) ACO test SaasExportAdapter\FeedSubmitTest hangs in Jenkins. <!--MDEE-1406-->
![Fix](../assets/fix.svg) Sorting support for Categories API. <!--MDEE-1409-->

### 1.0.14 Release

_June 11, 2026_

![Fix](../assets/fix.svg) **PHP 8.5 compatibility** – The [!DNL Adobe Commerce Optimizer Connector] now supports PHP 8.5, so you can upgrade your [!DNL Adobe Commerce] environment without disrupting connector functionality or catalog synchronization. <!--MDEE-1388-->

![Fix](../assets/fix.svg) **Price books update after currency changes** – Updated prices are automatically reflected in Adobe Commerce Optimizer after currency changes.. <!--MDEE-1384-->

![Fix](../assets/fix.svg) **Navigation respects disabled or hidden parent categories** – Products from disabled or hidden category hierarchies no longer appear unexpectedly in navigation experiences.<!--MDEE-1385-->

![Fix](../assets/fix.svg) **Consistent category URLs after staging updates** – Category links and navigation remain accurate after staging updates are applied. <!--MDEE-1395-->

### 1.0.13 Release

_May 6, 2026_

![Fix](../assets/fix.svg) **Improved [!DNL Adobe Commerce Optimizer Connector] configuration instructions** – Updated the [!DNL Adobe Commerce Optimizer] configuration page in the Commerce Admin to link to the _[!DNL Adobe Commerce Optimizer Connector] Integration Guide_.
<!--COMOPT-1922-->

![Fix](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector] metadata enhancement** – The [!DNL Adobe Commerce Optimizer Connector] now includes its installed version in the metadata header. This improvement enables teams to quickly identify which connector version is in use during troubleshooting or support engagements.<!--MDEE-1323-->

### 1.0.12 Release

_April 2, 2026_

![New](../assets/new.svg) **Added support for the Categories feed in `saas:resync` command**–You can now easily refresh and view your latest category data using the `saas:resync` CLI command:

```shell
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
