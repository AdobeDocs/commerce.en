---
title: '[!DNL Adobe Commerce Optimizer Connector] Release Notes'
description: The latest release information for [!DNL Adobe Commerce Optimizer Connector] for Adobe Commerce.
feature: Services, Catalog Service, Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
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
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Adobe Commerce Optimizer Connector release notes

These release notes describe all releases for the [!DNL Adobe Commerce Optimizer Connector] and include:

![New](../assets/new.svg) New features
![Fixed issue](../assets/fix.svg) Fixes and improvements
![Known issue](../assets/bug.svg) Known issues

## 2026 Releases

### 1.0.13 Release

_May 6, 2026_

![Fix](../assets/fix.svg) **Improved Connector configuration instructions**–Updated the Commerce Optimizer configuration page in the Commerce Admin to link to the _Adobe Commerce Connector Guide_. <!--COMOPT-1922-->
![Fix](../assets/fix.svg) **Connector metadata enhancement**–The Adobe Commerce Optimizer Connector now includes its installed version in the metadata header. This improvement enables teams to quickly identify which connector version is in use during troubleshooting or support engagements.<!--MDEE-1323-->

### 1.0.12 Release

_April 2, 2026_

![New](../assets/new.svg) **Added support for the Categories feed in `saas:resync` command**–You can now easily refresh and view your latest category data using the `saas:resync` CLI command:

```terminal
bin/magento saas:resync --feed=categories
```

### 1.0.11 Release

_March 10, 2026_

![Fixed issue](../assets/fix.svg) Fixed a compatibility issue that blocked access to the Commerce Services Connector configuration page from the Commerce Admin System and Configuration menus when Adobe Commerce Optimizer Connector is installed on a Commerce instance.  Now, you can access the Commerce Services Connector configuation page when both extensions are installed. <!--MDEE-1322-->


### v1.0.10 Release

_March 09, 2026_

![Fix](../assets/fix.svg) If you access the Data Feed Sync Status page before completing the Connector configuration, you are now automatically redirected to the Connector configuration page. This guided flow ensures that the Connector setup is completed and helps prevent errors caused by missing configuration settings that could result in failed or incomplete status items.<!--MDEE-1296-->

### v1.0.9 Release

_March 01, 2026_

General availability release of the Adobe Commerce Optimizer Connector.

>[!NOTE]
>
>If you participated the Beta program for the Adobe Commerce Optimizer Connector and have an earlier version of the extension installed, upgrade to the General availability version to receive the latest updates.

