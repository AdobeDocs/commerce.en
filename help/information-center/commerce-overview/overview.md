---
title: Commerce Overview
description: Learn about the Adobe Commerce product model, including Adobe Commerce, Commerce Foundation, Adobe Commerce Optimizer, and Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
---

# Commerce overview

Adobe Commerce spans several products and platform options that share a common commerce model. Use this page to understand what each product is before you compare architectures or choose a starting point.

## What is Adobe Commerce?

[!DNL Adobe Commerce] is the core commerce platform for building and running online stores. It's available on Adobe-managed cloud infrastructure (Adobe Commerce on Cloud) or on-premises, giving you deployment control over the platform's infrastructure. See the [Adobe Commerce getting started guide](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview).

## What is Commerce Foundation?

[!DNL Commerce Foundation] is the base commerce capability beneath the storefront and merchandising layers. It includes capabilities such as:

- Catalog and product data
- Pricing and promotions
- Cart and checkout
- Customer and account operations
- Order processing
- Multi-site and multi-channel support
- Integrations for payment, tax, shipping, inventory, and fulfillment

>[!NOTE]
>
>Older strategy material may call Commerce Foundation "Core Commerce" or the "PHP Foundational Layer." Those are legacy terms. Use Commerce Foundation in current customer-facing content.

Commerce Foundation is delivered through [!DNL Adobe Commerce] on Cloud, [!DNL Adobe Commerce] on premises, or [!DNL Adobe Commerce as a Cloud Service], depending on the selected platform. Core platform operations and transactions are accessed through the Commerce Foundation APIs. See [APIs](../apis/overview.md).

## What is Adobe Commerce Optimizer?

[!DNL Adobe Commerce Optimizer] is a SaaS experience and merchandising layer for catalog discovery, search, recommendations, merchandising rules, catalog views, and related analytics. It can be used in two ways:

- With [!DNL Adobe Commerce] on Cloud or on premises through the [!DNL Adobe Commerce Optimizer Connector].
- As a stand-alone service connected to an existing or third-party commerce backend.

[!DNL Adobe Commerce Optimizer] doesn't replace the transactional system for cart, checkout, orders, payments, tax, shipping, inventory, or fulfillment. Those responsibilities remain with Commerce Foundation or the connected third-party commerce platform. See [What is Adobe Commerce Optimizer?](/help/optimizer/overview.md).

## What is Adobe Commerce as a Cloud Service?

[!DNL Adobe Commerce as a Cloud Service] is a cloud-native, fully managed SaaS version of Adobe Commerce, where Adobe handles infrastructure, updates, and scaling. Commerce services are installed and configured automatically, so administrators don't manage individual service extensions. See the [[!DNL Adobe Commerce as a Cloud Service] overview](/help/cloud-service/overview.md).

## Related guidance

- [Choose a Commerce option](../choose-commerce-option/overview.md)
- [Architecture options](../architecture-options/overview.md)
