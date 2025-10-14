---
title: Release Notes
description: The latest release information for the [!DNL Adobe Commerce Optimizer].
role: Admin, Architect, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
---
# Release Notes

The following release notes contain updates to [!DNL Adobe Commerce Optimizer].

## October 2025

**Release date**: October 14, 2025

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

The [!DNL Commerce Optimizer Salesforce Commerce Connector] is a new App Builder integration starter kit that enables Commerce administrators and developers to seamlessly connect Salesforce B2C Commerce catalog data with [!DNL Commerce Optimizer].<!--COMOPT-536-->

**For Admins:**
  * Catalog updates in Salesforce (products, prices, metadata, pricebooks) are automatically synchronized with Commerce Optimizer—no manual intervention required.
  * The integration operates independently from Adobe Commerce, reducing complexity and potential points of failure.
  * Admins can rely on scheduled regularly schedule updates to ensure accurate catalog data within Commerce Optimizer, improving merchandising and product recommendations.

**For Developers:**
 * The starter kit provides a streamlined, extensible framework for ingesting Salesforce catalog data into SaaS Merchandising Services.
 * Reference implementations, design documentation, and code samples are available to accelerate custom integrations or troubleshooting.<!--COMOPT-536-->

>[!ENDSHADEBOX]

### Layered Search

* GA release for the following advanced search capabilities: layered search using `startsWith` and `contains`. [Learn more](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).


>[!ENDSHADEBOX]

## August 2025

**Release date**: August 28, 2025

>[!BEGINSHADEBOX]

### EU region now available

European Union region (eu1) support for customer IMS organizations is now available. You can now select **European Union** as a **Region** when [adding a Commerce Optimizer instance](./get-started.md#step-1-create-an-instance) in the Cloud Manager. The European Union region is only available for production environments.

The base production URLs for the European Union region are:

* Admin: `https://eu1.admin.commerce.adobe.com`
* REST and GraphQL: `https://eu1.api.commerce.adobe.com`

![create instance](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

>[!ENDSHADEBOX]
