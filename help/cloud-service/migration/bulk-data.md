---
title: Bulk Data Migration Tool
description: Learn how to use the bulk data migration tool to migrate data from your existing Adobe Commerce on Cloud instance to [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
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
>The tool supports migrating first-party core commerce data only. Custom data migration is not supported. Configuration settings, such as store settings and system configuration, are not migrated automatically and must be applied to the target instance independently before migration.

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
| **Commerce Data Migration Service (CDMS) API** | Adobe-managed REST API that registers migrations, coordinates state transitions, and issues pre-signed upload URLs for extracted data. The migration tool connects to this API using the CDMS endpoint URL and IMS credentials in your `.env` configuration. |
| **Commerce Data Migration Service (CDMS) worker** | Adobe-managed background service that loads extracted data into the target instance and runs post-load integrity verification. |
| **[!DNL Adobe Commerce as a Cloud Service]** | The SaaS-based version of Adobe Commerce and your migration target. Receives loaded data and exposes Catalog, Live Search, and pricing rule services used during integrity verification. |

### Data flow

Data moves through the components in the following sequence:

1. The bulk data migration tool reads the database schema and data from the source instance, through an SSH tunnel for [!DNL Adobe Commerce on Cloud] or a direct database connection for on-premises.
1. The tool registers the migration and uploads the extracted data through the CDMS API.
1. The CDMS worker loads the data into the target [!DNL Adobe Commerce as a Cloud Service] tenant.
1. [!DNL Adobe Commerce as a Cloud Service] ingests the loaded catalog data and builds the catalog index.
1. The Commerce Data Migration Service (CDMS) worker verifies the loaded data through REST and GraphQL across the following services:

   - **Catalog** (GraphQL) — product and category data.
   - **Live Search** (REST) — search index correctness.
   - **Pricing rules** (REST) — price and rule data.

1. The tool polls the migration status throughout and retrieves the final migration report on completion.

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

## Migration guides

The following pages demonstrate the full migration lifecycle, from preparation to execution. For a complete understanding of the migration process, review them in the following order:

1. [Customer readiness checklist](readiness-checklist.md) — Confirm the engagement, migration machine, source, and target prerequisites before you request tool access.
1. [Verify migration service access](cdms-access.md) — After obtaining access to the tool, validate network reachability, IMS authentication, and tenant authorization against the Commerce Data Migration Service (CDMS) API.
1. [Run a bulk data migration](migration-guide.md) — Configure the tool, prepare your network and instances, and begin the migration.

For the full configuration reference, custom transformation and test frameworks, and troubleshooting guidance, refer to the documentation included in the tool distribution package.

## Data integrity verification

After the load phase, CDMS performs the following automatic checks to confirm the accuracy and completeness of the migrated data:

- **API-based verification** — Compares REST and GraphQL API responses from pre-extracted source queries with corresponding records in the target instance. Discrepancies are visible in the migration status. Verification spans the following services:

  - **Catalog** (GraphQL) — validates product and category data.
  - **Live Search** (REST) — validates search index correctness.
  - **Pricing rules** (REST) — validates price and rule data.

- **Record count verification** — Compares the number of extracted records with the number of records loaded.

**On-demand verification (optional)**

>[!NOTE]
>
>This process is resource-intensive and should only be used in sandbox environments.

You can manually trigger a comprehensive verification of all system records. This includes complete API-based verification using all pre-extracted REST and GraphQL API responses and a detailed report of any inconsistencies found.
