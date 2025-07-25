---
title: Installation
description: Learn how to install [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Onboarding and Installation

Install the Catalog Service to request and receive product data from a Commerce instance using the [Catalog Service GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). The Catalog Service is delivered as a composer metapackage from the repo.magento.com repository.

>[!NOTE]
>
>If your Commerce instance uses Live Search or Product Recommendations, the Catalog Service is installed or updated automatically when you onboard or upgrade those services. For details, see the installation instructions for [Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) and [Product Recommendations](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure).


## System requirements

**Software requirements**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3, 8.4
- Composer: 2.x

**Supported platforms**

- Adobe Commerce on cloud infrastructure: 2.4.4+
- Adobe Commerce on premises: 2.4.4+

## Endpoints

[!DNL Catalog Service] has two endpoints available for onboarding:

- Sandbox (`https://catalog-service-sandbox.adobe.io/graphql`)—used for testing and validation before going live
- Production (`https://catalog-service.adobe.io/graphql`)—used for live traffic for Commerce merchants and websites

All Commerce test instances use the Sandbox endpoint.

Perform all Load testing on the Sandbox endpoint. Before you begin load testing, submit a [Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) so that the Services team can anticipate the additional server traffic.

## Installation and configuration

To get started with [!DNL Catalog Service] for Adobe Commerce, the following steps are required:

- Install the Catalog Service extension (`magento/catalog-service`)
- Configure the service and data export
- Access the service

### Install the Catalog Service extension

>[!BEGINSHADEBOX]

**Prerequisite**

- Access [repo.magento.com](https://repo.magento.com) to install the extension. For key generation and obtaining the necessary rights, see [Get your authentication keys](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). For cloud installations, see the [Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Access to the command line of the Adobe Commerce application server.

>[!ENDSHADEBOX]

Install the latest version of the Catalog Services extension (`magento/catalog-service`) on an Adobe Commerce instance that is running Adobe Commerce version 2.4.4 or later. The Catalog Service is delivered as a composer metapackage from the [repo.magento.com](https://repo.magento.com) repository.

>[!BEGINTABS]

>[!TAB Cloud infrastructure]

Use this method to install the [!DNL Catalog Service] for a Commerce Cloud instance.

1. On your local workstation, change to the project directory for your Adobe Commerce on cloud infrastructure project.

   >[!NOTE]
   >
   >For information about managing Commerce project environments locally, see [Managing branches with the CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) in the _Adobe Commerce on Cloud Infrastructure User Guide_.

1. Check out the environment branch to update using the Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Add the Catalog Service module.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Update package dependencies.

   ```bash
   composer update "magento/catalog-service"
   ```

1. Add, commit, and push the code changes for the `composer.json` and `composer.lock` files to the cloud environment.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   Pushing the updates to the cloud environment initiates the [Commerce cloud deployment process](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) to apply the changes. Check the deployment status from the [deploy log](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB On-premises]

Use this method to install the [!DNL Catalog Service] for an on-premises instance.

1. Use Composer to add the Catalog Service module to your project:

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Update dependencies and install the extension:

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Upgrade Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Clear the cache:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >In some cases, particularly when deploying to production, you might wish to avoid clearing compiled code because it can take some time. Ensure that you back up your system before making any changes.

>[!ENDTABS]

### Configure the service and data export

After you install the [!DNL Catalog Service], complete the following tasks to integrate the Catalog service with your Adobe Commerce instance. This integration enables the data synchronization and communication between the Commerce instance, the Catalog Service, and other supporting services. Data synchronization is handled by the [SaaS Data Export extension](../data-export/overview.md).

1. Set up the [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) by specifying the API keys and selecting a SaaS Data Space.

   Commerce Services Connector setup is a one-time process required to use Adobe Commerce services like the Catalog Service, Live Search, and Product Recommendations. If you have already configured the connector for another service, skip this step.

1. Perform an initial data sync from the [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   The initial sync can take from a few minutes to hours depending on the catalog size. You can monitor the synchronization status from the Data Management dashboard. After the initial sync, the Catalog exports product data on an ongoing basis to keep the services up to date.

   >[!NOTE]
   >
   >You can also start the initial sync from the command line using the Commerce CLI. See [Initial sync](../data-export/data-export-cli-commands.md#initial-sync) in the _SaaS Data Export Guide_.

To ensure that the catalog export is running correctly:

- [Confirm that cron jobs are running](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verify that the indexers are running from the [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) or by using the Commerce CLI command `bin/magento indexer:info`.
- Verify that the `Catalog Attributes Feed, Product Feed, Product Overrides Feed`, and `Product Variant Feed` indexers are set to `Update by Schedule`.

### Monitor and troubleshoot data synchronization

From the Commerce Admin, you can monitor the synchronization process using the [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Use the [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) and logs to manage and troubleshoot the process.
