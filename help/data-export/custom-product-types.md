---
title: Support for Custom Product Types in SaaS Catalog Data Export
description: Learn how the Commerce Storefront MCP catalog enablement module lets SaaS Data Export represent unrecognized, custom third-party product types as simple products in catalog data sent to Live Search and Catalog Service.
role: Admin, Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Support for custom product types in SaaS catalog data export

>[!IMPORTANT]
>
>Support for custom product types is currently in **Early Access** as part of the [!DNL Commerce Storefront MCP]. Availability, packaging, and installation requirements are subject to change before general availability. Contact your Adobe account manager for eligibility.

## Overview

[!DNL SaaS Data Export] recognizes the standard Adobe Commerce product types (simple, configurable, bundle, and so on) when it prepares catalog data for connected Commerce Services such as [Live Search](../live-search/overview.md) and [Catalog Service](../catalog-service/overview.md). Third-party extensions can introduce **custom product types** that [!DNL SaaS Data Export] does not natively recognize.

The Commerce Storefront MCP catalog enablement module lets [!DNL SaaS Data Export] represent these unrecognized, custom product types as **simple products** in the outbound catalog payload, so shoppers using the [!DNL Commerce Storefront MCP] can discover them through catalog-backed services.

## Scope of the behavior

- Representing a custom product type as a simple product applies only to catalog data sent to [!DNL Live Search] and [!DNL Catalog Service]. It does not change the product type stored in Adobe Commerce.
- No Admin setting or runtime configuration is required. Standard product types continue to export normally.
- The module targets custom product types introduced by third-party extensions, not the standard Commerce product types.

## 1. Install the module

To enable the Commerce Storefront MCP catalog enablement module, run the following from the command line:

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## 2. Resync your catalog data

Installing the module does not change the underlying product data in Adobe Commerce, so existing custom product type items are not automatically re-exported. To apply the new simple product representation to catalog data that was already synced before you installed the module, manually resync your catalog data. See [Manually resync data](data-sync-manage.md#manually-resync-data).

## Compatibility and limitations

This module is in Early Access and is supported in Adobe Commerce versions 2.4.4 and newer. Deployment types and limitations will be documented here as they are confirmed.
