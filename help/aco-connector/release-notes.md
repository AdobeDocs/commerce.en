---
title: "[!DNL Adobe Commerce Optimizer Connector] Release Notes"
description: "The latest release information for [!DNL Adobe Commerce Optimizer Connector] for Adobe Commerce."
feature: Services, Catalog Service, Release Notes

---
# Adobe Commerce Optimizer Connector release notes

These release notes describe all releases for the [!DNL Adobe Commerce Optimizer Connector] and include:

![New](../assets/new.svg) New features
![Fixed issue](../assets/fix.svg) Fixes and improvements
![Known issue](../assets/bug.svg) Known issues

## 2026 Releases

### 1.0.12 Release

_April 2, 2026_

![Fix](../assets/fix.svg) **Support for Categories Feed in `saas:resync` command **–You can now easily refresh and view your latest category data using the `saas:resync` CLI command: 

```terminal
bin/magento saas:resync --feed=categories

### v1.0.11 Release

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

