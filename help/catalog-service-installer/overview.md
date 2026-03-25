---
title: '[!DNL Catalog Service Installer]'
description: 'Learn how the Catalog Service Installer registers the Catalog Service feature with your Adobe Commerce SaaS environment.'
recommendations: noCatalog
exl-id: 
---
# [!DNL Catalog Service Installer] for Adobe Commerce

The **[!DNL Catalog Service Installer]** (`magento/catalog-service-installer`) is an Adobe Commerce module that **registers the Catalog Service feature** for the SaaS environment ID associated with your instance. Registration tells Adobe Commerce services which capabilities are enabled for that environment so [Storefront [!DNL Catalog Service]](../catalog-service/overview.md) can operate correctly alongside the [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions) configuration.

The installer does not replace the main Catalog Service extension or onboarding steps described in **[Onboarding and Installation](../catalog-service/installation.md)**—it handles service-side feature registration tied to your SaaS environment.

## Registration behavior

The module keeps Catalog Service registration in sync with the lifecycle of the package and your SaaS configuration:

| Event | What happens |
| ----- | ------------ |
| **Module installed** | A request is sent to the registration service to **enable** the Catalog Service feature for the current SaaS environment ID. |
| **Module uninstalled** | A request is sent to the registration service to **remove** the Catalog Service feature for that environment. |
| **SaaS environment ID changes** | When the ID is updated—through **configuration import** or **saving configuration** in the Admin—the feature is **registered again** for the new environment so it matches your active Commerce Services setup. |

>[!NOTE]
>
> Ensure your [SaaS project and environment configuration](../landing/saas.md) is correct before or when using Catalog Service. An incorrect or stale environment ID can cause registration to target the wrong SaaS scope.

## Related information

* [[!DNL Catalog Service] overview](../catalog-service/overview.md)—architecture, GraphQL endpoints, and storefront use cases
* [Onboarding and Installation](../catalog-service/installation.md)—Composer install, Admin configuration, and verification
* [[!DNL Commerce Storefront Catalog Service Installer] Release Notes](release-notes.md)—package version and compatibility details
