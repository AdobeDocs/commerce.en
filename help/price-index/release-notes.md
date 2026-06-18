---
title: "[!DNL Catalog Adapter] Release Notes"
description: The latest release information for [!DNL Catalog Adapter] for Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
TQID: https://experienceleague.adobe.com/btPlBYpdRdf-gMfqSv2px6iMfiI3FfXJSN40j61HXOU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
---
# [!DNL Catalog Adapter] Extension Release Notes

These release notes describe the latest versions of the [!DNL Catalog Adapter] extension. Support is provided for the current major released version. Release notes for older versions are provided for reference.

Updates include:

![New](../assets/new.svg) New features
![Fix](../assets/fix.svg) Fixes and improvements
![Bug](../assets/bug.svg) Known issues


>[!NOTE]
>
>The [Catalog Adapter extension](catalog-adapter.md) disables Adobe Commerce price indexing. If you have installed it, you can check the version installed on your system using composer. In some cases, you might want to upgrade the catalog adapter extension on your system to pick up fixes or new capabilities without updating the Commerce Service version.

## Current major version

## 1.0.11 Release

_June 18, 2026_

![Fix](../assets/fix.svg) Add php 8.5. <!--MDEE-1368-->

## 1.0.10 Release

![Fix](../assets/fix.svg) Fixed an issue where price queries for imported or newly created bundle products could result in internal server errors because the system attempted to use a concatenated SKU for lookup instead of the correct, valid SKU. Price queries for bundle products now use the appropriate SKU and resolve correctly.<!--MDEE-1040-->

## 1.0.9 Release

![Fix](../assets/fix.svg) Added compatibility for PHP 8.4. <!--MDEE-941-->

## 1.0.8 Release

![Fix](../assets/fix.svg) Fixed an issue that caused an error in the exception log when adding configurable product variants with numeric SKUs to the wishlist. <!--MDEE-876-->
