---
title: 'Bulk Data Migration Tool'
description: Learn how to use the Bulk Data Migration Tool to migrate data from your existing Adobe Commerce on Cloud instance to [!DNL Adobe Commerce as a Cloud Service].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Architect
---

# Bulk data migration tool

The bulk data migration tool follows a distributed architecture that enables secure and efficient data migration from PaaS to SaaS environments. This tool is designed for solution implementers to migrate data from an existing Adobe Commerce on Cloud instance (PaaS) to [!DNL Adobe Commerce as a Cloud Service] (SaaS). For more information on the migration process, see the [Migration overview](./overview.md).

>[!NOTE]
>
>The bulk data migration tool only supports migrating first-party core commerce data. Custom data migration is not currently supported.

The following image details the architecture and key components for using the Bulk data migration tool.

![Bulk Data Migration Tool architecture](../assets/bulk-data-diagram.png)

## Migration workflow

The bulk data migration workflow consists of the following steps:

1. Set up a new environment for your migration.
1. Copy your data from your old system.
1. Move your data into the new system.
1. Make your product catalog available in the new system.
1. Confirm that your data migrated correctly.

The following sections describe these steps in detail.

## Access the bulk data migration tool

The availability of the bulk data migration tool is as follows:

- **Mid-July 2025** - To access the bulk data migration tool, submit a support ticket.
- **Mid-August 2025** - The bulk data migration tool will be publicly available and will accessible from this page.

## Create target environment

The solution implementer (SI) creates a target environment for the migration. This environment is used to store the data that is migrated from the source instance.

First, [create a new [!DNL Adobe Commerce as a Cloud Service] (SaaS) instance](../getting-started.md#create-an-instance).

### Configure extraction tool

The extraction tool is used to extract data from the source instance.

1. Download the extraction tool from the link provided to you by Adobe.
1. Set the following environment variables in the extraction tool:
   - Connection details to your existing MySQL database
   - The target tenant ID for your [!DNL Adobe Commerce as a Cloud Service] instance
   - Your IMS credentials, including:
      - Client ID
      - Client secret
      - IMS scopes
      - IMS URL
      - IMS organization ID

### Extract data

Before running the extraction tool, the solution implementer must establish an SSH tunnel to the PaaS database using:

```bash
magento-cloud tunnel:open
```

Then run the extraction tool, which will: 

1. Connect to the PaaS database, analyze its schema, and compare it with the SaaS tenant schema details.
1. Generate an extraction and transformation plan based on the common schema elements between PaaS and SaaS.
1. Extract the data using Catalog Data Management Service (CDMS) authentication.

### Load data

Run the load data tool provided by Adobe. This tool will:

1. Connect to the SaaS tenant database using a migration account.
1. Generate a loading plan.
1. Execute the plan, moving data to the SaaS tenant database in batches.
1. Process catalog media and transfer it to the target environment.
1. Flushes the SaaS Redis cache and invalidates database indexes for the tenant.

### Catalog data ingestion

After the data loads, the catalog data automatically flows from the SaaS tenant database to the Catalog Service.

The Catalog Service shares this data with Live Search and Product Recommendations. No manual intervention is required for this process. The data will be available in all services once the ingestion completes.

### Data integrity verification

After migration, CDMS performs the following automatic data integrity checks to ensure the accuracy and completeness of the migrated data:

**API-based verification**

During verification, CDMS compares REST and GraphQL API responses from previously run queries with corresponding records from the target instance. Any discrepancies are visible in the migration status.

**Database-level verification**

During verification, CDMS counts the number of extracted records and compares that number to the amount of records loaded.

**On-demand verification (optional)**

You can also manually trigger comprehensive verification of all system records:

>[!NOTE]
>
>This process is resource-intensive and should only be used in sandbox environments.

The full verification includes:

- Complete API-based verification using all pre-extracted REST and GraphQL API responses
- Detailed report of any inconsistencies found
