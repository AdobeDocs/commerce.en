---
title: Customer Readiness Checklist
description: Learn how to prepare for a bulk data migration to Adobe Commerce as a Cloud Service with a readiness checklist covering engagement, machine, source, and target.
feature: Cloud
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
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
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Customer readiness checklist

{{bulk-data-early-access}}

Use this checklist to prepare for a data migration from an [!DNL Adobe Commerce] PaaS or on-premises instance to [!DNL Adobe Commerce as a Cloud Service] using the bulk data migration tool.

The migration tool is distributed as part of the Commerce Deployed Engineering (CDE) engagement process. Access to the tool is gated on a signed CDE agreement, and it is not publicly downloadable. The typical engagement lifecycle is:

1. **CDE Discovery**: Complete the initial scoping call, assess data footprint and complexity, and complete the scoping questionnaire.
1. **Deal Sign**: Put the commercial agreement in place and agree on the migration scope. At this stage, you are granted access to the migration tool.
1. **CDE Co-Innovation / Support**: Work jointly with Adobe to install the tool in your environment and execute test migrations.
1. **Go Live**: Run the production cutover migration and complete data integrity verification.

This checklist covers what you need to have in place before the tool is shared (Stage 1) and what you need ready to begin configuration and execution once you have the tool (Stage 2). Review it with your Adobe team early, because some items require Adobe coordination and should not be assumed or estimated.

## Stage 1: before tool access

Complete or confirm the following before the migration tool and documentation are provided.

- **CDE engagement signed** — A signed CDE agreement must be in place. Tool access is granted at the Deal Sign stage of the CDE lifecycle. Coordinate with your Adobe team.
- **Scoping questionnaire completed** — A scoping questionnaire is completed during CDE Discovery to validate that the migration is feasible with the current tool capabilities and to assess data footprint and complexity. Ensure this is completed with your Adobe team before you move forward.
- **No HIPAA data confirmed** — The source instance must not contain HIPAA-regulated data. Confirm this before you proceed.
- **IP addresses provided** — Provide your Adobe team with the list of IP addresses from which the migration tool runs. This is required for network access to be configured on the Adobe side.
- **Target instance provisioned** — The target [!DNL Adobe Commerce as a Cloud Service] instance must be provisioned before migration begins. Coordinate with your Adobe team to confirm the instance is ready.

## Stage 2: before running the migration

After you have access to the tool, make the following items ready before you begin configuration and execution.

### Migration machine

The migration tool runs on a machine you control, such as a dedicated jump box. This machine must meet the following requirements.

- **[!DNL Docker] and [!DNL Docker Compose] installed** — The tool is [!DNL Docker]-based. Both `docker` and `docker compose` (or the legacy `docker-compose`) must be installed and working on the migration machine.
- **[!DNL Docker] execution permissions** — The user running the migration must be permitted to execute [!DNL Docker] commands. On [!DNL Linux], the user must be in the `docker` group. On [!DNL macOS] and [!DNL Windows], [!DNL Docker Desktop] must be running and accessible.
- **Writable working directory** — The directory where the migration tool is extracted must be fully writable by the migration user. The tool writes logs, cache, [!DNL Composer] dependencies, and generated files during execution.
- **Sufficient disk space** — Ensure adequate free disk space for extracted data, [!DNL Docker] images, and log output. Space requirements vary depending on the size of the source database.
- **On-premises sources: direct database connectivity from the migration machine** — For on-premises source instances, the migration machine must have direct network access to the source database. The tool does not establish on-premises database connectivity automatically. Confirm that the host, port, and credentials are reachable from the migration machine before you run any migration command.
- **PaaS sources: Magento Cloud CLI installed and SSH key registered** — For [!DNL Adobe Commerce] Cloud (PaaS) source instances, the [Magento Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) must be installed on the migration machine. Your SSH public key must also be registered in your [!DNL Adobe Commerce] Cloud account. See the [Secure connections guide](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) for instructions.

### Source instance

- **Source store APIs accessible** — The source store's REST and GraphQL APIs must be accessible from the migration machine. Ensure that no HTTP Basic Auth or network restriction blocks API traffic to the source URL.
- **Source OAuth credentials** — The migration tool uses OAuth to authenticate with the source store. Create or confirm an integration in the source [!UICONTROL Admin] ([!UICONTROL System] > [!UICONTROL Extensions] > [!UICONTROL Integrations]) and have the consumer key, consumer secret, access token, and access token secret ready.
- **PaaS sources: Magento Cloud API token** — Generate a [!DNL Magento Cloud] API token from your [Magento Cloud account settings](https://accounts.magento.cloud) under [!UICONTROL Account Settings] > [!UICONTROL API Tokens]. Required only when the source is an [!DNL Adobe Commerce] Cloud (PaaS) instance.
- **On-premises sources: source database credentials** — Have the source [!DNL MySQL] database connection details ready for configuration: `host`, `port`, `user`, `password`, and `database` name.
- **Ability to pause Magento cron** — You must be able to stop [!DNL Magento] cron on the source instance for the duration of data extraction to prevent concurrent writes.
- **Ability to pause integrations and background jobs** — Any third-party integrations (ERP, OMS, PIM), scheduled jobs, or background processes that write to the source database must be pausable for the extraction window.
- **Phased migration only: ability to enable and disable maintenance mode** — If you run a phased migration with a maintenance window (Option B), you must be able to enable and disable [!DNL Magento] maintenance mode on the source instance.

### Target instance

- **Tenant ID and organization ID confirmed** — Obtain your `TARGET_TENANT_ID` and `TARGET_ORG_ID` from your Adobe team before configuration.
- **IMS OAuth Server-to-Server credentials** — Required for the migration tool to authenticate with the target. Generated through the [Adobe Developer Console](https://developer.adobe.com/console/). You need [!UICONTROL Developer] or [!UICONTROL Admin] access to your Adobe organization, because basic user access is not sufficient to create credentials. Coordinate with your Adobe team for the correct product profile to select, and have the client ID (`ADOBE_IMS_CLIENT_ID`) and client secret (`ADOBE_IMS_CLIENT_SECRET`) ready.
- **CDMS endpoint URL** — Provided by your Adobe team. Do not attempt to infer this value. You need both the pre-production endpoint for sandbox and test migrations and the production endpoint for live cutover migrations.
- **Core configuration aligned between source and target** — Core configuration data, such as store settings and system configuration, is not migrated by the tool. Set it up manually on the target to match the source before migration.
- **B2B stores: B2B features consistently configured** — If the source is a B2B-enabled store, ensure that the relevant B2B [!UICONTROL Admin] settings are consistently configured on both source and target before migration. Refer to the [migration guide](migration-guide.md) for the specific settings required.

### Migration planning

- **Migration approach decided** — Determine which approach fits your use case before you start. Option A (single phase, no maintenance mode) suits dry runs, dev or sandbox environments, or any migration where the source can remain live during extraction. Option B (multi-phase, maintenance mode required) is required for production migrations where the source must be frozen during extraction to ensure data consistency.
- **Maintenance window planned (Option B only)** — If you use Option B, plan and communicate the maintenance window in advance. The source instance is unavailable to end users for the duration of the extraction and loading phases.
- **Store view code confirmed** — Identify the store view code (`STORE_CODE`) on the source instance. It defaults to `default` but must match the actual code in [!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]. An incorrect store code can affect data operations during migration.

## Summary

| Area | Key items |
| --- | --- |
| Pre-engagement | CDE signed, scoping questionnaire completed, no HIPAA data, IP addresses provided, target instance provisioned |
| Migration machine | [!DNL Docker] installed and permitted, write access, disk space, database connectivity (on-premises) or Cloud CLI (PaaS) |
| Source instance | APIs accessible, OAuth credentials, database credentials (on-premises), Cloud CLI token (PaaS), ability to pause cron and integrations |
| Target instance | Tenant and organization IDs, IMS credentials, CDMS endpoint, core configuration aligned with source |
| Planning | Migration approach (Option A or B), maintenance window if Option B, store code confirmed |

After you confirm all items, you are ready to verify service access with the [migration service access guide](cdms-access.md), and then begin the configuration and execution steps in the [migration guide](migration-guide.md).
