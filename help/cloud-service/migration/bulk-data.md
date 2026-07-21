---
title: Bulk Data Migration Tool
description: Learn how to use the bulk data migration tool to migrate data from your existing Adobe Commerce on Cloud instance to [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-06-18T16:10:45.417Z'
TQID: 'https://experienceleague.adobe.com/4Zx1cFtsyfuy21Af6Ov9pU7ndMW35NyCwlcdlKNTk6Q'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Bulk data migration tool

>[!IMPORTANT]
>
>The bulk data migration tool is currently in Early Access. Access is provided exclusively through the Commerce Deployed Engineering (CDE) engagement process.

The bulk data migration tool is a Docker-based CLI that system integrators run on their own migration machine. It connects to the source instance, extracts first-party core commerce data, uploads it to Adobe's migration service (Commerce Data Migration Service), and monitors progress through to completion. For more information on the overall migration process, see the [Migration overview](./overview.md).

>[!NOTE]
>
>The tool supports migrating first-party core commerce data only. Custom data migration is not supported.

## Eligibility and access

Before requesting access, confirm that your project meets all the following requirements:

- **Healthcare add-on:** The tool is not available to customers with the Healthcare (HIPAA) add-on.
- **CDE engagement:** A signed Commerce Deployed Engineering (CDE) engagement is required. Contact your Adobe representative to initiate the engagement.
- **Scoping questionnaire:** A completed CDE data migration scoping questionnaire is required before tool access is granted. Your Adobe representative provides this questionnaire as part of the CDE engagement.

## Architecture

The following image details the architecture and key components for using the bulk data migration tool.

![Bulk data migration tool architecture diagram showing PaaS to SaaS data flow](../assets/bulk-data-diagram.png){zoomable="yes"}

### Components

| Component | Role |
| --------- | ---- |
| **Bulk data migration tool** | The Docker-based CLI that the system integrator runs on the migration machine, which orchestrates the full pipeline by reading the schema and data from the source, uploading extracted data to Adobe's migration service, and driving status transitions. |
| **Source instance (PaaS or on-premises)** | The migration source. The tool connects through REST and GraphQL APIs and through an SSH tunnel (PaaS) or through a direct database connection (on-premises) for data extraction. |
| **Commerce Data Migration Service (CDMS)** | Adobe-managed backend service that registers migrations, coordinates state transitions, issues pre-signed upload URLs for extracted data, loads data into the target instance, and runs post-load integrity verification. |
| **[!DNL Adobe Commerce as a Cloud Service]** | The SaaS-based version of Adobe Commerce and your migration target. Receives loaded data and exposes Catalog, Live Search, and pricing rule services used during integrity verification. |

## Migration workflow

A migration runs in three phases:

1. **Extract** — The tool reads schema and data from the source instance (PaaS or on-premises) and uploads it to Adobe's migration service.
1. **Load** — CDMS loads the extracted data into the target [!DNL Adobe Commerce as a Cloud Service] tenant and processes catalog media. Catalog data automatically flows to the Catalog Service and becomes available to Live Search and Product Recommendations once loading completes.
1. **Verify** — CDMS performs automated integrity checks. See [Data integrity verification](#data-integrity-verification).

## Tool distribution

The tool is distributed as part of the CDE engagement. Your Adobe representative provides the tool package, which includes:

- The Docker-based CLI and build configuration
- An `.example.env` configuration template with documentation for all required environment variables
- Comprehensive technical documentation covering the tool's architecture, configuration reference, custom transformation and test frameworks, and troubleshooting guides

For detailed setup and operational instructions, refer to the documentation included in the tool distribution package.

## Operational guide

The following sections describe how to configure and run a migration.

### Prerequisites

Before running the tool, ensure the following are in place:

- **Docker** — Docker must be installed and running on the migration machine.
- **Target instance** — Create a new [!DNL Adobe Commerce as a Cloud Service] instance. See [Create an instance](../getting-started.md#create-an-instance).
- **Catalog configuration** — Note your current Catalog configuration settings in the [!DNL Commerce Admin] before migration. Configuration settings are not migrated automatically and must be applied to the target instance independently.
- **B2B configuration** — If your source instance uses B2B features, apply the equivalent B2B configuration to the target instance before running the migration.
- **IMS credentials** — Obtain your IMS Client ID, client secret, IMS scopes, IMS URL, and IMS organization ID from the **Credentials** section of your project in the [Adobe Developer Console](https://developer.adobe.com/console/).

### Configure the tool

Set the following environment variables in the `.env` file:

- Connection details for your source MySQL database
- The target tenant ID for your [!DNL Adobe Commerce as a Cloud Service] instance
- Your IMS credentials (Client ID, client secret, IMS scopes, IMS URL, IMS organization ID)
- The CDMS endpoint URL for your region

Refer to the `.example.env` file in the tool package for the full configuration reference and additional options.

### Prepare your network and instances

For PaaS source instances, open an SSH tunnel to the source database before running the tool:

```bash
magento-cloud tunnel:open
```

For on-premises source instances, ensure the migration machine has direct database access to the source.

### Run a migration

The tool supports two migration approaches:

#### Single-phase migration

Run the full migration, including the extract, load, and verify steps in a single operation. This approach is appropriate for sandbox and development environments where downtime is not a concern.

#### Multi-phase migration with maintenance mode

For production cutover, split the migration into phases and apply maintenance mode to prevent data changes during the final load:

1. Run the initial extract and load while the source instance is live to pre-populate the target instance.
1. Enable maintenance mode on the source instance to prevent further data changes.
1. Run the final incremental extract and load to capture any changes made since the initial run.
1. Complete the [data integrity verification](#data-integrity-verification) and then cut over to the target instance.

Refer to the migration guide in the tool distribution package for the exact commands and phase flags for each option.

### Resume an interrupted migration

If a migration run is interrupted, re-run the same command to resume from the last completed checkpoint. The tool tracks migration state and picks up where it left off. Refer to the tool documentation for resume flags and behavior.

### Logs and debugging

The tool outputs logs to the console during each phase. Log verbosity is configurable in the `.env` file. For troubleshooting guidance, refer to the troubleshooting section in the technical documentation included with the tool distribution package.

## Data integrity verification

After the load phase, CDMS performs the following automatic checks to confirm the accuracy and completeness of the migrated data:

- **API-based verification** — Compares REST and GraphQL API responses from pre-extracted source queries with corresponding records in the target instance. Discrepancies are visible in the migration status.

- **Record count verification** — Compares the number of extracted records with the number of records loaded.

**On-demand verification (optional)**

>[!NOTE]
>
>This process is resource-intensive and should only be used in sandbox environments.

You can manually trigger a comprehensive verification of all system records. This includes complete API-based verification using all pre-extracted REST and GraphQL API responses and a detailed report of any inconsistencies found.
